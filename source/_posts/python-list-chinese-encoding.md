title: python 中 处理 list dict 中文(utf-8)编码    
date: 2014-06-24 18:30:16
categories: python
tags: [python]
---
python在打印集合的时候发现中文内容被转码了

```python
#!/usr/bin/env python
# -*- coding:utf-8 -*-
import json

data = json.loads('{"errno": 102, "message": "参数操作"}')
print json.dumps(data)
```

```json
{"errno": 102, "message": "\u53c2\u6570\u64cd\u4f5c"}
```
<!--more--> 

json.dumps ensure_ascii 默认是true, so 只需要把它改成false

```python
print json.dumps(data, ensure_ascii=False)
```

```json
{"errno": 102, "message": "参数操作"}
```