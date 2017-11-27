---
title: linux常用命令总结
date: 2017-03-27 16:46:41
tags:
categories: linux
---
常用的linux命令总结
<!-- more -->
## linux用户管理
### 查看用户
``` bash
$ who am i

或者

$ who mom likes
```
输出的第一列表示打开当前伪终端的用户的用户名（要查看当前登录用户的用户名，去掉空格直接使用 whoami 即可），第二列的 pts/0 中 pts 表示伪终端，所谓伪是相对于 /dev/tty 设备而言的，还记得上一节讲终端时的那七个使用 [Ctrl]+[Alt]+[F1]～[F7] 进行切换的 /dev/tty 设备么,这是“真终端”，伪终端就是当你在图形用户界面使用 /dev/tty7 时每打开一个终端就会产生一个伪终端， pts/0 后面那个数字就表示打开的伪终端序号，你可以尝试再打开一个终端，然后在里面输入 who am i ，看第二列是不是就变成 pts/1 了，第三列则表示当前伪终端的启动时间。
![](http://ww1.sinaimg.cn/large/006iB0xgly1fe1hxzc68fj308n08r0sv.jpg)

### 创建用户
``` bash
$ sudo adduser biyong   #创建用户
$ su -l lilei           #切换登录用户
```
退出当前用户跟退出终端一样可以使用 exit 命令或者使用快捷键 Ctrl+d。

### 用户组
#### 使用group命令
``` bash
$ groups shiyanlou
```
#### 将其它用户加入 sudo 用户组
默认情况下新创建的用户是不具有 root 权限的，也不在 sudo 用户组，可以让其加入sudo用户组从而获取 root 权限。
``` bash
$ su -l lilei
$ sudo ls
```
### 删除用户
``` bash
$ sudo deluser biyong --remove-home
```
## 文件权限
### 查看文件权限
使用较长格式列出文件：
``` bash
$ ls -l
```
![](http://ww1.sinaimg.cn/large/006iB0xgly1fe1ihgapf1j30fn067q33.jpg)
### 变更文件所有者
假设目前是 lilei 用户登录，新建一个文件，命名为 “iphone6”：
``` bash
$ touch iphone6
```
可见文件所有者是 lilei ：
现在，换回到biyong用户身份，使用以下命令变更文件所有者为 biyong ：
``` bash
$ cd /home/biyong
$ ls iphone6
$ sudo chown shiyanlou iphone6
$ cp iphone6 /home/biyong
```
### 修改文件权限
方式一：二进制数字表示
![](http://ww1.sinaimg.cn/large/006iB0xgly1fe1irc69v0j30n807b0tp.jpg)
即：
``` bash
$ chmod 700 "文件"
```
现在，其他用户已经不能读这个“文件”文件了：
方式二：加减赋值操作
``` bash
$ chmod go-rw "文件"
```
## Linux 目录结构及文件基本操作
![](http://ww1.sinaimg.cn/large/006iB0xgly1fe1k373pl0j30yn12kdky.jpg)


##未完待续
