
# Linux开发环境搭建
## 4、centos7中jenkins的安装及应用
### 4.1、centos7中jenkins的安装

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

### 4.2、centos7中jenkins的应用
#### 4.2.1、基于vue的前端项目、GitHub的代码仓库用 jenkins 实现自动部署
https://www.jb51.net/article/159497.htm
本文基于 vue 的前端项目、 GitHub 的代码仓库，简述在 CentOS7 上利用 jenkins 实现自动部署。
 - 一、安装插件 NodeJS
 Dashboard->系统管理-> 插件管理 
 可选插件-> 搜索中输入 NodeJS，勾选 NodeJS，点击 Install without restart 安装
 - 二、配置 NodeJS 插件
 Dashboard->系统管理-> 全局工具配置
 NodeJS 节点下，点击 NodeJS installations
 填写 Name，勾选 Install automatically，选择 Version，最后点击 Save
 - 三、发布配置
Jenkins -> New Item
填写 job name，选择 Freestyle project，点击 OK
点击 Configure 配置 job 构建参数
General 配置，填写 Project name，Description
Source Code Management，选择 Git，填写 Repository URL，如果是私有仓库，还需要填写 Credentials( 点击 Add 添加)