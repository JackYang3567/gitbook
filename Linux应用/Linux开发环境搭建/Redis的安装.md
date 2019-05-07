# Linux开发环境搭建
## 1、Redis的安装及配置
### 1.1、 下载最新版Redis
> 官网[下载](http://download.redis.io/releases/), 进入后拉到底，选择以*.tar.gz最新版本，鼠标右击复制链接  
打开终端：  

```
$ cd /usr/local/
$ wget http://download.redis.io/releases/redis-5.0.4.tar.gz

```

### 1.2、 解压安装Redis


```
$ tar xzf redis-5.0.4.tar.gz
$ cd redis-5.0.4
$ make
$ make install
$ src/redis-server

$ src/redis-cli
redis> set foo bar
OK
redis> get foo
"bar"
```
### 1.3、启动服务器
```
cd /usr/local/src/redis-5.0.4
src/redis-server
```
### 1.4、运行客户端
```
src/redis-cli
```
### 1.5、设置redis的开机自启动
#### 1.5.1、移动相关文件
```
mkdir -p /usr/local/redis
[root@localhost redis-5.0.4]# cp redis.conf /usr/local/redis/
[root@localhost redis-5.0.4]# cd src
[root@localhost src]# cp redis-server /usr/local/redis/
[root@localhost src]# cp redis-cli /usr/local/redis/
```
#### 1.5.2、编辑配置文件redis.conf
```
vim /usr/local/redis/redis.conf
```
> 将 daemonize no 修改为 yes  
 

#### 1.5.3、添加开机启动服务

```
vim /etc/systemd/system/redis-server.service
```
>复制下方代码时，在vim中一定要检查是否一致

```
[Unit]
Description=The redis-server Process Manager
After=syslog.target network.target

[Service]
Type=simple
PIDFile=/var/run/redis_6379.pid
ExecStart=/usr/local/redis/redis-server /usr/local/redis/redis.conf         
ExecReload=/bin/kill -USR2 $MAINPID
ExecStop=/bin/kill -SIGINT $MAINPID

[Install]
WantedBy=multi-user.target
```
#### 1.5.4、刷新配置
```
systemctl daemon-reload 
systemctl start redis-server.service 
systemctl enable redis-server.service
```

### 1.6、启动、重启、停止
````
systemctl start redis
systemctl restart redis
systemctl stop redis
````
### 1.7、创建自动启动软链接
创建软链接是为了下一步系统初始化时自动启动服务
```
ln -s /lib/systemd/system/redis.service /etc/systemd/system/multi-user.target.wants/redis.service
```
### 1.8、设置开机启动
```
systemctl enable redis
```
### 1.9、禁止开机启动
```
systemctl disable redis
```

### 1.10、创建redis命令软连接
ln -s /usr/local/redis/redis-cli /usr/bin/redis


## 2、Redis可视化工具
Redis可视化工具Redis Desktop Manager使用
```
vi /usr/local/redis/redis.conf
找到# requirepass foobared
修改为 requirepass redis
修改redis.conf配置文件，去掉redis配置文件的bind 127.0.0.1这个限制，让所有都可以连接。
修改配置文件，在redis3.2之后，redis增加了protected-mode，在这个模式下，即使注释掉了bind 127.0.0.1，再访问redisd时候还是报错，如下 
修改办法：protected-mode no 
```


## 3、Redis应用中相关报错

### 3.1、service redis does not support chkconfig 
#### 3.1.1、解决办法
必须把下面两行注释放在/etc/init.d/redis文件靠前的注释中：
```
# chkconfig:   2345 90 10
# description:  Redis is a persistent key-value database
```
(error) NOAUTH Authentication required.  
127.0.0.1:6379> auth redis

