---
title: git使用
date: 2018/11/08 13:42:00
tags: 
- git
categories: 
- git
---
# git使用（怕遗忘）


先输入账号和邮箱：
```
git config --global user.name "用户名"
```
```
git config --global user.email "邮箱"
```
git 同步master
```
git clone xxxxxx.git
```
git 同步分支
```
git clone xxxxxx.git - b 分支名
```
上传的话
输入命令 cd 文件夹地址，进入文件夹
```
git init
```
上传所有文件的话：
 ```
git add .
```
上传提交信息
```
git commit  -m  "提交信息"
```
将本地的库链接到仓库
```
git remote add origin xxxxx.git
```
失败的话
```
git remote rm origin
```
push
```
git push
```

Step1、查看代码的修改状态

打开git shell(环境：以windows为例，安装好Github的客户端并配置好账户信息)， 默认是在git的工作空间路径，ls命令可以查看workspace下的所有目录（建议：workspace下的目录应以项目为单位）, cd命令进入目标工程。

```
git status
```

红色或绿色部分字体是工程内的发生修改的状态标识:

modified 代表文件和上一版本相比，有过修改

new  file  代表文件是新增加的

deleted   代表文件被删除了，提交成功后，文件将从repository中删除

untracked file 一般都是新增加的文件夹

Step2、查看代码的修改内容

```
git diff <filename> 
```

这里查看的是.gitignore文件的修改变化。
查看历史修改，需要用到节点hashcode（hashcode可以从github上commit记录上获得）:

```
git diff <hascode> <hashcode> <filename>
```

Step3、暂存需要提交的代码

增加一个需要上传的文件：


```
git add <filename>
```
删除一个不需要的文件：
```
git rm <filename>
```
增加全部需要上传的文件：
```
git add --all
```
Step4、提交已暂存的文件

我们现在推荐不加-m的方式

```
git commit
```
执行后会弹出编辑框，一行标题，另起一行，写上详细注释。这就符合git的上传规范了。

不推荐大家直接-m提交注释，因为只能写个标题。

```
git commit -m <comment>
```
如果发现有文件漏提或注释有误，使用amend修正：
```
git commit --amend
```
注意：使用commit命令只是将修改提交到本地仓库
Step5、同步到服务器

使用push命令形象的将修改push到github的代码服务器，so you can access the code anywhere.

```
git push -u origin master
```
同步到服务器前先需要将服务器代码同步到本地
命令：
```
git pull
```

如果执行失败，就按照提示还原有冲突的文件，然后再次尝试同步。
命令：
```git checkout -- <有冲突的文件路径>
```

同步到服务器
命令：
```git push origin  <本地分支名>
```

如果执行失败，一般是没有将服务器代码同步到本地导致的，先执行上面的git pull命令。

