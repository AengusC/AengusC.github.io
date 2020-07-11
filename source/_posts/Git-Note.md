---
title: Git 学习笔记
date: 2020-03-12 11:43:33
tags:
    - 学习笔记
    - 技术
    - GIT
categories: 
    - 笔记
    - GIT
cover: https://i.loli.net/2020/03/13/Fnxi1LTuImwdavc.jpg
---
#### 一.git 创建本地版本库小结
初始化一个Git仓库,使用`git init`命令。\
添加文件到Git仓库,分两步：\
使用命令`git add <file>`,注意,可反复多次使用,添加多个文件；\
使用命令`git commit -m <message>` 完成.	
***

#### 二.要随时掌握工作区的状态

1.使用`git status`命令。

2.如果`git status`告诉你有文件被修改过,用git diff可以查看修改内容。
***

#### 三.版本回退

1.HEAD指向的版本就是当前版本,因此,Git允许我们在版本的历史之间穿梭,
使用命令`git reset --hard commit_id`。

2.穿梭前,用`git log`可以查看提交历史,以便确定要回退到哪个版本。

3.要重返未来,用`git reflog`查看命令历史,以便确定要回到未来的哪个版本。

***

#### 四.工作区和暂存区

1.就是你在电脑里能看到的目录,比如我的`AengusChen.github.io`文件夹就是一个工作区\

2.工作区有一个隐藏目录.git,这个不算工作区,而是Git的版本库,Git的版本库里存了很多东西,其中最重要的就是称为stage（或者叫index）的暂存区,还有Git为我们自动创建的第一个分支`master`,以及指向master的一个指针叫HEAD。

3.git管理的是修改,也就是说每次修改需要git add <file> 放入到暂存区,然后`git commit`才能算最终的修改。


![0.jpg](https://i.loli.net/2020/03/11/gZGwzKQbujBacJM.jpg)
***

#### 五.撤销修改场景

场景1：当你改乱了工作区某个文件的内容,想直接丢弃工作区的修改时,用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容,还添加到了暂存区时,想丢弃修改,分两步,第一步用命令`git reset HEAD <file>`,就回到了场景1,第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时,想要撤销本次提交,参考版本回退一节,不过前提是没有推送到远程库。
***

#### 六.删除情景

1.在文件管理器中删除文件,只删除了工作区的文件,暂存区的文件并未更新,
会导致工作区与暂存区的文件版本不一致,这个时候可以使用`git rm` 删除暂存区的文件,也可以使用 git reflog查看命令历史操作日志,然后用`git reset --hard +log`中的ID进行回滚。

2.直接使用 `git rm <文件名>` 同时删除工作区与暂存区的文件。


3.以上两种操作都是可以回滚的,除非是 git push -u origin master 提交至远程仓库,只要是在暂存区的文件都可以通过日志找到ID进行回滚。
***

#### 七.添加github远程库与本地git工作区建立连接

1.`git remote add origin` 自己github中仓库的SSH地址\

2.`git push -u origin master` 第一次推送本地库的master所有内容至
远程库。

3.`git push origin master` 只要进行过步骤二的操作,就可以通过这个命令进行推送了。
***

#### 八.从远程克隆github库到本地

1.git clone github仓库的SSH地址 (建议用SSH协议,http协议速度太慢,每次都要输入口令)