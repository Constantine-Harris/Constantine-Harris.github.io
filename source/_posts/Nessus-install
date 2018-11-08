---
title: python地址
date: 2018/11/07 20:20:00
tags: 
- python入门手册
- 廖雪峰python
Categories: 
- python入门手册
---

## 实验环境
kali linux

## 安装过程
### 下载 Nessus
在官方网站下载对应的 Nessus 版本：http://www.tenable.com/products/nessus/select-your-operating-system

这里选择自己系统的版本安装包就行

## 安装 Nessus
下载得到的是 deb 文件，与普通 deb 文件安装方法类似，执行

```
dpkg -i Nessus-6.10.5-debian6_amd64.deb
```
接下来进行启动和登陆 web 界面。 
根据提示执行以下命令启动 nessus

```
/etc/init.d/nessusd start
```

启动后可以查看nessus 启动状态

```
netstat -ntpl | grep nessus

```

同样即为成功

获取激活码
打开网站：http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code



点击“Nessus Home”版本下面的“Register Now”



然后填写姓名和邮箱，姓名随意，邮箱最好翻墙用谷歌邮箱

因为登陆 web 界面需要输入 nessus 激活码，为了不打断中间的安装过程，我们提前获取激活码以便使用。



登陆 web 界面
按照之前提示信息打开网页：https://guet:8834/
或者直接访问本地，浏览器中启动软件。Nessus采用的B/S架构，在浏览器中输入https://127.0.0.1:端口号 即可打开Nessus主页，启动之后需要设置管理帐号和密码，设置完之后需要输入Active code（激活码）才可以进行插件的更新安装，Active code获取方法如下：访问 http://www.tenable.com/products/nessus/nessus-homefeed 进行注册，填写正确邮箱，注册完成会收到邮件，邮件中就有Active code。输入Active code之后就可以开始下载安装插件了

打开网站：http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code



创建登录用户按个人喜好填写



然后填写邮箱收到的激活码





之后会开始下载。。。。不过。。。你以为到这里就完了么。。。一般到这里就gg了，最大的难点也就是这里了，不过参照网文也倒总结出来了

Nessus 下载插件出错的解决方法


翻了墙就不用这么麻烦了，直接一条命令就OK了
```
/opt/nessus/sbin/nessuscli update
```
没那个条件的还是乖乖配置吧～～

个人也比较推荐这个



这个方法使用离线方式下载插件，然后安装。 
离线方式需要挑战码和激活码，而且刚才那个激活码因为已经使用过了，所以失效了，可以重新填写信息发送一个新的激活码，好像一小时内只能发送一次激活码，如果告知已经达到限制了，可以换个邮箱也是可以获取激活码的。

现在生成挑战码，在目录/opt/nessus/sbin下执行
```
./nessuscli fetch --challenge
```

如上图所示，会得到一个挑战码，保存这个挑战码。打开网页：https://plugins.nessus.org/v2/offline.php



将挑战码和激活码分别输入相应的位置，然后点击“Submit”



会跳转到上图的下载页面，点击红框中的两个链接分别下载插件和注册码。 
这个插件有一百多兆，而且下载可能会比较慢，注册码比较小，下载很快。

下载好后将两个文件都复制到目录/opt/nessus/sbin/下，然后注册
```
./nessuscli fetch --register-offline nessus.license
```

接着安装插件
```
./nessuscli update all-2.0.tar.gz 
```



最后重新启动下
```
./nessusd
```

操作完成了就说明搞定了，再去刷新登录页面填写自己创建的用户名及密码就行了
