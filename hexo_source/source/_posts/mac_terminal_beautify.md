---
title: Mac 终端窗口美化
date: 2016-10-03 00:56
tags:
  - Mac
  - 终端
  - 美化
---
/*声明：此博文非原创，来源于网络搜集，作者已无法考证，故未列出出处*/
## 美化前效果图：

![885A6415-6907-43E6-B197-08E00F082695.png](http://upload-images.jianshu.io/upload_images/2255840-7c437d0dfa6ac8f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 开始美化：
### 1.通过终端偏好设置，选择配色和字体
```
配色方案是“Homebrew”，字体用的是“Menlo Regular 18 pt”
```
![F19F385B-E7EF-49EA-B858-9C2728E4C084.png](http://upload-images.jianshu.io/upload_images/2255840-88b14771c95ae938.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!--More-->
### 2.写配置文件，修改路径，提示符颜色，以及打开ls命令的高亮显示
>* 在用户主目录下建立一个配置文件即可：
```
vi ./.bash_profile
```
>* 然后写入（按i进入编辑模式）如下配置文件：
```
# for color(“#”此符号后为注释，可以不加输入，为了减少错误尽量复制)
export CLICOLOR=1
# \h:\W \u\$
export PS1='\[\033[01;33m\]\u@\h\[\033[01;31m\] \W\$\[\033[00m\] '
# grep
alias grep='grep --color=always'
```
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-3961205386d95ab6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>* 然后按“ESC”键，再输入":wq",其中冒号和"w"、"q"都是英文状态下的字符
```
:wq
```
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-11a6312badde7fb6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>* 回车，退回到主界面，现在就可以退出当前终端窗口，重新打开看看是否已经成为下图的效果，如果没有到下面的效果，请仔细按照步骤重新来一遍
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-1cfa3cf82e7b45d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 如果有什么错误，请不吝赐教🙏🏻。。。
