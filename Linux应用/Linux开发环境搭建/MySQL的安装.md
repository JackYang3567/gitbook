# Linux开发环境搭建
## 1、MySQL的安装


## 2、SQLyog远程链接Linux服务器的MySQL
### 2.1、 下载SQLyog
 官网[下载](https://sqlyog.en.softonic.com/)
### 2.2、 安装SQLyog
### 2.3、 连接到远程服务器上的MySQL
![conn-mysqlyog.png](conn-mysqlyog.png)


## 3、错误
### 3.1、10060 错误 
  **报错：** Can't connect to MySQL server on '192.168.33.10' （10060）
  **解决：** 
  * 1、修改MySQL配置文件/etc/my.conf
```
# vim /etc/my.conf
将行：
bind-address    = 127.0.0.1
修改为：
bind-address    = 0.0.0.0
```
  * 2、MySQL创建用户、授权
```
# mysql -u root -p
Enter password:
 mysql> create user 'root'@'%' identified by 'root';
远程登录的话，将"localhost"改为"%"，表示在任何一台电脑上都可以登录

 mysql>grant all on quant.* to 'root'@'%' identified by 'root';
 mysql>flush privileges;
 ```