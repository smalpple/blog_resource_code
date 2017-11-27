---
title: adb常用命令
date: 2017-04-12 11:18:46
tags:
categories: 测试
---
## adb 常用命令
- 查看连接计算机的设备：
```bash
adb devices
```
...
<!-- more -->
- 获取序列号：
```bash
adb get-serialno
```
- 查看模拟器/设施的当前状态:
```bash
adb get-state
```
- 重启机器：
```bash
adb reboot
```
- 重启到recovery，即恢复模式：
```bash
adb reboot recovery
```
- 查看log
```bash
adb logcat
```
- 终止adb服务进程：
```bash
adb kill-server
```
- 安装APK：
```bash
adb install <apkfile> //比如：adb install baidu.apk
```
- 卸载APK：
```bash
adb uninstall <package> //比如：adb uninstall com.baidu.search
```
- 从本地复制文件到设备：
```bash
adb push <local> <remote>
```
- 从设备复制文件到本地：
```bash
adb pull <remote> <local>
```
- 清除log缓存：
```bash
adb logcat -c
```
- 查看bug报告：
```bash
adb bugreport
```
- 查看ADB帮助：
```bash
adb help
```
## adb shell常用命令
- 获取编译时间
```bash
cat /proc/version
```
- 获取硬件信息
```
adb shell getprop | grep cpu
```
- 查看Service列表
```
adb shell service list
adb shell dumpsys activity services
```
- 检查Service是否存在
```
adb shell service check phone
```
- 获取机器MAC地址：
```
adb shell cat /sys/class/net/wlan0/address
```
- 获取CPU序列号：
```
adb shell cat /proc/cpuinfo
```
- 启动应用：
```
adb shell am start -n <package_name>/.<activity_class_name>
```
- 查看数据库：
```
adb shell content query --uri content://settings/secure
```
- 查看设备cpu和内存占用情况：
```
adb shell top
```
- 查看占用内存前6的app：
```
adb shell top -m 6
```
- 刷新一次内存信息，然后返回：
```
adb shell top -n 1
```
- 查询各进程内存使用情况：
```
adb shell procrank
```
- 启动应用程序:
```
adb shell am
```
- 杀死一个进程：
```
adb shell kill [pid]
```
- 查看进程列表：
```
adb shell ps
```
- 查看Android系统的属性
```
adb shell prop
```
- 查看指定进程状态：
```
adb shell ps -x [PID]
```
- 查看后台services信息：
```
adb shell service list
```
- adb 查看最上层成activity名字：
```
linux:
adb shell dumpsys activity | grep "mFocusedActivity"
windows:
adb shell dumpsys activity | findstr "mFocusedActivity"
```
- 查看当前内存占用：
```
adb shell cat /proc/meminfo
```
- 查看IO内存分区：
```
adb shell cat /proc/iomem
```
- 进入文件夹，等同于dos中的cd 命令：
```
adb shell cd <folder>
```
- 重命名文件：
```
adb shell rename path/oldfilename path/newfilename
```
- 删除system/avi.apk：
```
adb shell rm /system/avi.apk
```
- 删除文件夹及其下面所有文件：
```
adb shell rm -r <folder>
```
- 移动文件：
```
adb shell mv path/file newpath/file
```
- 设置文件权限：
```
adb shell chmod 777 /system/fonts/DroidSansFallback.ttf
```
- 新建文件夹：
```
adb shell mkdir path/foldelname
```
- 查看文件内容：
```
adb shell cat <file>
```
- 查看wifi密码：
```
adb shell cat /data/misc/wifi/*.conf
```
- 跑monkey：
```
adb shell monkey -v -p your.package.name 500
```
- 查看应用程序内存使用情况:
```
adb shell dumpsys meminfo <package_name>
```
> 其中，package_name 也可以换成程序的pid,
 pid可以通过 adb shell top | grep app_name 来查找.
 内存使用情况参考http://blog.csdn.net/bigconvience/article/details/35553983

- 查看进程占用cpu的情况:
```
adb shell top -n 1 -d 0.5 | grep proc_ id
```
- procrank查看内存占用：
```
adb shell procrank
```
> VSS - Virtual Set Size 虚拟耗用内存（包含共享库占用的内存）
  RSS - Resident Set Size 实际使用物理内存（包含共享库占用的内存）
  PSS - Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）
  USS - Unique Set Size 进程独自占用的物理内存（不包含共享库占用的内存）

- 快速查看apk内androidmanifest文件内容:
```
aapt dump xmltree xxxx.apk AndroidManifest.xml
```
- 列出一些系统信息和所有应用的信息:
```
adb shell dumpsys packages > d:\\packages.txt
```
- 列出一些指定应用的信息:
```
adb shell dumpsys package com.ijinshan.duba > d:\\duba.txt
```
- 查看当前谁持有WAKE_LOCK锁对象：
```
adb shell dumpsys power
```
- 查看电池用量详情：
```
adb shell dumpsys batteryinfo
```
- 搜索文件：
```
busybox find -name *xxx*
```
- 电池日志：
```
adb shell dumpsys batterystats > x:\batterystats.txt
bugreport日志：adb bugreport > x:\bugreport.txt
```
电池日志图形界面查看
https://github.com/cacker/battery-historian

- 查看应用uid
```
cat /proc/<pid>/status
cat /data/system/packages.list | grep xxx
```
- cpu频率
查看：
```
cat [%cpuFreqPath%]/cpuinfo_cur_freq (当前cpu频率)
```
修改：
```
echo xxx > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq (当前cpu频率)
cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq (最大cpu频率)
cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_min_freq (最小cpu频率)
cat /sys/devices/system/cpu/cpu0/cpufreq/related_cpus (cpu数量标号,从0开始,如果是双核,结果为0,1)
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies (cpu所有可用频率)
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors (cpu所有可用调控模式)
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor (当前使用哪种调控模式)
cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_transition_latency (变频延迟)
```
- 某个应用内存消耗信息
```
adb shell dumpsys meminfo sina.mobile.tianqitong > d:\\meminfo.txt
```
- zygote的堆栈dump

> adb shell // 进入shell
  chmod 777 /data/anr // /data/anr设置可读写权限
  rm -r traces.txt // 删除原始traces
  adb shell ps //查看进程pid
  kill -3 //
  adb pull /data/anr/traces.txt d:/trace.txt
  trace中查看cpu调度的基本信息

  ```
  "Thread-196" prio=5 tid=27 SUSPENDED
  | sysTid=2271 nice=0 sched=0/0 cgrp=apps/bg_non_interactive handle=1543812984
  | state=S schedstat=( 1177036142201 119659820902 234955 ) utm=84431 stm=33272 core=0
  #00  pc 000217a8  /system/lib/libc.so (__futex_syscall3+8)
  #01  pc 0000e09c  /system/lib/libc.so (__pthread_cond_timedwait_relative+48)
  #02  pc 0000e0f8  /system/lib/libc.so (__pthread_cond_timedwait+60)
  #03  pc 0005419d  /system/lib/libdvm.so (dvmChangeStatus(Thread*, ThreadStatus)+72)
  #04  pc 00049995  /system/lib/libdvm.so
  #05  pc 0004b9c1  /system/lib/libdvm.so
  #06  pc 0006e721  /system/lib/libandroid_runtime.so
  #07  pc 0001e610  /system/lib/libdvm.so (dvmPlatformInvoke+112)
  #08  pc 0004df29  /system/lib/libdvm.so (dvmCallJNIMethod(unsigned int const*, JValue*, Method const*, Thread*)+500)
  #09  pc 00027a24  /system/lib/libdvm.so
  #10  pc 000fedc8  [stack:2271]
  at android.util.Log.println_native(Native Method)
  at android.util.Log.println(Log.java:332)
  at com.android.internal.os.AndroidPrintStream.log(AndroidPrintStream.java:47)
  at com.android.internal.os.LoggingPrintStream.println(LoggingPrintStream.java:311)
  at java.net.PlainSocketImpl.read(PlainSocketImpl.java:487)
  at java.net.PlainSocketImpl.access$000(PlainSocketImpl.java:46)
  at java.net.PlainSocketImpl$PlainSocketInputStream.read(PlainSocketImpl.java:240)
  at java.io.InputStream.read(InputStream.java:163)
  at java.io.BufferedInputStream.fillbuf(BufferedInputStream.java:142)
  at java.io.BufferedInputStream.read(BufferedInputStream.java:309)
  at com.sina.push.i.c.c(SourceFile:241)
  at com.sina.push.i.c.b(SourceFile:133)
  at com.sina.push.i.c.d(SourceFile:270)
  at com.sina.push.i.c.e(SourceFile:496)
  at com.sina.push.i.c.<init>(SourceFile:97)
  at com.sina.push.b.a.b.a(SourceFile:56)
  at com.sina.push.b.e.a(SourceFile:166)
  at com.sina.push.b.e$b$a.run(SourceFile:487)
  ```
其中schedstat=( 1177036142201 119659820902 234955 ) utm=84431 stm=33272 core=0
从左到右六个数字分别是:
1- 当前线程在cpu上消耗的时间
2- 当前任务在CPU任务轮询中的等待时间
3- 当前线程在这个cpu上运行的次数
4- 当前线程的用户态执行时间
5- 当前线程的内核态执行时间
6- 当前线程在哪里个核心上执行
实际上描述了调度的基本信息

- SYSTEM LOG
```
logcat -b system -v time -d *:v | grep sina.mobile
```
> -b // 加载一个可使用的日志缓冲区供查看，比如event和radio,默认值是main.
  system // system log
  -v // 输出字段 time 显示时间
  -d // 缓冲区日志打印并退出
  *:v // 日志级别高到低 E W I D V
  grep sina.mobile // 过滤包含sina.mobile的信息