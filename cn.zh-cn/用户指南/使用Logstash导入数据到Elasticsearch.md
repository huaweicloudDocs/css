# 使用Logstash导入数据到Elasticsearch<a name="css_01_0048"></a>

云搜索服务支持使用Logstash将其收集的数据迁移到Elasticsearch中，方便用户通过Elasticsearch搜索引擎高效管理和获取数据。数据文件支持JSON、CSV等格式。

Logstash 是开源的服务器端数据处理管道，能够同时从多个来源采集数据、转换数据，然后将数据发送到Elasticsearch中。Logstash的官方文档请参见：[https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html)。

数据导入分为如下2种场景：

-   [Logstash部署在外网时导入数据](#section072813417814)
-   [Logstash部署在弹性云服务器上时导入数据](#section1098217174335)

## 前提条件<a name="section371994174412"></a>

-   为方便操作，建议采用Linux操作系统的机器部署Logstash。
-   Logstash的下载路径为：[https://www.elastic.co/downloads/logstash](https://www.elastic.co/downloads/logstash)
-   安装完Logstash后，再根据如下步骤导入数据。安装Logstash的操作指导，请参见：[https://www.elastic.co/guide/en/logstash/current/installing-logstash.html](https://www.elastic.co/guide/en/logstash/current/installing-logstash.html)
-   安装Logstash之前，需要先安装JDK。在Linux操作系统中，您可以执行**yum -y install java-1.8.0**命令直接安装1.8.0版本JDK。在Windows操作系统中，您可以访问[JDK官网](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)，下载符合操作系统版本的JDK，并根据指导安装。
-   在“[Logstash部署在弹性云服务器上时导入数据](#section1098217174335)”场景中，请确保此弹性云服务器与接入的Elasticsearch集群在同一个VPC下。

## Logstash部署在外网时导入数据<a name="section072813417814"></a>

当Logstash部署在外网时，导入数据的流程说明如[图1](#fig471717481106)所示。

**图 1**  Logstash部署在外网时导入数据示意图<a name="fig471717481106"></a>  
![](figures/Logstash部署在外网时导入数据示意图.png "Logstash部署在外网时导入数据示意图")

1.  <a name="li1648853125014"></a>创建一个跳转主机，并按如下要求进行配置。
    -   跳转主机为一台Linux操作系统的弹性云服务器，且已绑定弹性IP。
    -   跳转主机与CSS集群在同一虚拟私有云下。
    -   已开放跳转主机的本地端口，用于SSH转发，能够从本地端口转发至CSS集群某一节点的9200端口。
    -   关于跳转主机的本地端口转发配置，请参见[SSH官方文档](https://man.openbsd.org/ssh.1#L)。

2.  使用PuTTY，通过弹性IP登录已创建的跳转主机。
3.  执行如下命令进行端口映射，将发往跳转主机对外开放端口的请求转发到待导入数据的集群中。

    ```
    ssh -g -L <跳转主机的本地端口:节点的内网访问地址和端口号> -N -f root@<跳转主机的私网IP地址>
    ```

    >![](public_sys-resources/icon-note.gif) **说明：**   
    >-   _<_跳转主机的本地端口_\>_：为步骤[1](#li1648853125014)中的端口。  
    >-   _<节点的内网访问地址和端口号\>_：为集群中某一节点的内网访问地址和端口号。当该节点出现故障时，将导致命令执行失败。如果集群包含多个节点，可以将_<__节点的内网访问地址和端口号\>_替换为集群中另一节点的内网访问地址和端口号；如果集群只包含一个节点，则需要将该节点修复之后再次执行命令进行端口映射。  
    >-   <__跳转主机_的私网IP地址_\>：打开弹性云服务器管理控制台，从“IP地址“列中获取标有“私网“对应的IP地址。  

    例如：跳转主机对外开放的端口号为9200，节点的内网访问地址和端口号为192.168.0.81:9200，跳转主机的私网IP地址为192.168.0.227，需要执行如下命令进行端口映射。

    ```
    ssh -g -L 9200:192.168.0.81:9200 -N -f root@192.168.0.227
    ```

4.  <a name="li5164153542312"></a>登录部署了Logstash的服务器，将需要进行操作的数据文件存储至此服务器中。

    例如，需要导入的数据文件“access\_20181029\_log“，文件存储路径为“/tmp/access\_log/“，此数据文件中包含的数据如下所示：

    ```
    |   All |               Heap used for segments |                        |     18.6403 |      MB |
    |   All |             Heap used for doc values |                        |    0.119289 |      MB |
    |   All |                  Heap used for terms |                        |     17.4095 |      MB |
    |   All |                  Heap used for norms |                        |   0.0767822 |      MB |
    |   All |                 Heap used for points |                        |    0.225246 |      MB |
    |   All |          Heap used for stored fields |                        |    0.809448 |      MB |
    |   All |                        Segment count |                        |         101 |         |
    |   All |                       Min Throughput |           index-append |     66232.6 |  docs/s |
    |   All |                    Median Throughput |           index-append |     66735.3 |  docs/s |
    |   All |                       Max Throughput |           index-append |     67745.6 |  docs/s |
    |   All |              50th percentile latency |           index-append |     510.261 |      ms |
    ```

5.  在部署Logstash的服务器中，执行如下命令在Logstash的安装目录下新建配置文件logstash-simple.conf。

    ```
    cd /<Logstash的安装目录>/
    vi logstash-simple.conf
    ```

6.  在配置文件logstash-simple.conf中输入如下内容。

    ```
    input {
    数据所在的位置
    }
    filter {
    数据的相关处理
    }
    output {
        elasticsearch {
            hosts => "<跳转主机的公网IP地址>:<跳转主机对外开放的端口号>"
        }
    }
    ```

    -   input：指明了数据的来源。实际请根据用户的具体情况来设置。input参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/input-plugins.html](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)。
    -   filter：指定对数据进行处理的方式。例如，对日志进行了提取和处理，将非结构化信息转换为结构化信息。filter参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)。
    -   output：指明了数据的目的地址。output参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/output-plugins.html](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)。<__跳转主机_的公网IP地址_\>请从弹性云服务器管理控制台的“IP地址“列中获取标有“弹性公网“对应的IP地址。_<跳转主机对外开放的端口号\>_即为步骤[1](#li1648853125014)中的端口，例如：9200。

    以步骤[4](#li5164153542312)中“/tmp/access\_log/“的数据文件为例，输入数据文件从首行开始，且过滤条件保持为空，即不做任何数据处理操作。跳转主机的公网IP和端口号为“192.168.0.227:9200“。导入数据的索引名称为“myindex“。配置文件的示例如下所示，配置文件按实际数据情况修改完成后，输入“:wq“保存。

    ```
    input { 
        file{
          path => "/tmp/access_log/*"
          start_position => "beginning"
        }
    } 
    filter { 
    } 
    output { 
        elasticsearch { 
          hosts => "192.168.0.227:9200"
          index => myindex
          document_type => mytype
        } 
    }
    ```

7.  执行如下命令将Logstash收集的数据导入到集群中。

    ```
    ./bin/logstash -f logstash-simple.conf
    ```

8.  登录云搜索服务管理控制台。
9.  在左侧导航栏中，选择“集群管理“，进入集群列表页面。
10. 在集群列表页面中，单击待导入数据的集群“操作“列的“Kibana“。
11. 在Kibana的左侧导航中选择“Dev Tools“，单击“Get to work“，进入Console界面。
12. 在已打开的Kibana的Console界面，通过搜索获取已导入的数据。

    在Kibana控制台，输入如下命令，搜索数据。查看搜索结果，如果数据与导入数据一致，表示数据文件的数据已导入成功。

    ```
    GET myindex/_search
    ```


## Logstash部署在弹性云服务器上时导入数据<a name="section1098217174335"></a>

当Logstash部署在同一VPC的弹性云服务时，导入数据的流程说明如[图2](#fig124034434127)所示。

**图 2**  Logstash部署在弹性云服务器上时导入数据示意图<a name="fig124034434127"></a>  
![](figures/Logstash部署在弹性云服务器上时导入数据示意图.png "Logstash部署在弹性云服务器上时导入数据示意图")

1.  确保已部署Logstash的弹性云服务器与待导入数据的集群在同一虚拟私有云下，已开放安全组的9200端口的外网访问权限，且弹性云服务器已绑定弹性IP。
2.  <a name="li1652411439236"></a>使用PuTTY登录弹性云服务器。

    例如此服务器中存储了需要导入的数据文件“access\_20181029\_log“，文件存储路径为“/tmp/access\_log/“，此数据文件中包含的数据如下所示：

    ```
    |   All |               Heap used for segments |                        |     18.6403 |      MB |
    |   All |             Heap used for doc values |                        |    0.119289 |      MB |
    |   All |                  Heap used for terms |                        |     17.4095 |      MB |
    |   All |                  Heap used for norms |                        |   0.0767822 |      MB |
    |   All |                 Heap used for points |                        |    0.225246 |      MB |
    |   All |          Heap used for stored fields |                        |    0.809448 |      MB |
    |   All |                        Segment count |                        |         101 |         |
    |   All |                       Min Throughput |           index-append |     66232.6 |  docs/s |
    |   All |                    Median Throughput |           index-append |     66735.3 |  docs/s |
    |   All |                       Max Throughput |           index-append |     67745.6 |  docs/s |
    |   All |              50th percentile latency |           index-append |     510.261 |      ms |
    ```

3.  执行如下命令在Logstash的安装目录下新建配置文件logstash-simple.conf。

    ```
    cd /<Logstash的安装目录>/
    vi logstash-simple.conf
    ```

    在配置文件logstash-simple.conf中输入如下内容。

    ```
    input {
    数据所在的位置
    }
    filter {
    数据的相关处理
    }
    output {
        elasticsearch{
            hosts => "<节点的内网访问地址和端口号>"} 
    }
    ```

    -   input：指明了数据的来源。实际请根据用户的具体情况来设置。input参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/input-plugins.html](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)。
    -   filter：对日志进行了提取和处理，将非结构化信息转换为结构化信息。filter参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/filter-plugins.html](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)。
    -   output：指明了数据的目的地址。output参数的详细解释和使用介绍请参见[https://www.elastic.co/guide/en/logstash/current/output-plugins.html](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)。_<节点的内网访问地址和端口号\>_为集群中节点的内网访问地址和端口号。

        当集群包含多个节点时，为了避免节点故障，建议将上述命令中_<节点的内网访问地址和端口号\>_替换为该集群中多个节点的内网访问地址和端口号，多个节点的内网访问地址和端口号之间用英文逗号隔开，填写格式请参见如下示例。

        ```
        hosts => ["192.168.0.81:9200","192.168.0.24:9200"]
        ```

        当集群只包含一个节点时，填写格式请参见如下示例。

        ```
        hosts => "192.168.0.81:9200"
        ```

    以步骤[2](#li1652411439236)中“/tmp/access\_log/“的数据文件为例，输入数据文件从首行开始，且过滤条件保持为空，即不做任何数据处理操作。需导入数据的集群，其节点内网访问地址和端口号为“192.168.0.81:9200“。导入数据的索引名称为“myindex“。配置文件的示例如下所示，配置文件按实际数据情况修改完成后，输入“:wq“保存。

    ```
    input { 
        file{
          path => "/tmp/access_log/*"
          start_position => "beginning"
        }
    } 
    filter { 
    } 
    output { 
        elasticsearch { 
          hosts => "192.168.0.81:9200"
          index => myindex
          document_type => mytype
        } 
    }
    ```

4.  执行如下命令将Logstash收集的弹性云服务器的数据导入到集群中。

    ```
    ./bin/logstash -f logstash-simple.conf
    ```

5.  登录云搜索服务管理控制台。
6.  在左侧导航栏中，选择“集群管理“，进入集群列表页面。
7.  在集群列表页面中，单击待导入数据的集群“操作“列的“Kibana“。
8.  在Kibana的左侧导航中选择“Dev Tools“，单击“Get to work“，进入Console界面。
9.  在已打开的Kibana的Console界面，通过搜索获取已导入的数据。

    在Kibana控制台，输入如下命令，搜索数据。查看搜索结果，如果数据与导入数据一致，表示数据文件的数据已导入成功。

    ```
    GET myindex/_search
    ```


