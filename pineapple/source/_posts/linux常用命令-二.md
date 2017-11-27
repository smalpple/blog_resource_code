---
title: linux常用命令(二)
date: 2017-04-11 14:41:01
tags:
categories: linux
---
## 常用的linux命令总结
<!-- more -->
### 路径
进入上一级目录：
``` bash
$ cd ..
```
进入你的 home 目录：
``` bash
$ cd ~ 
# 或者 cd /home/<你的用户名>
```
使用 pwd 获取当前路径：
``` bash
$ pwd
```
### Linux 文件的基本操作
#### 1. 新建
##### 新建空白文件
使用 touch 命令创建空白文件，关于 touch 命令，其主要作用是来更改已有文件的时间戳的（比如，最近访问时间，最近修改时间），但其在不加任何参数的情况下，只指定一个文件名，则可以创建一个指定文件名的空白文件（不会覆盖已有同名文件），当然你也可以同时指定该文件的时间戳.
``` bash
$ cd ~
$ touch test
```
##### 新建目录
使用 `mkdir`（make directories）命令可以创建一个空目录，也可同时指定创建目录的权限属性。
创建名为“ mydir ”的空目录：
``` bash
$ mkdir mydir
```
使用 `-p` 参数，同时创建父目录（如果不存在该父目录），如下我们同时创建一个多级目录（这在安装软件、配置安装路径时非常有用）：
``` bash
$ mkdir -p father/son/grandson
```
输入tree查看是否建好文件：
``` bash
$ tree
#输入tree即可以文件树的形式展现文件
```
![](http://ww1.sinaimg.cn/large/006iB0xgly1feir3grw88j30hi01qdfm.jpg)

#### 2. 复制
##### 复制文件
使用 `cp`（copy）命令复制一个文件到指定目录。
将之前创建的“ test ”文件复制到“ /home/shiyanlou/father/son/grandson ”目录中：
``` bash
$ cp test father/son/grandson
```
##### 复制目录
要成功复制目录需要加上 `-r` 或者 `-R` 参数，表示递归复制，就是说有点“株连九族”的意思：
``` bash
$ madir family
$ cp -r father family
```
#### 3. 删除
##### 删除文件
使用 `rm`（remove files or directories）命令删除一个文件：
```bash
$ rm test
```
使用 `-f` 参数强制删除：
```bash
$ rm -f test
```
##### 删除目录
跟复制目录一样，要删除一个目录，也需要加上 `-r` 或 `-R` 参数：
```bash
$ rm -r family
```
#### 4. 移动文件与文件重命名
##### 移动文件
使用 `mv`（move or rename files）命令移动文件（剪切）。
```bash
$ mkdir Documents
$ mv file1 Documentst
```
##### 重命名文件
将文件“ file1 ”重命名为“ myfile ”：
```bash
$ mv file1 myfile
```
##### 批量重命名
```bash
# 使用通配符批量创建 5 个文件:
$ touch file{1..5}.txt

# 批量将这 5 个后缀为 .txt 的文本文件重命名为以 .c 为后缀的文件:
$ rename 's/\.txt/\.c/' *.txt

# 批量将这 5 个文件，文件名改为大写:
$ rename 'y/a-z/A-Z/' *.c
```
#### 5. 查看文件
##### 使用 `cat`，`tac` 和 `nl` 命令查看文件
前两个命令都是用来打印文件内容到标准输出（终端），其中 cat 为正序显示，tac 为倒序显示。
> 标准输入输出：当我们执行一个 shell 命令行时通常会自动打开三个标准文件，即标准输入文件（stdin），默认对应终端的键盘、标准输出文件（stdout）和标准错误输出文件（stderr），后两个文件都对应被重定向到终端的屏幕，以便我们能直接看到输出内容。进程将从标准输入文件中得到输入数据，将正常输出数据输出到标准输出文件，而将错误信息送到标准错误文件中。
```bash
$ cat passwd
```
可以加上 `-n` 参数显示行号：
```bash
$ cat -n passwd
```
##### 使用 `more` 和 `less` 命令分页查看文件
```bash
$ more passwd
```
#### 6. 查看文件类型
使用 `file` 命令查看文件的类型：
```bash
$ file hello_shell.sh
```
![](http://ww1.sinaimg.cn/large/006iB0xgly1feirxpo93fj30cn00et8h.jpg)

#### 7. 添加和删除环境变量
##### 查看变量
查看 `PATH` 环境变量的内容：
```bash
$ echo $PATH
```
##### 添加变量
添加自定义路径到“ PATH ”环境变量
```bash
$ PATH=$PATH:/home/BY/mybin

```
注意这里一定要使用绝对路径。
使变量永久生效：
在每个用户的 home 目录中有一个 Shell 每次启动时会默认执行一个配置脚本，以初始化环境，包括添加一些用户自定义环境变量等等。zsh 的配置文件是 .zshrc，相应 Bash 的配置文件为 .bashrc 。它们在 etc 下还都有一个或多个全局的配置文件，不过我们一般只修改用户目录下的配置文件。
```bash
$ echo "PATH=$PATH:/home/BY/mybin" >> .zshrc
```
##### 修改和删除已有变量
###### 变量修改

变量的修改有以下几种方式：
![](http://ww1.sinaimg.cn/large/006iB0xgly1feitpcywt2j30is07qwfk.jpg)
##### 变量删除
可以使用 `unset` 命令删除一个环境变量：
```bash
$ unset temp
```
##### 让变量立即生效
前面我们在 Shell 中修改了一个配置脚本文件之后（比如 zsh 的配置文件 home 目录下的 `.zshrc`），每次都要退出终端重新打开甚至重启主机之后其才能生效，很是麻烦，我们可以使用 `source` 命令来让其立即生效，如：
```bash
$ source .zshrc
```
#### 8. 搜索文件
与搜索相关的命令常用的有 whereis，which，find 和 locate 。
- `whereis` 简单快速
```bash
$whereis who
```
	这个搜索很快，因为它并没有从硬盘中依次查找，而是直接从数据库中查询。`whereis` 只能搜索二进制文件(-b)，man 帮助文件(-m)和源代码文件(-s)。如果想要获得更全面的搜索结果可以使用 `locate` 命令。
- `locate` 快而全
```bash
$ locate /etc/sh
```
	> 注意，它不只是在 /etc 目录下查找，还会自动递归子目录进行查找。
	查找 /usr/share/ 下所有 jpg 文件：

	```bash
	$ locate /usr/share/\*.jpg
	```
- `which` 小而精
`which` 本身是 Shell 内建的一个命令，我们通常使用 which 来确定是否安装了某个指定的软件，因为它只从 PATH 环境变量指定的路径中去搜索命令：
```bash
$ which man
```