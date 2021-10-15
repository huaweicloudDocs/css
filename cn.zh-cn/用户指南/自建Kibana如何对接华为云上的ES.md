# 自建Kibana如何对接华为云上的ES？<a name="css_02_0097"></a>

自建Kibana对接华为云的ES，需满足如下条件：

1.  本地环境需要支持外网访问。
2.  通过同vpc下ecs服务搭建kibana，本地公网访问kibana即可。

kibana配置文件参考：

安全模式：

```
elasticsearch.username: "***"
elasticsearch.password: "***"
elasticsearch.ssl.verificationMode: none
server.ssl.enabled: false
server.rewriteBasePath: false
server.port: 5601
logging.dest: /home/Ruby/log/kibana.log
pid.file: /home/Ruby/run/kibana.pid
server.host: 192.168.25.226
elasticsearch.hosts: https://10.0.0.207:9200
elasticsearch.requestHeadersWhitelist: ["securitytenant","Authorization"]
opendistro_security.multitenancy.enabled: true
opendistro_security.multitenancy.tenants.enable_global: true
opendistro_security.multitenancy.tenants.enable_private: true
opendistro_security.multitenancy.tenants.preferred: ["Private", "Global"]
opendistro_security.multitenancy.enable_filter: false
```

>![](public_sys-resources/icon-note.gif) **说明：** 
>-   安全模式需要安装插件opendistro\_security\_kibana，详细请参考_https://opendistro.github.io/for-elasticsearch-docs/docs/kibana/plugins/_。
>-   安装的插件版本需要和集群版本保持一致，可通过**GET \_cat/plugins**获取到集群安全插件的版本号。

非安全模式：

```
server.port: 5601
logging.dest: /home/Ruby/log/kibana.log
pid.file: /home/Ruby/run/kibana.pid
server.host: 192.168.25.226
elasticsearch.hosts: https://10.0.0.207:9200
```

