# Linux开发环境搭建
## 1、MySQL的安装

### 1.1、查看是否有安装过mysql
```
 # rpm -qa | grep mysql
```
### 1.2、配置Mysql 8.0安装源
```
# rpm -Uvh https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
```
### 1.3、安装Mysql 8.0
```
# yum --enablerepo=mysql80-community install mysql-community-server
```
### 1.4、启动mysql服务
```
# service mysqld start
Redirecting to /bin/systemctl start  mysqld.service
```
### 1.5、查看mysql服务运行状态
```
# service mysqld status
```
### 1.6、查看root临时密码
 - 安装完mysql之后，会生成一个临时的密码让root用户登录
```
grep "A temporary password" /var/log/mysqld.log
il9fyqsDie/Z
```
 
### 1.7、更改临时密码
 
```
 # mysql -uroot -p
 Enter password: 输入临时密码

 mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
 ERROR 1819 (HY000): Your password does not satisfy the current policy requirements

  mysql> SHOW VARIABLES LIKE 'validate_password.%';
  ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.


  mysql> select user();
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.
mysql> ALTER USER USER() IDENTIFIED BY '123456';
SET PASSWORD=PASSWORD('123456');
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
mysql>set global validate_password_policy=0;
Query OK, 0 rows affected (0.00 sec)
mysql> set global validate_password_mixed_case_count=2;
Query OK, 0 rows affected (0.02 sec)
```
### 1.8、添加参数
```
#添加密码验证插件
plugin-load-add=validate_password.so

#服务器在启动时加载插件，并防止在服务器运行时删除插件
validate-password=FORCE_PLUS_PERMANENT

```
### 1.9、重启mysql
```
# systemctl restart mysqld

 mysql>set global validate_password_policy=0;
 Query OK, 0 rows affected (0.03 sec)
 mysql>set global validate_password_length=1;
 Query OK, 0 rows affected (0.03 sec)
SHOW VARIABLES LIKE 'validate_password%';
 mysql>alter user 'root'@'localhost' identified by '123456';
```
### 1.2、开机启动设置
```
#systemctl enable mysqld
#systemctl daemon-reload
```
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
### 3.1、ERROR 1045 
 重置密码解决MySQL for Linux错误  
 ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)  

一般这个错误是由密码错误引起，解决的办法自然就是重置密码。  

假设我们使用的是root账户。  
1.重置密码的第一步就是跳过MySQL的密码认证过程，方法如下：  
```

#vim /etc/my.cnf(注：windows下修改的是my.ini)
```
在文档内搜索mysqld定位到[mysqld]文本段：
/mysqld(在vim编辑状态下直接输入该命令可搜索文本内容)

在[mysqld]后面任意一行添加“skip-grant-tables”用来跳过密码验证的过程，如下图所示：

```
explicit_defaults_for_timestamp=true
skip-grant-tables
```

保存文档并退出：
```
#:wq
```
2.接下来我们需要重启MySQL：
```
service mysqld restart
```
3.重启之后输入#mysql即可进入mysql。

```
#mysql
mysql>
```
4.接下来就是用sql来修改root的密码
```
mysql> use mysql;
mysql> update  mysql.user set authentication_string=PASSWORD("你的新密码") where user="root";

 update mysql.user set authentication_string=PASSWORD('root') where user='root';
 
mysql> flush privileges;
mysql> quit
```
到这里root账户就已经重置成新的密码了。



5.编辑my.cnf,去掉刚才添加的内容，然后重启MySQL。大功告成！
```
#explicit_defaults_for_timestamp=true
#skip-grant-tables
```