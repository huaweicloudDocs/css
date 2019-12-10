# 使用Kibana或API导入数据到Elasticsearch<a name="css_01_0024"></a>

云搜索服务支持使用Kibana或者API将数据导入到Elasticsearch中，数据文件支持JSON、CSV等格式。

## 使用Kibana导入数据<a name="section1430231820400"></a>

在导入数据之前，您可以使用Kibana接入集群。如下操作步骤介绍如何使用POST命令导入数据。

1.  登录Kibana Console页面，详细操作请参见[在管理控制台通过Kibana接入集群](接入集群.md#section9848115695612)。

    首次登录时，需要在Kibana的左侧导航中选择“Dev Tools“，单击“Get to work“，进入Console界面。非首次登录可单击“Dev Tools“直接进入Kibana Console页面。

2.  （可选）在Console界面，执行命令创建待存储数据的索引，并指定自定义映射来定义数据类型。

    如果待导入数据的集群已存在可用的索引，则不需要再创建索引；如果待导入数据的集群不存在可用的索引，则需要参考如下示例创建索引。

    例如：在Console界面，执行如下命令，创建索引“my\_store“，并指定自定义映射来定义数据类型。

    ```
    PUT /my_store
    {
      "settings": {
        "number_of_shards": 1
      },
      "mappings": {
        "products": {
          "properties": {
            "productName": {
              "type": "text"
              },
            "size": {
              "type": "keyword"
            }
          }
        }
      }
    }
    ```

3.  在Console界面的右侧文本框中输入要导入数据的POST命令，以导入一条数据为例，执行如下命令。

    ```
    POST /my_store/products/_bulk 
    {"index":{}} 
    {"productName":"Latest art shirts for women in 2017 autumn","size":"L"}
    ```

    返回结果如[图1](#fig93061932172813)所示，当返回结果信息中“errors“字段的值为“false“时，表示导入数据成功。

    **图 1**  返回消息<a name="fig93061932172813"></a>  
    ![](figures/返回消息.png "返回消息")


## 使用API导入数据<a name="section239718062912"></a>

使用bulk API通过cURL命令导入数据文件，如下操作以JSON数据文件为例。

>![](public_sys-resources/icon-note.gif) **说明：**   
>使用API导入数据文件时，导入的数据文件大小不能超过50MB。  

1.  登录即将接入集群的弹性云服务器。

    接入集群的详细操作指导请参见[在同一VPC内的弹性云服务器，直接调用Elasticsearch API](接入集群.md#section16223134914582)。

2.  执行如下命令，导入JSON数据。

    其中，**\{_Private network address and port number of the node_\}**需替换为集群中节点的内网访问地址和端口号，当该节点出现故障时，将导致命令执行失败。如果集群包含多个节点，可以将**\{_Private network address and port number of the node_\}**替换为集群中另一节点的内网访问地址和端口号；如果集群只包含一个节点，则需要将该节点修复之后再次执行命令进行导入数据。**test.json**为导入数据的json文件。

    ```
    curl -X PUT "http://{Private network address and port number of the node} /_bulk" -H 'Content-Type: application/json' --data-binary @test.json
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >其中，-X参数的参数值为命令，如“-X PUT“，-H参数的参数值为消息头，如“-H 'Content-Type: application/json' --data-binary @test.json“。添加的-k参数时，请勿将-k参数放置在参数与参数值之间。  

    **示例：**将“testdata.json“数据文件中的数据导入至Elasticsearch集群，此集群未进行通信加密，其中一个节点内网访问地址为“192.168.0.90“，端口号为“9200“。其中testdata.json文件中的数据如下所示：

    ```
    {"index": {"_index":"my_store","_type":"products"}}
    {"productName": "2019秋装新款文艺衬衫女装","size": "M"}
    {"index": {"_index":"my_store","_type":"products"}}
    {"productName": "2019秋装新款文艺衬衫女装","size": "L"}
    ```

    导入数据的操作步骤如下所示：

    1.  可执行以下命令，创建my\_store索引。

        ```
        curl -X PUT http://192.168.0.90:9200/my_store -H 'Content-Type: application/json' -d '
         { 
           "settings": { 
             "number_of_shards": 1 
           }, 
           "mappings": { 
             "products": { 
               "properties": { 
                 "productName": { 
                   "type": "text" 
                   }, 
                 "size": { 
                   "type": "keyword" 
                 } 
               } 
             } 
           } 
         }'
        ```

    2.  执行以下命令，导入testdata.json文件中的数据。

        ```
        curl -X PUT "http://192.168.0.90:9200/_bulk" -H 'Content-Type: application/json' --data-binary @testdata.json
        ```



