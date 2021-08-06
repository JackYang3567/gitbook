#  Linux常用命令
——CentOS7.2常用命令   https://www.cnblogs.com/yjd_hycf_space/p/7730690.html

## 1、系统信息  

### 1.1、查看版本
#### 1.1.1、查看redhat的release版本  
——查看已经安装的CentOS版本信息  

```
$ cat /etc/redhat-release
```
> 显示 ：  
CentOS Linux release 7.2.1511 (Core)  

#### 1.1.2、显示内核的版本 
```
$ cat /proc/version
```
> 显示 ：  
Linux version 3.10.0-327.4.5.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC) ) #1 SMP Mon Jan 25 22:07:14 UTC 2016

#### 1.1.3、显示当前操作系统名称、版本、机器的处理器架构
```
$ uname -a
```
> 显示 ：Linux localhost.localdomain 3.10.0-327.4.5.el7.x86_64 #1 SMP Mon Jan 25 22:07:14 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

##### 1.1.3.1、显示当前操作系统版本、机器的处理器架构
```
uname -r
```
> 显示 ：
3.10.0-327.4.5.el7.x86_64  

##### 1.1.3.2、显示当前机器的处理器架构

```
$ uname -m
```
> 显示 ：x86_64

或:
```  
$ arch
```
> 显示 ：x86_64

### 1.2、 显示系统日期 
#### 1.2.1、显示系统当前日期 
```
$ date
```
> 显示 ：Tue  7 May 14:06:57 CST 2019  

#### 1.2.2、显示指定年份的日历表
```
$ cal 2021 显示2021年的日历表
```

#### 1.2.3、设置日期和时间 - 月日时分年.秒 
```
date 050714282021.00
```
### 1.3、 cat /proc/ 系列
#### 1.3.1、显示CPU info的信息
```
$ cat /proc/cpuinfo

processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 60
model name      : Intel(R) Core(TM) i5-4590 CPU @ 3.30GHz
stepping        : 3
cpu MHz         : 3292.035
cache size      : 6144 KB
physical id     : 0
siblings        : 2
....
```

#### 1.3.2、显示中断
```
$ cat /proc/interrupts
           CPU0       CPU1
  0:        131          0   IO-APIC-edge      timer
  1:          1          9   IO-APIC-edge      i8042
  8:          0          1   IO-APIC-edge      rtc0
  9:          0          0   IO-APIC-fasteoi   acpi
 12:          0        155   IO-APIC-edge      i8042
 14:          0          0   IO-APIC-edge      ata_piix
 15:          0          0   IO-APIC-edge      ata_piix
 16:         99      10053   IO-APIC-fasteoi   enp0s8
 19:          0      18485   IO-APIC-fasteoi   enp0s3
 20:          0       8107   IO-APIC-fasteoi   vboxguest
 21:      26274      11841   IO-APIC-fasteoi   0000:00:0d.0
NMI:          0          0   Non-maskable interrupts
LOC:    1322337    1434519   Local timer interrupts
SPU:          0          0   Spurious interrupts
PMI:          0          0   Performance monitoring interrupts
IWI:     243659     157804   IRQ work interrupts
RTR:          0          0   APIC ICR read retries
RES:     415254     390263   Rescheduling interrupts
CAL:       7256      11527   Function call interrupts
TLB:      33068      13870   TLB shootdowns
TRM:          0          0   Thermal event interrupts
THR:          0          0   Threshold APIC interrupts
MCE:          0          0   Machine check exceptions
MCP:         68         68   Machine check polls
ERR:          0
MIS:          0
```
#### 1.3.3、校验内存使用 

```
$ cat /proc/meminfo

MemTotal:         629984 kB
MemFree:           75648 kB
MemAvailable:     118852 kB
Buffers:               0 kB
Cached:           127716 kB
SwapCached:        15580 kB
Active:           204796 kB
Inactive:         274520 kB
Active(anon):     150036 kB
Inactive(anon):   218552 kB
Active(file):      54760 kB
Inactive(file):    55968 kB
```
#### 1.3.4、显示哪些swap被使用 

```
$ cat /proc/swaps
Filename        Type           Size      Used     Priority
/dev/dm-1       partition      1023996   115468   -1
```

#### 1.3.5、显示内核的版本 
```
$ cat /proc/version

Linux version 3.10.0-327.4.5.el7.x86_64 (builder@kbuilder.dev.centos.org) (gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC) ) #1 SMP Mon Jan 25 22:07:14 UTC 2016
```

#### 1.3.6、显示网络适配器及统计
```
$ cat /proc/net/dev
```

#### 1.3.7、显示已加载的文件系统
```
$ cat /proc/mounts

rootfs / rootfs rw 0 0
sysfs /sys sysfs rw,nosuid,nodev,noexec,relatime 0 0
proc /proc proc rw,nosuid,nodev,noexec,relatime 0 0
devtmpfs /dev devtmpfs rw,nosuid,size=305300k,nr_inodes=76325,mode=755 0 0
securityfs /sys/kernel/security securityfs rw,nosuid,nodev,noexec,relatime 0 0
tmpfs /dev/shm tmpfs rw,nosuid,nodev 0 0
```
### 1.4、 显示硬件系统部件
#### 1.4.1、显示硬件系统部件
```
$ dmidecode -q

BIOS Information  //##BIOS信息
        Vendor: innotek GmbH
        Version: VirtualBox
        Release Date: 12/01/2006
        Address: 0xE0000
        Runtime Size: 128 kB
        ROM Size: 128 kB  //只读存储器大小
        Characteristics:
                ISA is supported
                PCI is supported
                Boot from CD is supported
                Selectable boot is supported
                8042 keyboard services are supported (int 9h)
                CGA/mono video services are supported (int 10h)
                ACPI is supported

System Information
        Manufacturer: innotek GmbH
        Product Name: VirtualBox
        Version: 1.2
        Serial Number: 0
        UUID: 14EAB622-2104-4D81-85B6-094289FB07DE
        Wake-up Type: Power Switch
        SKU Number: Not Specified
        Family: Virtual Machine

Base Board Information
        Manufacturer: Oracle Corporation
        Product Name: VirtualBox
        Version: 1.2
        Serial Number: 0
        Asset Tag: Not Specified
        Features:
                Board is a hosting board
        Location In Chassis: Not Specified
        Type: Motherboard

Chassis Information
        Manufacturer: Oracle Corporation
        Type: Other
        Lock: Not Present
        Version: Not Specified
        Serial Number: Not Specified
        Asset Tag: Not Specified
        Boot-up State: Safe
        Power Supply State: Safe
        Thermal State: Safe
        Security Status: None

OEM Strings
        String 1: vboxVer_6.0.4
        String 2: vboxRev_128413
```

#### 1.4.2查看系统是32位或者64位的方法
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


## 2、关机 (系统的关机、重启以及注销 ) 
### 2.1、 Linux centos重启命令

#### 2.1.1、reboot重启
```
　$ reboot             #立刻重启
```
#### 2.1.2、shutdown -r 重启
```
　$ shutdown -r now    #立刻重启(root用户使用)
　$ shutdown -r 10     #过10分钟自动重启(root用户使用)
　$ shutdown -r 20:35  #在时间为20:35时候重启(root用户使用)
```
> 如果是通过shutdown命令设置重启的话，可以用shutdown -c 命令取消重启

### 2.2、 Linux centos关机命令

#### 2.2.1、 halt 立刻关机
```
$ halt             #立刻关机
```
#### 2.2.2、poweroff 立刻关机
```
$ poweroff         #立刻关机
```

#### 2.2.3、 shutdown 关机
```
$ shutdown -h now  #立刻关机(root用户使用)
$ shutdown -h 10   #10分钟后自动关机
```
>如果是通过shutdown命令设置关机的话，可以用shutdown -c命令取消关机  

#### 2.2.4、 init 0 关闭系统
```
$ init 0           #关闭系统
```
#### 2.2.5、 telinit 0 关闭系统
```
$ telinit 0        #关闭系统
``` 

### 2.3、 Linux centos注销：
```
$ logout
```

## 3、文件和目录操作 
### 3.1、切换目录 cd
```
[vagrant@localhost ~]$   #当前在个人的主目录 ~

$ cd  /                  #切换到根目录  /
[vagrant@localhost /]$

$ cd  /home              #切换到home目录
[vagrant@localhost home]$

$ cd  ..                 #返回上一级目录
[vagrant@localhost /]$
$ cd /www/wwwroot/ 
$ cd  ../..              #返回上两级目录 
[vagrant@localhost /]$
$ cd  ~                  #进入个人的主目录 
$ cd  -                  #返回上次所在的目录       
```

### 3.2、显示当前目录 pwd
```
$ pwd
```
### 3.3、列出目录中的文件 ls -laF
```
$ ls             #查看目录中的文件
$ ls  -F         #查看目录中的文件
$ ls  -l         #显示文件和目录的详细资料 
$ ls  -a         #显示隐藏文件 
$ ls *[0-9]*     #显示包含数字的文件名和目录名 
$ ls -lSr |more  #以尺寸大小排列文件和目录 
```
### 3.4、创建目录 mkdir
```
$ mkdir test-1                 #创建一个叫做 'test-1' 的目录' 
mkdir: cannot create directory ‘test-1’: Permission denied
$ su root 或 sudo

$ mkdir test-1 test-12         #同时创建两个目录 
$ mkdir -p test-1/test-2       #创建一个目录树 
```
### 3.5、删除目录 rm
```
$ rm -f ftest-1                #删除一个叫做 'test-1' 的文件' 
  rm: cannot remove ‘test-1/’: Is a directory

$ rmdir test-1                #删除一个叫做 'test-1 ' 的空目录' 

$ rm -rf test-1 test-12        #同时删除两个目录及它们的内容
```
### 3.6、移动（重命名）目录 mv
```
$ mv test-1/ mytest     #重命名/移动 一个目录 
```
### 3.7、复制目录 cp
```
$ cp  myfile1  myfile2    #复制一个文件 
$ cp  cp testdir/* .      #复制一个目录下的所有文件到当前工作目录 
$ cp -a /tmp/dir1 .       #复制一个目录到当前工作目录 
$ cp -a dir1 dir2         #复制一个目录 
```
### 3.8、链接 ln 
```
$ ln -s file1 lnk1    #创建一个指向文件或目录的软链接 
$ ln file1 lnk1       #创建一个指向文件或目录的物理链接 
```
### 3.9、修改一个文件或目录的时间戳
```
$ touch -t 1905071551 doc1    # 修改一个文件或目录的时间戳 - (YYMMDDhhmm)
```

## 4、文件搜索 

### 4.1、find搜索
```
$ find / -name doc1      #从 '/' 开始进入根文件系统搜索文件和目录 
$ find / -user user1      #搜索属于用户 'user1' 的文件和目录 
$ find /home/user1 -name \*.bin    #在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件 
$ find /usr/bin -type f -atime +100  #搜索在过去100天内未被使用过的执行文件 
$ find /usr/bin -type f -mtime -10   #搜索在10天内被创建或者修改过的文件 
$ find / -name \*.rpm -exec chmod 755 '{}' \;  #搜索以 '.rpm' 结尾的文件并定义其权限 
$ find / -xdev -name \*.rpm  #搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备 
```
### 4.2、locate搜索
```
locate \*.ps 寻找以 '.ps' 结尾的文件 - 先运行 'updatedb' 命令 
```
### 4.3、whereis搜索
```
$ whereis wget
wget: /usr/bin/wget /usr/share/man/man1/wget.1.gz
显示一个二进制文件、源码或man的位置
```

### 4.4、which搜索
```
$ which yum
/usr/bin/yum
显示一个二进制文件或可执行文件的完整路径 
```
## 5、挂载一个文件系统 

## 6、磁盘空间 

```
$ df -h            #显示已经挂载的分区列表 
$ du -sh home      #估算目录 'home' 已经使用的磁盘空间' 
$ du -sk * | sort -rn #以容量大小为依据依次显示文件和目录的大小 
$ rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n 以大小为依据依次显示已安装的rpm包所使用的空间 (fedora, redhat类系统) 
$ dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n 以大小为依据显示已安装的deb包所使用的空间 (ubuntu, debian类系统) 
```

## 7、用户和群组 

## 8、文件的权限 - 使用 "+" 设置权限，使用 "-" 用于取消 

## 9、文件的特殊属性 - 使用 "+" 设置权限，使用 "-" 用于取消 

## 10、打包和压缩文件 

## 11、RPM 包 - （Fedora, Redhat及类似系统） 

## 12、YUM 软件包升级器
### 12.1、 yum list 列出当前系统中安装的所有包 
```
$ yum list
```

### 12.2、 yum remove 删除一个rpm包 
```
$ yum remove package_name
```

### 12.3、 yum install下载并安装一个rpm包
```
//下载并安装一个rpm包
$ yum install package_name  


//将安装一个rpm包，使用你自己的软件仓库为你解决所有依赖关系
$ yum localinstall package_name.rpm 
 
```
### 12.4、 升级CentOS
```
$ yum -y upgrade   #升级所有包和系统版本，不改变内核,软件和系统设置
或：
$ yum -y update    #升级所有包,系统版本和内核，改变软件设置和系统设置
```
### 12.5、yum clean 清除yum下载的软件包

> yum 会把下载的软件包和header存储在cache中，而不会自动删除。
> yum clean指令进行清除yum下载的软件包
```
$ yum clean headers    #删除所有头文件
$ yum clean packages   #清除下载的rpm包
$ yum clean all        #全部清除所有缓存的包和头文件 
```




## 13、 CentOS7查看和关闭防火墙
- 查看防火墙状态
  ```
  $ firewall-cmd --state
  ```
  not running

## 14、 Linux如何查看端口
```
 # lsof -i:80
 -bash: lsof: command not found 

 # yum install lsof

 # lsof -i:80
 COMMAND  PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
 nginx   1840   root    6u  IPv4  17124      0t0  TCP *:http (LISTEN)
 nginx   1841 nobody    6u  IPv4  17124      0t0  TCP *:http (LISTEN)
```


