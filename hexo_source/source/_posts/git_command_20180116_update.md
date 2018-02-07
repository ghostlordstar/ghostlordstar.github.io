---
title: git常用命令(20180116更新)
date: 2017-11-22 19:20
tags:
	-	Mac
	-	git
	-	终端
	-	命令
---

更新信息：

-----
20180116：

```
1.添加Mac 终端的基础操作命令
2.修改排版
```

20171211：

```
1.添加撤销文件在工作区的修改命令（命令 2.14）
```

20171205：

```
1.添加版本操作命令分区
```

20171123：

```
1.添加几个新的分支操作命令
2.修改错误的一个分支操作命令
```

20171122：

```
1.第一次发表
```

-----
<!--more-->
# git 常用命令

## 1. 基础命令

	#1.1 克隆远程仓库到本地，克隆到当前文件夹下
	$ git clone git@server:/srv/sample.git

	#1.2 查看工作空间状态
	$ git status

	#1.3 添加修改文件
	$ git add xxx(文件路径+文件名.*)

	#1.4 添加所有修改的文件
	$ git add --all / git add -A

	#1.5 提交修改到暂存区
	$ git commit -m "提交描述"

	#1.6 拉取远端的最新变更(示例为拉取远端的master分支最新变更)
	$ git pull origin master

	#1.7 推送当前变更到远端(示例为推送本地代码到远端的master分支)
	$ git push origin master

	#1.8 合并本地分支到当前分支（示例为合并develop_branch分支到当前分支）
	$ git merge develop_branch

## 2. 分支操作命令

	#2.1 列出所有远程仓库（列出所有仓库，包括克隆地址）
	$ git remote -v

	#2.2 展示远程仓库的详细信息(示例为展示origin仓库的详细信息)
	$ git remote show origin

	#2.3 重命名远程仓库名称（示例为将origin 重命名为 origin_rename）
	$ git remote rename origin origin_rename

	#2.4 移除远程仓库（示例为移除origin仓库）
	$ git remote rm origin

	#2.5 添加远程仓库（添加一个名为origin_1的远程仓库）
	$ git remote add origin_1 giturl

	#2.6 列出所有在当前仓库下的远程分支
	$ git branch -r

	#2.7 删除远程分支(示例为删除远程仓库下的 develop 分支)
	$ git push origin --delete develop

	#2.8 列出所有当前本地分支（带有*标志的分支为当前所在分支）
	$ git branch

	#2.9 删除本地分支(示例为删除本地为dev的分支)
	$ git branch -D dev

	#2.10 更新所有当前远程仓库下的远程分支列表(示例更新的是origin仓库下的分支列表)
	$ git remote update origin --prune

	#2.11 从当前版本分支创建一个新的本地分支(示例是:从当前分支创建一个新的本地分支dev)
	$ git branch dev

	#2.12 从远程分支创建一个新的本地分支（示例为:从origin/master分支创建一个命为dev_r 的本地分支）
	$ git checkout -b dev_r origin/master

	#2.13 切换分支（从当前分支切换到dev分支）
	$ git checkout dev

	#2.14 撤销某个文件在工作区的修改（示例为:撤销test.md文件在工作区的修改）
	$ git checkout -- test.md

## 3.版本操作命令
	#3.1 查看版本提交记录(不添加任何参数，默认会按照提交时间排序，最新提交在最上面)
	$ git log

	#3.2 回滚到指定版本 (示例为：回滚到e377f60e28c8b84158版本,)
	$ git reset --hard e377f60e28c8b84158

------

# 拓展：终端常用命令

>* 备注：无特殊说明命令行下的操作都是对当前目录进行操作，如果想要在当前目录下操作其他目录，需要在命令后添加上路径，例如：

```
# 列出当前目录下的文件和文件夹
$ ls

# 列出指定目录下的文件和文件夹(列出根目录下的Users目录中的内容)
$ ls /Users

```

## 1. 文件操作命令

	#1.1 查看当前目录(列出当前目录下未隐藏的文件和文件夹)
	$ ls

	#1.2 查看当前目录所有文件和文件夹(包括隐藏的)
	$ ls -ah

	#1.3 查看当前所处的路径
	$ pwd

	#1.3 新建文件夹(在当前目录下新建一个名为XXXX的文件夹，"sudo" 为使用管理员权限，在一些特定的路径下只有管理员才有权限建立新的文件夹)
	$ (sudo) mkdir XXXX

	#1.4 删除文件夹(可以删除非空文件夹，删除当前目录下名为XXXX的文件夹，"-rf" 表示递归和强制，慎用！)
	$ (sudo) rm -rf XXXX

	#1.5 进入下级目录(示例为进入当前目录的xxxx目录)
	$ cd xxxx

	#1.6 回到上级目录
	$ cd ..

	#1.7 回到根目录
	$ cd
