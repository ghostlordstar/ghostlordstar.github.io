---
title: cocoapods(1.3.1)全新安装（20171124更新）
date: 2016-08-05 13:26
tags:
  - Mac
  - 终端
  - 命令
  - cocoapods
  - rvm
  - ruby
---

cocoapods使用以前方法安装时会出错，现更新下安装方法
1、 安装nodejs 、Xcode和Command line tools 会避免很多麻烦。
1.1 、安装nodejs,官网下载，安装(https://nodejs.org/en/)
1.2 、首先安装好Xcode，并且打开一次Xcode，主要是为了授权
1.3 、安装command line tools (一般安装过Xcode的就不用再安装了),不安装时使用rvm更新ruby环境会报错 ，注意cocommand line tools一定要对应的Xcode版本(比如我的Xcode版本是7.3.1，我下载的就是如下图的cocommand line tools)
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-e791419c4cbf61f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
1.4、如果不能在网页上下载command line tool,也可以从终端中安装：
在终端中输入：
```
xcode-select --install
```
回车后会弹出一个弹框，选择安装，然后等待显示安装完成即可

2、使用rvm更新ruby环境
<!--more-->
2.1 、安装rvm(官方网址:http://www.rvm.io/)
在终端中：复制以下代码，回车
```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```
如果报错：gpg: keyserver receive failed: No route to host ，请替换上述命令中的keyServer(hkp://keys.gnupg.net) 为:hkp://pgp.mit.edu (更新时间20171124)

如果报错：gpg:command not found,请安装gunpg(安装方法在文末备注)

如果没有错误：复制以下代码，回车
```
\curl -sSL https://get.rvm.io | bash -s stable
```
2.2 、rvm安装成功后需要更新ruby环境,cocoapods 1.0.1要求ruby环境 >= 2.2.2
#### 注意：如果安装成功还是显示command not found,请重启一下终端窗口
```
# 列出已知版本
rvm list known

# 安装2.2.2版本（更高版本格式也一样）
rvm install ruby-2.2.2
```
3 、安装cocoapods
```
# 查看现在的ruby环境
gem sources -l

# 移除原有的ruby镜像源（如果有稳定的翻墙环境可以不替换源）
gem sources --remove https://rubygems.org/

# 换成国内的淘宝镜像
gem sources -a https://ruby.taobao.org/

# 安装cocoapods
sudo gem install cocoapods

# 安装成功后需要设置一下
pod setup
```
如果pod setup出现Setting up CocoaPods master repo,半天没有任何反应
可以考虑自己下载库文件，地址：git@github.com:CocoaPods/Specs.git
[!记得是克隆（clone）,不是下载zip,如果有客户端可以open in desktop,没有就在终端用git克隆吧]
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-d35861bcb0d6f264.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
当Specs clone完成以后，可以将文件夹内的文件全部拖到/Users/ghostlord/.cocoapods/repos/master/路径中（记得开隐藏文件[命令备注有]，因为需要隐藏的版本库文件夹）

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-f694f3a3ca43e569.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
等文件复制完成后，再回到终端pod setup ，一小会就会成功。
最终截图如下：

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2255840-ba01c6780d4af6b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

备注：
1.安装gnupg
```
brew install gnupg gnupg2
```
如果安装完成后运行显示"gnupg already installed, it's just not linked",就可以使用以下命令link
```
chmod 755 /usr/local/lib/pkgconfig
brew link gnupg
brew link gnupg2
brew doctor
```
###*如果此处还有问题，请留言，留言时请将错误信息贴出来###


2.如果报错：brew:command not found，那么就先安装Homebrew
```
 ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
如果以前安装过brew,或者安装完后在终端还是显示“-bash: brew: command not found”错误，那就将brew先卸载，然后再重新安装，以下命令是卸载命令
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

3.是否显示隐藏文件：
```
# 此命令显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool true
# 此命令关闭显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool false
# 命令运行之后需要重新加载Finder：
# 快捷键option+command+esc，选中Finder，重新启动即可
```

写的仓促，有错误请指正 /抱拳
