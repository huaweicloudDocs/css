# Elasticsearch使用建议<a name="css_01_0032"></a>

Elasticsearch是开源搜索引擎，在深入使用Elasticsearch搜索引擎过程中，积累了一些经验和技巧，建议用户在使用云搜索服务时，作为参考。

## 提高索引效率<a name="section53922812102832"></a>

-   **使用多进程或多线程发送数据到Elasticsearch**

    一个单线程发送bulk请求不能够发挥一个集群的索引能力。为了更好地利用集群的资源，应该使用多线程或多进程来发送数据，提升数据处理效率。

    对于相同大小的bulk请求，通过测试可以得到最优的线程数量。可以逐步增加线程数量直至到集群中的机器Load或CPU饱和。建议使用“nodes stats“接口查看节点中的cpu和load状态，您可以通过“os.cpu.percent“、“os.cpu.load\_average.1m“、“os.cpu.load\_average.5m“和“os.cpu.load\_average.15m“参数信息了解详细信息。“nodes stats“接口的使用指导和参数解释请参见：[https://www.elastic.co/guide/en/elasticsearch/reference/6.2/cluster-nodes-stats.html\#os-stats](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/cluster-nodes-stats.html#os-stats)

    例如，在执行bulk请求时，使用的线程数量为2个，观察Load和CPU的情况，如果未饱和，可再增加线程数量。当线程数量增加到N个时，此时Load和CPU已饱和，建议就采用N个线程去执行bulk请求提高索引效率。通过测试获得最优的线程数量。

-   **增加refresh\_interval刷新的间隔时间**

    默认情况下，每个分片每秒自动刷新一次。但并不是所有场景都需要每秒刷新。在使用Elasticsearch索引大量的日志文件，想优化索引速度而不是近实时搜索，可以通过设置，降低每个索引的刷新频率。

    ```
    PUT /my_logs
    {
      "settings": {
        "refresh_interval": "30s"
      }
    }
    ```

-   **在初始化索引时，可以禁用refresh和replicas数量**

    如果需要一次导入较大数据量的数据进index里面时，可以先禁用refresh，把“refresh\_interval“设置成为“-1“，把“number\_of\_replicas“设置成“0“。当数据导入完成后，将refresh\_interval和number\_of\_replicas设置回原来的值。


## 选择合适的分片数和副本数<a name="section5630987515348"></a>

在创建索引数据时，建议指定相关的分片数和副本数，否则会使用服务器中的默认配置参数“shards=5, replicas=1“，即分片数为5，副本数为1。

分片数，与检索速度非常相关的指标，如果分片数过少或过多都会导致检索比较慢。分片数过多会导致检索时打开比较多的文件，且会导致多台服务器之间通讯慢。而分片数过少会导致单个分片索引过大，所以检索速度慢。

根据机器数、磁盘数、索引大小等设置分片数，建议单个分片不要超过30GB。总数据量除以分片数，则为分片的大小。

```
PUT /my_index
{
  "settings": {
    "number_of_shards":   1,
    "number_of_replicas":  0
  }
}
```

## 将数据存放在不同的索引<a name="section1581140613444"></a>

Elasticsearch是基于Lucene进行索引和存储数据的，主要的工作方式是密集的数据，即所有的document拥有相同的字段。

-   **避免把无关联的数据放在同一个index**

    不要把完全不同的数据结构document放在同一个index里。可以考虑创建一些较小的index，用较少的shard去存储。

-   **避免不同的type放在同一个index**

    多个type放在单个index看起来是个简单的方法，但是Elasticsearch并不是基于type来存储的，不同的type在单个index会影响效率。如果type没有非常相似的mapping，建议放到一个单独的index。

-   **同一个index里面不同type之间字段不能冲突**

    如果有两个不同的type，每个type都有同名的字段，但映射不同，这在Elasticsearch是不允许的。


## 按照时间范围创建索引<a name="section3608304314745"></a>

在Elasticsearch用于存储跟时间相关的数据时，如日志数据，建议按照时间范围创建索引，而不是把所有数据都存放到一个超级大的索引里面。

基于时间范围索引。可以开始于一个按年的索引（logs\_2014）或按月的索引（logs\_2014-10）。当数据量变得非常庞大的时候切换到一个按天的索引（logs\_2014-10-24）。

按照时间范围创建索引具有如下优势：

-   **扩容的时候根据当前数据量选择合适的shard和Replica**

    针对时间范围创建的每个索引都可以灵活的设置Shard数和Replica数，从而可以避免在一开始设置一个很大的shard来考虑扩容的情况。在集群扩容之后也可以方便的设置时间范围周期来适配集群规模。

-   **删除旧数据只需要删除旧的索引**

    ```
    DELETE /logs_2014-09
    ```

-   **利用alias机制可以在索引间灵活切换**

    例如，将logs\_current的alias机制中的logs\_2014-09索引删除，并在此alias机制中新增logs\_2014-10索引。

    ```
    POST /_aliases
    {
      "actions": [
        { "add":    { "alias": "logs_current",  "index": "logs_2014-10" }},
        { "remove": { "alias": "logs_current",  "index": "logs_2014-09" }}
      ]
    }
    ```

-   **针对不再更新的索引，如上周或者上月的索引，进行索引优化以提高查询效率**

    将logs\_2014-09-30索引下多个小segment合并成一个大的分片，以提高查询效率。

    7.x之前版本

    ```
    PUT /logs_2014-09-30/_settings
    { "number_of_replicas": 0 }
    
    POST /logs_2014-09-30/_forcemerge?max_num_segments=1
    
    PUT /logs_2014-09-30/_settings
    { "number_of_replicas": 1 }
    ```

    7.x之后版本

    ```
    PUT /logs_2014-09-30/_settings 
    { "number_of_replicas": 0 } 
    
    POST /logs_2014-09-30/_forcemerge
    {
      "max_num_segments":1
    }
    
    PUT /logs_2014-09-30/_settings 
    { "number_of_replicas": 1 }
    ```


## 优化索引配置<a name="section1425508814337"></a>

-   **区分text和keyword**

    在Elasticsearch中string字段被拆分成两种新的数据类型：text用于全文搜索的，而keyword用于关键词搜索。

    对于不需要分词的字符串精确值字段，如标签或枚举，建议配置为keyword类型。

    7.x之前版本

    ```
    PUT my_index1
    {
      "mappings": {
        "my_type": {
          "properties": {
            "tags": {
              "type":  "keyword"
            },
            "full_name": {
              "type":  "text"
            }
          }
        }
      }
    }
    ```

    7.x之后版本

    ```
    PUT my_index1 
    { 
      "mappings": { 
             "properties": { 
            "tags": { 
              "type":  "keyword" 
            }, 
            "full_name": { 
              "type":  "text" 
            } 
          } 
        } 
      }
    ```

-   **基于text字段的聚合统计**

    分词字段的聚合统计不是一种常见的需求。在Elasticsearch对于分词字段的聚合统计需要用到fielddata，默认是禁用的，开启fielddata会带来较大的内存负担。

    建议的做法是分词字符串进行多字段映射，映射为一个text字段用于全文检索，和一个keyword字段用于聚合统计。

    7.x之前版本

    ```
    PUT my_index2
    {
      "mappings": {
        "my_type": {
          "properties": {
            "full_name": {
              "type": "text",
              "fields": {
                "raw": { 
                  "type":  "keyword"
                }
              }
            }
          }
        }
      }
    }
    ```

    7.x之后版本

    ```
    PUT my_index2
    {
        "mappings": {
                "properties": {
                    "full_name": {
                        "type": "text",
                        "fields": {
                            "raw": {
                                "type": "keyword"
                            }
                        }
                    }
                }
            }
      }
    ```


## 使用索引模板<a name="section5914550314410"></a>

Elasticsearch支持通过索引模板控制一些新建索引的设置（settings）和映射（mappings），如限制分片数为1，并且禁用\_all域。索引模板可以用于控制何种设置（settings）应当被应用于新创建的索引：

-   索引模板可以通过template字段指定通配符。
-   多个索引模板可以通过order指定覆盖顺序。数值越大，优先级越高。

如下示例表示，logstash-\*匹配的索引采用my\_logs模板，且my\_logs模板的优先级数值为1。

7.x之前版本

```
PUT /_template/my_logs 
{
  "template": "logstash-*", 
  "order":    1, 
  "settings": {
    "number_of_shards": 1 
  },
  "mappings": {
    "_default_": { 
      "_all": {
        "enabled": false
      }
    }
  },
  "aliases": {
    "last_3_months": {} 
  }
}
```

7.x之后版本

```
PUT /_template/my_logsa
{
  "index_patterns": ["logstasaah-*"],
  "order": 1,
  "settings": {
    "number_of_shards": 1
  },
  "mappings": {
    "properties": {
      "_all": {
        "enabled": false
      }
    }
  },
  "aliases": {
    "last_3_months": {}
  }
}
```

## 数据备份和恢复<a name="section40063217144230"></a>

Elasticsearch副本提供了高可靠性，让您可以容忍零星的节点丢失而不会中断服务。

但是，副本并不提供对灾难性故障的保护。对这种情况，您需要的是对集群真正的备份，在某些东西确实出问题的时候有一个完整的拷贝。

备份集群，您可以使用创建快照的功能，将集群的数据保存到OBS桶中。其备份过程是智能的。第一个快照建议是数据的完整拷贝，后续的快照会保留的是已存快照和新数据之间的差异。随着您不时的对数据进行快照，备份也在增量的添加和删除。这意味着后续备份会相当快速，因为它们只传输很小的数据量。

## 用过滤提高查询效率<a name="section2867565144451"></a>

过滤器的执行速度非常快，不会计算相关度（直接跳过了整个评分阶段），而且很容易被缓存。

通常当查找一个精确值的时候，我们不希望对查询进行评分计算。只希望对文档进行包括或排除的计算，所以我们会使用constant\_score查询以非评分模式来执行term查询并以一作为统一评分。

```
GET /my_store/products/_search
{
    "query" : {
        "constant_score" : { 
            "filter" : {
                "term" : { 
                    "city" : "London"
                }
            }
        }
    }
}
```

## 采用scroll API返回大量数据<a name="section49009950144620"></a>

当返回大量数据时，先查后取的过程支持用from和size参数分页，但有限制。结果集在返回之前需要在每个分片上先进行排序，然后合并之后再排序输出。使用足够大的from值，排序过程可能会变得非常沉重，使用大量的CPU、内存和带宽。因此，强烈建议不要使用深分页。

为了避免深度翻页，推荐采用scroll查询返回大量数据。

scroll查询可以用来对Elasticsearch有效地执行大批量的文档查询，而又不用付出深度分页那种代价。scroll查询允许我们先做查询初始化，然后再批量地拉取结果。

## 查询（query）与过滤（filter）的区别<a name="section1034545719364"></a>

**性能差异：**一般情况下，一次过滤会比一次评分的查询性能更优异，并且表现更稳定。

当使用过滤情况时，查询被设置为一个“不评分“或“过滤“查询。即这个查询只是去判断是否匹配，结果是yes或no。

例如，以下情况是典型的过滤情况：

-   created时间是否在2013与2014这个区间？
-   status字段是否包含published这个单词？
-   lat\_lon字段表示的位置是否在指定点的10km范围内？

当使用查询情况时，查询会变成一个“评分“的查询。和不评分的查询类似，也要去判断这个文档是否匹配，同时还需要判断这个文档匹配的程度如何。此查询的典型用法是用于查找以下文档：

-   查找与full text search这个词语匹配的文档。
-   包含run这个词，也能匹配runs、running、jog或者sprint。
-   包含quick、brown和fox这几个词，词之间离的越近，文档相关性越高。
-   标有lucene、search或java标签，标签越多，相关性越高。

## 验证查询是否合法<a name="section519218536381"></a>

查询在和不同的分析器与不同的字段映射相结合时，会比较难理解，可以用**validate-query API**来验证查询是否合法。

示例：在Kibana的Console界面中，执行如下命令。validate请求会告诉您这个查询不合法。

7.x之前版本

```
GET /gb/tweet/_validate/query 
{   
 "query": {      
 "tweet" : {       
   "match" : "really powerful"     
  }    
} 
}
```

7.x之后版本

```
GET /gb/tweet/_validate/query  
{ 
"query": { 
   "productName" : { 
  "match" : "really powerful" 
  } 
  } 
 }
```

为了找出查询不合法的原因，可以把explain参数加到查询字符串中，执行如下命令。

7.x之前版本

```
GET /gb/tweet/_validate/query?explain 
{
"query": {
   "tweet" : {
  "match" : "really powerful"
  }
  }
 }
```

7.x之后版本

```
GET /gb/tweet/_validate/query?explain
{    
 "query": {       
 "productName" : {        
   "match" : "really powerful"      
  }     
}  
}
```

返回结果如下所示，可以从返回结果看出查询类型（match）与字段名称（tweet）搞混了。

```
{
  "valid": false,
  "error": "org.elasticsearch.common.ParsingException: no [query] registered for [tweet]"
}
```

因此，对于合法查询，使用explain参数将返回可读的描述，这对准确理解云搜索服务是如何解析query是非常有帮助的。

