# CentOS7 (linux)下go开发环境搭建

## 1.下载安装
- go 安装版本下载网址：[https://golang.google.cn/dl/](go 安装版本下载网址：https://golang.google.cn/dl/)
- 复制Featured downloads 中Linux版本的go安装包链接
- 下载
> wget https://dl.google.com/go/go1.12.linux-amd64.tar.gz
```
# cd /usr/local
# mkdir apps
# cd apps
# mkdir code
# cd code
# mkdir goproject
```
> 解压go1.12.linux-amd64.tar.gz到/usr/local/apps下
> tar -zxvf go1.12.linux-amd64.tar.gz -C /usr/local/apps
> 进入安装目录：cd /usr/local/apps
> 查看go版本：go/bin/go version

## 2.配置环境变量
```
vim /etc/profile #将下列几行代码复制进去
   export GOROOT=/usr/local/apps/go
   export GOPATH=/usr/local/apps/code/goproject
   export PATH=$PATH:$GOROOT/bin

source /etc/profile
