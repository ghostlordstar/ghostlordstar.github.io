---
title: svn learn
date: 2016-06-30 19:51:50
tags:
  - svn 
  - Mac
  - 终端
  - 版本控制
---
## SVN常用命令
---
### 服务器端配置
>* 参考博客：[http://www.cnblogs.com/jisheng/archive/2012/09/13/2683060.html] [Hecker385]
[http://blog.csdn.net/q199109106q/article/details/8655204] [M了个J]
#### 创建
>* 1.创建一个仓库：路径为：/Users/apple/svn，仓库名为：mycode
	svnadmin create /Users/apple/svn/mycode
	// 成功会在mycode路径下会有以下目录结构
	// README.txt conf       db         format     hooks      locks

<!--More-->
#### 配置svn的权限，主要是修改 /svn/mycode/conf 目录下的三个文件
>* 1.打开svnserve.conf 将下列配置项前面 的#和空格都去掉
```
# 其中anon-access = read 代表匿名访问的时候是只读的，若改为anon-access = none代表禁止匿名访问，需要账号密码才能访问
# anon-access = read  
# auth-access = write  
# password-db = passwd  
# authz-db = authz
```
>* 2.打开passwd ，在[users]下面添加账号和密码,例如账号：mj,密码：123
```
[users]  
mj = 123  
jj = 456  
```
>* 3.打开authz，配置用户组和权限
我们可以将在passwd里添加的用户分派到不同的用户组里，就可以对不同用户组设置不同的权限，没有必要对每个用户进行单独设置权限
在[groups]下面添加组名和用户名，多个用户名之间用逗号(,)隔开

```
[groups]
topgroup = mj,jj
// 说明mj和jj都是属于topgroup这个组的，接下来再进行权限配置。
// 使用[/]代表是svn服务器
[/]
@topgroup = rw
// 说明topgroup这个组中的所有用户对所有资源库都有读写(rw)权限，组名前要用(@),如果是用户名，不用加(@),比如mj这个用户有读写权限
```
>* 4.启动svn服务器
```
# 终端下输入
svnserve -d -r /User/apple/svn
# 或者
svnserve -d -r /User/apple/svn/mycode
# 如果没有提示就说明启动成功了
```
>* 5.关闭svn服务器
打开实用工具中的"活动监视器"，搜索svn，选择退出

------
### 客户端设置
>* 1.从本地导入代码到服务器(第一次导入)
```
# 在终端中输入
svn import /Users/ghostlord/Desktop/svntest svn://localhost/mycode/test -- username=ghostlord --password=aa -m "first repo"
// 其中 import 后面跟的是本地代码的路径，再后面是svn服务器地址，"first repo"是版本描述
```
>* 2.从服务器下载代码到客户端本地
```
# 在终端中输入
svn checkout svn://localhost/mycode --username=ghostlord --password=aa /Users/ghostlord/Desktop/code
# 将mycode仓库中的东西下载到本地桌面的code文件夹
```
>* 3.将修改过的代码同步到仓库
```
# 首先在终端中定位到/Users/ghostlord/Desktop/test目录
# 输入提交指令:
svn commit -m "修改了mian.m文件"
# 这个指令会将/Users/ghostlord/Desktop/code中所有的修改都同步到服务器
```
>* 4.更新服务器中的代码到本地
```
# 首先定位到本地的代码文件夹
# 在终端中输入:
svn update
```
>* 5.导出**版本，(不带有.svn文件夹的目录树)
```
# 导出形式是制定URL,如果指定版本号会导出指定版本，如果不指定会导出最新版本, 如果省略本地目录全路径，URL的最后一部分会作为本地目录的名字。
svn  export  [-r 版本号]  http://路径(目录或文件的全路径) [本地目录全路径]　--username　用户名
svn  export  [-r 版本号]  svn://路径(目录或文件的全路径) [本地目录全路径]　--username　用户名
# 本地检出的目录全路径到要导出的本地目录全路径，所有的本地修改将会保留，但是不在版本控制下(即没提交的新文件，因为.svn文件夹里没有与之相关的信息记录)的文件不会拷贝。
svn  export  本地检出的(即带有.svn文件夹的)目录全路径  要导出的本地目录全路径

```
>* 6.查看文件或者目录状态
```
# 目录下的文件和子目录的状态
svn status -v path
```

>* 7.删除文件：
```
svn delete path -m "delete fest file"
# 例如
svn delete svn://192.168.1.1/pro/domain/test.php -m "delete test file"
# 也可以拆开写:
svn delete test.php
svn ci -m "delete test file"
```
>* 8.查看日志
```
# 查看日志(显示这个文件的所有修改记录，及其版本号变化)
svn log test.php
```
>* 9.查看文件详细信息
```
svn info path
#例如
svn info test.php

```                                                    
>* 10.比较差异
```
# 将修改的文件与基础版本比较差异
svn diff test.php
svn diff -r m:n path(对版本m和版本n比较差异)
```

>* 11.版本库下的文件和目录列表
```
# 显示path目录下的所有属于版本库的文件和目录
svn list path
```
>* 12.创建纳入版本控制下的新目录
```
svn mkdir path
svn mkdir url
```
>* 13.恢复本地修改
```
# 恢复原始未改变的工作副本文件(恢复大部分的本地修改)。
svn revert
# 此条命令不会存取网络，并写会接触冲突的情况，但是并不会恢复被删除的目录
svn revert PATH...
```
>* 14.解决冲突
```
# 移除工作副本的目录或文件的"冲突"状态
svn resolved [path...]
# 本条命令不会依据语法来解决冲突或是移除冲突标记，它只是移除冲突标记的相关文件，然后让PATH可以再次提交
```

>* 15.输出指定文件或URL的内容。
```
# 如果指定了版本，将从指定的版本开始查找。
svn cat 目标[@版本]…
# PREV 是上一版本,也可以写具体版本号,这样输出结果是可以提交的
svn cat -r PREV filename > filename
```
