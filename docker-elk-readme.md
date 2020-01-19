# 说明
elk 日志收集 postgresql csv centos
## 步骤

1. 先安装 elk
1. 在安装 filebeat rpm
1. 最后配置 filebeat 与 elk pipeline plugin

## 改动

- 添加 csv 插件
- 配置 filebeat 收集 pg 数据库日志
  - 添加 pipeline for pg csv log
  - 额外配置 filebeat.yml 多行日志处理 
  
  ```yml
  - type: log
    multiline.pattern: '^([0-9]{3}[1-9]|[0-9]{2}[1-9][0-9]{1}|[0-9]{1}[1-9][0-9]{2}|[1-9][0-9]{3})-(((0[13578]|1[02])-(0[1-9]|[12][0-9]|3[01]))|((0[469]|11)-(0[1-9]|[12][0-9]|30))|(02-(0[1-9]|[1][0-9]|2[0-8])))'
    multiline.negate: true
    multiline.match: after
  ```

## 参考

- [filebeat pipeline](https://gryzli.info/2019/04/21/working-with-ingest-pipelines-in-elasticsearch-and-filebeat/)
- [filebeat pipeline pg](https://note.yuchaoshui.com/blog/post/yuziyue/filebeat-use-ingest-node-dealwith-log-then-load-into-elasticsearch)

```sh
docker exec -it docker-elk_elasticsearch_1 /bin/sh
./bin/elasticsearch-plugin install https://github.com/johtani/elasticsearch-ingest-csv/releases/download/7.5.0/ingest-csv-7.5.0.0.zip

```

----------

## [Elastic stack (ELK) on Docker](https://github.com/deviantony/docker-elk.git)

