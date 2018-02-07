---
title: Mac下运行.sh脚本
date: 2018-01-12 19:11
tags:
  - Mac
  - 终端
  - 脚本
  - sh
---

有时下载来的三方框架中会有.sh脚本，一般用来下载文件或者编译源码，所以：
# 如何运行.sh脚本

>* 1. 直接拖到终端
>* 2. 从终端中(cd)进入到脚本所在的路径，在终端中直接运行
```
# 假如在libs文件夹下,脚本名称为：test.sh
libs ./test.sh
```

# 出现'permission denied: ./test.sh'的解决办法
```
# 这种错误是因为权限问题，重新设置一下权限就可以运行
libs chmod 777 test.sh
```
