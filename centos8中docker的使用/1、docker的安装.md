# centos8中docker的安装
## 1、docker安装步骤
### 1.1、安装docker-ce
```
# yum -y install docker-ce 
```
### 1.2、启动docker
```
# systemctl start docker
```

### 1.3、检查docker安装是否成功
```
# docker version
```

### 1.4、查看版本信息
```
# docker info
```

## 2、docker配置
### 2.1、阿里云镜像加速
```
登录阿里云，进入https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors
复制加速器地址：https://a8xzcgqo.mirror.aliyuncs.com
```
#### 2.1.1、修改daemon配置文件/etc/docker/daemon.json ，将复制的地址按照如下格式写入文件，若存在多行，使用逗号分隔。

```
# vi /etc/docker/daemon.json
将下列内容编辑到打开的文件中

{
  "registry-mirrors": ["https://a8xzcgqo.mirror.aliyuncs.com"]
}
```

#### 2.1.2、重启服务
```
# systemctl daemon-reload
# systemctl restart docker
```