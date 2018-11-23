---
title: python爬虫实战
date: 2018/11/23 18:24:00
tags: 
- 爬虫
- python
categories: 
- python
- 爬虫
---
如何爬取别人的博客：
[LXML解析HTML](http://www.cnblogs.com/ospider/p/5911339.html "LXML解析HTML")
[python文件读写](http://www.runoob.com/python3/python3-file-methods.html "python文件读写")
```python
import requests
import time
import re
from lxml import html
#文件读写新建一个文件1.txt，必须使用一个编码格式
aa = open("C:\\Users\\john\\1.txt", mode='x', encoding="utf-8")
#遍历a-z网站页面
for i in range(ord("a"),ord("z")+1):
    a = "http://flvoters.com/index_pages/"+(chr(i))+".html"
    b = requests.get(a)
	#正则匹配正确的链接格式
    c = re.finditer('''[a-zA-z]+://flvoters.com/index_pages/'''+chr(i)+'''[1-9][0-9]{1,}[^"'\s]*''', b.text)
    time.sleep(5)
	#正则匹配正确的链接格式
    print(1)
    for match in c:
        d = requests.get(match.group())
        e = re.finditer('''[a-zA-z]+://flvoters.com/pages/'''+chr(i)+'''[1-9][0-9]{4,}[^"'\s]*''',d.text)
        time.sleep(5)
		#替换https为http
        for match1 in e:
            f = match1.group()
            f = f.replace("https://", "http://")
            print(f)
            g =requests.get(f)
            time.sleep(10)
			#查找正确的内容
            i = re.finditer('''<br><br><big>[^\n]*''',g.text)
            g.close()
			#lxml解析
            for j in i:
                doc = html.fromstring(j.group())
                aa.write(doc.text_content()+"\n")

```
