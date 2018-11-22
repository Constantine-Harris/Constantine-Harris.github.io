---
title: python爬虫入门
date: 2018/11/22 18:24:00
tags: 
- 爬虫
- python
categories: 
- python
- 爬虫
---


如何爬取自己的博客
首先学会了[requests快速上手](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html# "requests快速上手")
了解博客存在一个xml文件--[genleak.com/atom.xml](http://genleak.com/atom.xml "genleak.com/atom.xml")
然后学习了XML解析[Python xml解析](http://www.runoob.com/python3/python3-xml-processing.html "Python xml解析")
```python
import requests
from xml.dom.minidom import parse
import xml.dom.minidom
import json

# 使用requests请求获得 XML 文档
a = requests.get("http://genleak.com/atom.xml")
# 使用minidom解析器打开 XML 文档
DOMTree = xml.dom.minidom.parseString(str(a.text))
collection = DOMTree.documentElement
# 在集合中获取所有文章，文章开头标签是entry
entrys = collection.getElementsByTagName("entry")
# 或者每片文章的详细信息，同时还要检验是否有空文章
for entry in entrys:
   # print("*****page*****")
   title,summary,published,content ="","","",""
   if entry.getElementsByTagName("title")[0].childNodes:
      # print("Title: %s" % entry.getElementsByTagName('title')[0].childNodes[0].data)
      title= entry.getElementsByTagName('title')[0].childNodes[0].data
   if entry.getElementsByTagName("summary")[0].childNodes:
       summary1 = entry.getElementsByTagName('summary')[0]
       # print("summary: %s" % summary1.childNodes[0].data)
       summary = entry.getElementsByTagName('summary')[0].childNodes[0].data
   if entry.getElementsByTagName("published")[0].childNodes:
       published1 = entry.getElementsByTagName('published')[0]
       # print("published: %s" % published1.childNodes[0].data)
       published = entry.getElementsByTagName('published')[0].childNodes[0].data
   if entry.getElementsByTagName("content"):
       content1 = entry.getElementsByTagName('content')[0]
       # print("content: %s" % content1.childNodes[0].data)
       content = entry.getElementsByTagName('content')[0].childNodes[0].data
```
如果用数组存储：
```python
   arr = {"Title",str(title),"Summary",str(summary),"published",str(published),"content",str(content)}
   json_str = json.dumps(arr)
   print(json_str)
```
```python
["Title", "", "Summary", "\n    \n    ", "published", "2018-11-22T10:25:07.643Z", "content", ""]
```
出现并不是json格式，经过查阅使用字典
[Python3 JSON](http://www.runoob.com/python3/python3-json.html "Python3 JSON")
json.dumps(): 对数据进行编码。
json.loads(): 对数据进行解码。
如果你要处理的是文件而不是字符串，你可以使用 json.dump() 和 json.load() 来编码和解码JSON数据。
```python
arr = {"Title":str(title),"Summary":str(summary),"published":str(published),"content":str(content)}
json_str = json.dumps(arr)
print(json_str)
```
```python
{"Title": "", "Summary": "\n    \n    ", "published": "2018-11-22T10:25:07.643Z", "content": ""}
```
```python
#application/json是json的content类型，
   headers = {'Content-Type': 'application/json'}
   #通过requests传入json到ES，名叫blog的索引和名叫pages的类型，同时新版只能使用post
   r = requests.post('http://172.16.1.215:9200/blog/pages', data=json_str,headers=headers)
```
