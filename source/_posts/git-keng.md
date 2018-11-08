---
title: git使用的一些坑
date: 2018/11/08 13:42:00
tags: 
- git
categories: 
- git
---
一.各种命令介绍：　
git pull：从其他的版本库(既可以是远程的也可以是本地的)将代码更新到本地，例如：'git pull origin master'就是将origin这个版本库的代码更新到本地的master主枝，该功能类似于SVN的update

git add：是将当前更改或者新增的文件加入到Git的索引中，加入到Git的索引中就表示记入了版本历史中，这也是提交之前所需要执行的一步，例如'git add app/model/user.rb'就会增加app/model/user.rb文件到Git的索引中

git rm：从当前的工作空间中和索引中删除文件，例如'git rm app/model/user.rb'

git commit：提交当前工作空间的修改内容，类似于SVN的commit命令，例如'git commit -m "story #3, add user model"'，提交的时候必须用-m来输入一条提交信息

git push：将本地commit的代码更新到远程版本库中，例如'git push origin'就会将本地的代码更新到名为orgin的远程版本库中

git log：查看历史日志

git revert：还原一个版本的修改，必须提供一个具体的Git版本号，例如'git revert bbaf6fb5060b4875b18ff9ff637ce118256d6f20'，Git的版本号都是生成的一个哈希值、

二.使用步骤及流程
创建新仓库
git init
检出仓库
件来人肉合并这些 冲突（conflicts） 了。改完之后，你需要执行如下命令以将它们标记为合并成功：
git add <filename>
在合并改动之前，也可以使用如下命令查看：
git diff <source_branch> <target_branch>
串创建一个本地仓库的克隆版本
git clone /path/to/repositoty
如果是远程服务器上的仓库
git clone username@host:/path/to/repository
件。已添加到缓存区的改动，以及新件，都不受影响。


假如你想要丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：
git fetch origin
git reset --hard origin/master
你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 工作目录，它持有实际件；第二个是 缓存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，指向你最近一次提交后的结果。
添加与提交
你可以计划改动（把它们添加到缓存区），使用如下命令：
git add <filename>
git add *
这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：
git commit -m "代码提交信息"
现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。推送改动
你的改动现在已经在本地仓库的 HEAD 中了。执行如下命令以将这些改动提交到远端仓库：
git push origin master
可以把 master 换成你想要推送的任何分支。 


如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：
git remote add origin <server>
如此你就能够将你的改动推送到所添加的服务器上去
分支
分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master 是“默认的”。在其他分支上进行开发，完成后再将它们合并到主分支上
创建一个叫做“feature_x”的分支，并切换过去：
git checkout -b feature_x
切换回主分支：
git checkout master
再把新建的分支删掉：
git branch -d feature_x
除非你将分支推送到远端仓库，不然该分支就是 不为他人所见的：
git push origin <branch>
更新与合并
要更新你的本地仓库至最新改动，执行：
git pull
以在你的工作目录中 获取（fetch） 并 合并（merge） 远端的改动。
要合并其他分支到你的当前分支（例如 master），执行：
git merge <branch>
两种情况下，git 都会尝试去自动合并改动。不幸的是，自动合并并非次次都能成功，并可能导致 冲突（conflicts）。 这时候就需要你修改这些文件来人肉合并这些 冲突（conflicts） 了。改完之后，你需要执行如下命令以将它们标记为合并成功：
git add <filename>
在合并改动之前，也可以使用如下命令查看：
git diff <source_branch> <target_branch>
替换本地改动
假如你做错事（自然，这是不可能的），你可以使用如下命令替换掉本地改动：
git checkout -- <filename>
此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到缓存区的改动，以及新文件，都不受影响。


假如你想要丢弃你所有的本地改动与提交，可以到服务器上获取最新的版本并将你本地主分支指向到它：
git fetch origin
git reset --hard origin/master

三.错误汇总
1.windows使用git时出现：warning: LF will be replaced by CRLF
windows中的换行符为 CRLF， 而在linux下的换行符为LF，所以在执行add . 时出现提示，解决办法：

$ rm -rf .git  // 删除.git  
$ git config --global core.autocrlf false  //禁用自动转换   
然后重新执行：

$ git init    
$ git add .  
2.git push origin master出错：error: failed to push some refs to
很明显是：

本地没有update到最新版本的项目（git上有README.md文件没下载下来）

本地直接push所以会出错。

【解决过程】

1.看到提示里面，感觉是本地的代码不是最新的。

所以觉得应该是类似于svn中的，先update一下，再去commit，估计就可以了。

所以先去pull试试：

git pull  --rebase origin master

解决！

 

3.Git: cannot checkout branch - error: pathspec '…' did not match any file(s) known to git
解决方案：传送门

4.fatal: remote origin already exists.
解决办法如下：

    1、先输入$ git remote rm origin

    2、再输入$ git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了！

    3、如果输入$ git remote rm origin 还是报错的话，error: Could not remove config section 'remote.origin'. 我们需要修改gitconfig文件的内容

    4、找到你的github的安装路径，我的是C:\Users\ASUS\AppData\Local\GitHub\PortableGit_ca477551eeb4aea0e4ae9fcd3358bd96720bb5c8\etc

    5、找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！

 

 

    如果输入$ ssh -T git@github.com
    出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。

    解决办法如下：

    1、先输入$ ssh-agent，再输入$ ssh-add ~/.ssh/id_key，这样就可以了。

    2、如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。

    3、最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。

 

 

    如果输入$ git push origin master

    提示出错信息：error:failed to push som refs to .......

    解决办法如下：

    1、先输入$ git pull origin master //先把远程服务器github上面的文件拉下来

    2、再输入$ git push origin master

    3、如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git repository以及fatal: Could not read from remote repository.

    4、则需要重新输入$ git remote add origingit@github.com:djqiang/gitdemo.git

 

 

    使用git在本地创建一个项目的过程

    $ makdir ~/hello-world    //创建一个项目hello-world
    $ cd ~/hello-world       //打开这个项目
    $ git init             //初始化 
    $ touch README
    $ git add README        //更新README文件
    $ git commit -m 'first commit'     //提交更新，并注释信息“first commit”
    $ git remote add origin git@github.com:defnngj/hello-world.git     //连接远程github项目  
    $ git push -u origin master     //将本地项目更新到github项目上去

 

   

    gitconfig配置文件

         Git有一个工具被称为git config，它允许你获得和设置配置变量；这些变量可以控制Git的外观和操作的各个方面。这些变量可以被存储在三个不同的位置： 
         1./etc/gitconfig 文件：包含了适用于系统所有用户和所有库的值。如果你传递参数选项’--system’ 给 git config，它将明确的读和写这个文件。 
         2.~/.gitconfig 文件 ：具体到你的用户。你可以通过传递--global 选项使Git 读或写这个特定的文件。
         3.位于git目录的config文件 (也就是 .git/config) ：无论你当前在用的库是什么，特定指向该单一的库。每个级别重写前一个级别的值。因此，在.git/config中的值覆盖了在/etc/gitconfig中的同一个值。
        在Windows系统中，Git在$HOME目录中查找.gitconfig文件（对大多数人来说，位于C:\Documents and Settings\$USER下）。它也会查找/etc/gitconfig，尽管它是相对于Msys 根目录的。这可能是你在Windows中运行安装程序时决定安装Git的任何地方。

 

        配置相关信息：

        2.1　当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：

　　$ git config --global user.name "John Doe"

　　$ git config --global user.email johndoe@example.com

 

       2.2    你的编辑器(Your Editor)

　　现在，你的标识已经设置，你可以配置你的缺省文本编辑器，Git在需要你输入一些消息时会使用该文本编辑器。缺省情况下，Git使用你的系统的缺省编辑器，这通常可能是vi 或者 vim。如果你想使用一个不同的文本编辑器，例如Emacs，你可以做如下操作：

　　$ git config --global core.editor emacs

 

      2.3 检查你的设置(Checking Your Settings)

　　如果你想检查你的设置，你可以使用 git config --list 命令来列出Git可以在该处找到的所有的设置:

　　$ git config --list

      你也可以查看Git认为的一个特定的关键字目前的值，使用如下命令 git config {key}:

　　$ git config user.name

 

      2.4 获取帮助(Getting help)

　　如果当你在使用Git时需要帮助，有三种方法可以获得任何git命令的手册页(manpage)帮助信息:

　　$ git help <verb>

　　$ git <verb> --help

　　$ man git-<verb>

　　例如，你可以运行如下命令获取对config命令的手册页帮助:

　　$ git help config
