# CentOS7.2常用命令

## 1、 查看已经安装的CentOS版本信息
```
$ cat /etc/redhat-release
```
> 显示 ：
CentOS Linux release 7.2.1511 (Core)

或：
```
$ cat /proc/version
```
> 显示 ：Linux version 3.10.0-327.4.5.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC) ) #1 SMP Mon Jan 25 22:07:14 UTC 2016

或：
```
$ uname -a
```
> 显示 ：Linux localhost.localdomain 3.10.0-327.4.5.el7.x86_64 #1 SMP Mon Jan 25 22:07:14 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

或：
```
uname -r
```
> 显示 ：
3.10.0-327.4.5.el7.x86_64


## 2、 查看系统是32位或者64位的方法
```
$ getconf LONG_BIT
64
或：
$ getconf WORD_BIT
32
```
> 分析：32位的系统中int类型和long类型一般都是4字节，64位的系统中int类型还是4字节的，但是long已变成了8字节inux系统中可用”getconf WORD_BIT”和”getconf LONG_BIT”获得word和long的位数。64位系统中应该分别得到32和64。
  所以该系统为64为Linux系统。

或：
```
$ file /bin/ls
```
/bin/ls: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=aa7ff68f13de25936a098016243ce57c3c982e06, stripped

显示： ELF 64-bit LSB 即系统为64位

## 3、yum clean all
```
yum 会把下载的软件包和header存储在cache中，而不会自动删除。
yum clean指令进行清除yum 会把下载的软件包
yum clean headers清除header，
yum clean packages清除下载的rpm包，
yum clean all一全部清除
```

## 4、 升级CentOS
```
$ yum -y upgrade   #升级所有包和系统版本，不改变内核,软件和系统设置
或：
$ yum -y update    #升级所有包,系统版本和内核，改变软件设置和系统设置
```

## 5、 centos关机与重启命令
   - Linux centos重启命令：
>```
　$ reboot
　$ shutdown -r now    #立刻重启(root用户使用)
　$ shutdown -r 10     #过10分钟自动重启(root用户使用)
　$ shutdown -r 20:35  #在时间为20:35时候重启(root用户使用)
>```

如果是通过shutdown命令设置重启的话，可以用shutdown -c 命令取消重启

   - Linux centos关机命令：
> ```
$ halt             #立刻关机
$ poweroff         #立刻关机
$ shutdown -h now  #立刻关机(root用户使用)
$ shutdown -h 10   #10分钟后自动关机
> ``` 如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消关机

## 6、 CentOS7查看和关闭防火墙
- 查看防火墙状态
  ```
  $ firewall-cmd --state
  ```
  not running

## 7、 Linux如何查看端口
```
 # lsof -i:80
 -bash: lsof: command not found 

 # yum install lsof

 # lsof -i:80
 COMMAND  PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
 nginx   1840   root    6u  IPv4  17124      0t0  TCP *:http (LISTEN)
 nginx   1841 nobody    6u  IPv4  17124      0t0  TCP *:http (LISTEN)
```


