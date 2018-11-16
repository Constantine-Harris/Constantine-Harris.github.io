---
title: python学习笔记
date: 2018/11/16 18:02:00
tags: 
- python入门
- 强制类型转换
categories: 
- python入门
---
python数据类型之间的转换
对python内置的数据类型进行转换时，可以使用内置函数，常用的类型转换函数如下
、、、
python常用类型转换函数
函数格式	使用示例	描述
int(x [,base])	int("8")	  可以转换的包括String类型和其他数字类型，但是会丢失精度      
float(x)	 float(1)或者float("1")	 可以转换String和其他数字类型，不足的位数用0补齐，例如1会变成1.0
 complex(real ,imag)	 complex("1")或者complex(1,2)	 第一个参数可以是String或者数字，第二个参数只能为数字类型，第二个参数没有时默认为0
 str(x)	 str(1)	 将数字转化为String
 repr(x)	 repr(Object)	 返回一个对象的String格式
 eval(str)	 eval("12+23")	 执行一个字符串表达式，返回计算的结果,如例子中返回35
 tuple(seq)	 tuple((1,2,3,4))	 参数可以是元组、列表或者字典，wie字典时，返回字典的key组成的集合
 list(s)	 list((1,2,3,4))	 将序列转变成一个列表，参数可为元组、字典、列表，为字典时，返回字典的key组成的集合
 set(s)	 set(['b', 'r', 'u', 'o', 'n'])或者set("asdfg")	 将一个可以迭代对象转变为可变集合，并且去重复，返回结果可以用来计算差集x - y、并集x | y、交集x & y
 frozenset(s)	 frozenset([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])	 将一个可迭代对象转变成不可变集合，参数为元组、字典、列表等，
 chr(x)	 chr(0x30)	 chr()用一个范围在 range（256）内的（就是0～255）整数作参数，返回一个对应的字符。返回值是当前整数对应的ascii字符。
 ord(x)	 ord('a')	 返回对应的 ASCII 数值，或者 Unicode 数值
 hex(x)	 hex(12)	 把一个整数转换为十六进制字符串
 oct(x)	 oct(12)	 把一个整数转换为八进制字符串
 、、、
