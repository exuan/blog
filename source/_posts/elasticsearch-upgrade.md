title: elasticsearch 升级
date: 2015-10-22 10:31:21
categories: elasticsearch
tags: [elasticsearch]
---
对于 1.5 以后的es升级是很容易的事情，备份快照然后升级。
```bash
# 创建
curl -XPUT 127.0.0.1:9200/_snapshot/backup -d '
{
"type":"fs",
"settings":{"location":"/data/backup/es"}
}'

# 备份
curl -XPUT 127.0.0.1:9200/_snapshot/backup/es-snapshot?wait_for_completion=true

# 恢复
curl -XPOST 127.0.0.1:9200/_snapshot/backup/es-snapshot/_restore
```
<!--more--> 