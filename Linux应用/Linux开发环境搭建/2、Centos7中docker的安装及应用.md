
# Linux开发环境搭建
## 2、Centos7中docker的安装及应用
### 2.0、docker官方镜像搜索 
  https://hub.docker.com/ 

  ```
  MyDocker!3567.
  ```
### 2.1、Centos7中docker的安装

- 1、Docker 要求 CentOS 系统的内核版本高于 3.10 ，查看本页面的前提条件来验证你的CentOS 版本是否支持 Docker 。

  通过 uname -r 命令查看你当前的内核版本
   
```
# uname -r
```

- 2、确保 yum 包更新到最新。

```
# yum update
```

- 3、安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
  
```
  # yum install -y yum-utils device-mapper-persistent-data lvm2
```

 - 4、设置yum源

```
  # yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
 
- 5、可以查看所有仓库中所有docker版本，并选择特定版本安装

```
  # yum list docker-ce --showduplicates | sort -r
```

- 6、安装docker

```
# sudo yum install docker -y
或
# sudo yum install docker-ce
```

- 7、启动并加入开机启动

```
# systemctl start docker
# systemctl enable docker
```

- 8、验证安装是否成功(有client和service两部分表示docker安装启动都成功了)

```
# docker version
```

### 2.2、Centos7中docker的应用

- 1、查看已经下载的镜像

```
  docker images
  REPOSITORY   TAG       IMAGE ID   CREATED   SIZE    
```
- 2、搜索下载镜像

```
  # docker search nginx　　　　　　　　　 #搜索镜像
  # docker pull nginx                    #下载镜像
```

- 3、再查看已经下载的镜像

``` 
  # docker images
  REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
  nginx        latest    88736fe82739   12 days ago   142MB
```
- 4、导出镜像

```
 先 到目录tmp下看看
 # cd /tmp/
 # ls
 systemd-private-fc2a4caa32b2422c89fd65517026ecfd-chronyd.service-3k8w2s  vboxguest-Module.symvers

 # docker save nginx >/tmp/nginx.tar.gz
 # ls
 nginx.tar.gz  systemd-private-fc2a4caa32b2422c89fd65517026ecfd-chronyd.service-3k8w2s  vboxguest-Module.symvers
```

- 5、删除镜像

```
 先查看一下当前镜像
 # docker images
  REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
  nginx        latest    88736fe82739   12 days ago   142MB

 # docker rmi -f nginx

 # docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

- 6、导入镜像

```
 # docker load </tmp/nginx.tar.gz

 # docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    88736fe82739   12 days ago   142MB
```

- 7、默认配置文件

```
 # vim /usr/lib/systemd/system/docker.service
```

### 2.3、docker 运维命令
 - 1、 查看docker工作目录
```
 # sudo docker info | grep "Docker Root Dir"
 Docker Root Dir: /var/lib/docker
```

- 2、查看docker磁盘占用总体情况
```
 # du -hs /var/lib/docker/ 
 395M    /var/lib/docker/
```

- 3、查看Docker的磁盘使用具体情况

```
  # docker system df
  TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
  Images          3         2         380.1MB   141.8MB (37%)
  Containers      3         0         15B       15B (100%)
  Local Volumes   0         0         0B        0B
  Build Cache     0         0         0B        0B
```

- 4、删除 无用的容器和镜像

 * 删除异常停止的容器

  ```
  # docker rm `docker ps -a | grep Exited | awk '{print $1}'` 
  ```

 * 删除名称或标签为none的镜像

  ```
  # docker rmi -f  `docker images | grep '<none>' | awk '{print $3}'` 
  
  ```

