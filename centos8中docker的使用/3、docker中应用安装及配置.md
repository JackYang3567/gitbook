
#  docker中应用安装及配置

## 1、docker下gitlab安装配置使用
### 1.1、先搜索一下可用的gitlab镜像
```
$ docker search gitlab 
 
NAME                                         DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
gitlab/gitlab-ce                             GitLab Community Edition docker image based …   3568                 [OK]
gitlab/gitlab-runner                         GitLab CI Multi Runner used to fetch and run…   776                  [OK]
gitlab/gitlab-ee                             GitLab Enterprise Edition docker image based…   316
....

```
### 1.2、docker pull gitlab/gitlab-ce 拉取最新稳定版本
```
$ docker pull gitlab/gitlab-ce
```
### 1.3、运行gitlab镜像
```
$ docker run -d  -p 4443:443 -p 8880:80 -p 222:22 --name gitlab --restart always -v /home/gitlab/config:/etc/gitlab -v /home/gitlab/logs:/var/log/gitlab -v /home/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce

# -d：后台运行
# -p：将容器内部端口向外映射
# --name：命名容器名称
# -v：将容器内数据文件夹或者日志、配置等文件夹挂载到宿主机指定目录
运行成功后出现一串字符串
ee33b641d3d3eb8a0c40f575862c76ba804364c43474d4d08615ad5ef88022d0

运行成功
```
### 1.4、配置
 >按上面的方式，gitlab容器运行没问题，但在gitlab上创建项目的时候，生成项目的URL访问地址是按容器的hostname来生成的，也就是容器的id。作为gitlab服务器，我们需要一个固定的URL访问地址，于是需要配置gitlab.rb（宿主机路径：/home/gitlab/config/gitlab.rb）。

```
# gitlab.rb文件内容默认全是注释
$ vim /home/gitlab/config/gitlab.rb
# 配置http协议所使用的访问地址,不加端口号默认为8880
external_url 'http://192.168.33.10:8880'

# 配置ssh协议所使用的访问地址和端口
gitlab_rails['gitlab_ssh_host'] = '192.168.33.10'
gitlab_rails['gitlab_shell_ssh_port'] = 222 # 此端口是run时22端口映射的222端口
:wq #保存配置文件并退出
修改gitlab.rb文件

# 重启gitlab容器
$ docker restart gitlab
```
>此时项目的仓库地址就变了。如果ssh端口地址不是默认的22，就会加上ssh:// 协议头
打开浏览器输入ip地址(因为我的gitlab端口为8880，所以浏览器url不用输入端口号，如果端口号不是80，则打开为：ip:端口号)
### 1.5、访问
>此时访问ip:8888无法访问，安全组也已经打开8880端口。发现是由于改了external_url 'http://192.168.33.110:8880’的端口为8880 后，gitlab容器的内部端口也被改为了8880，而我们在运行gitlab的时候，映射的是8880:80端口，故此时需要先stop容器，rm容器，然后重新以8880:8880的映射方式运行。
```
# docker stop gitlab
gitlab
[root@nb001 data]# docker rm gitlab
gitlab
[root@nb001 data]# docker run --name gitlab --restart always -p 4443:4443 -p 8880:8880 -p 222:22 -v /data/gitlab/config:/etc/gitlab -v /data/gitlab/logs:/var/log/gitlab -v /data/gitlab/data:/var/opt/gitlab -d gitlab/gitlab-ce

d2a108fd54f0876730208dd1f1d0cf0416bbaea759c59576e23858d9f0f9fcfd
```

## 2、docker下nginx安装配置使用


## 3、docker下postgesql安装配置使用


## 4、docker下mysql安装配置使用


## 5、docker下node.js安装配置使用


## 6、docker下redis安装配置使用


## 7、docker下rabbitmq安装配置使用


## 8、docker下jenkins安装配置使用


## 9、docker下MongoDB安装配置使用