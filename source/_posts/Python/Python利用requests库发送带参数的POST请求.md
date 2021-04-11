---
title: Python利用requests库发送带参数的POST请求
date: 2021-04-09 12:11:39
categories: Python
tags: [Python]
---
近日用了requests库写了下脚本，记录一下以备后用。

```python
import requests
import time
import json
import datetime
#设置请求URL
url = 'https://10.200.4.180/api/web/incident/search'
#设置cookie变量
cookie = 'blablabla'
#设置请求头，主要确认其中的Host，Origin和Referer
headers = {'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
           'Accept-Language': 'zh-CN,zh;q=0.9',
           'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36',
           'Connection': 'keep-alive',
           'Accept-Encoding': 'gzip, deflate, br',
           #cookie中如果有中文会报'latin-1'错误，可以先转义
           'Cookie': cookie.encode("utf-8").decode("latin1"),
           'Origin': 'https://10.200.4.180',
           'Referer': 'https://10.200.4.180/hosts',
           'Content-Type': 'application/json; charset=UTF-8',
           'Cache-Control': 'no-cache',
           'sec-ch-ua-mobile': '?0',
           'sec-fetch-dest': 'empty',
           'sec-fetch-mode': 'cors',
           'sec-fetch-site': 'same-origin'
           }

data = 'datacontent'
#如果需要转换为json发送，使用json.loads()
#data=json.loads(data)
#如果访问不受信任的网站，需要添加verify=false，否则会报错
response = requests.post(url, data=data, headers=headers, verify=False)
#返回结果在response.text，可以用json.loads转为json
res = json.loads(response.text)

```