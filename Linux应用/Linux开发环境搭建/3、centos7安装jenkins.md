
# Linux开发环境搭建
## 3、centos7安装jenkins

 - 1、确认已安装JDK
 - 2、安装jenkins
   添加Jenkins库到yum库，Jenkins将从这里下载安装。

 ```
 # wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
 # rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
  
 # yum install jenkins
 ```
  配置jenkis的端口
 ```
 vi /etc/sysconfig/jenkins
 ```
 找到修改端口号： JENKINS_PORT="9090"  此端口不冲突可以不修改 

 ```
 # firewall-cmd  --query-port=9090/tcp                            $查看端口是否打开 开放端口
 # firewall-cmd --zone=public --add-port=9090/tcp --permanent   $开放端口9090
 # firewall-cmd --reload                                        $重启防火墙
 ```
 - 3、启动jenkins

```
# chkconfig jenkins on              $设置开机启动
# service jenkins start/stop/restart 或
# systemctl start jenkins 
```
 - 4、打开jenkins 

在浏览器中访问 
首次进入会要求输入初始密码如下图， 
初始密码在：/var/lib/jenkins/secrets/initialAdminPassword 
 ```
  # cat /var/lib/jenkins/secrets/initialAdminPassword
 ```
选择“Install suggested plugins”安装默认的插件，下面Jenkins就会自己去下载相关的插件进行安装。 

