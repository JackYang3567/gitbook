# 1、Go 安装包下载
## 1）、Go Windows安装包下载
[Go 安装包下载](https://studygolang.com/dl)
[go1.12.windows-amd64.msi (117MB)](https://studygolang.com/dl/golang/go1.12.windows-amd64.msi)

## 2）、Go Windows 版安装
> 运行安装程序，安装到目录： E:\Go
```
go version   #检查版本

go version go1.12 windows/amd64 #显示所安装的版本
```
## 3）、配置环境变量（path，GOPATH,GOROOT）
  - 用户变量里配置path 
     > 添加 E:\Go\bin(安装目录\bin)
  - 系统变量里配置GOPATH和GOROOT
     > 添加GOPATH ：  E:\Go (安装目录)
     > 添加GOROOT :  D:\works\go_pro (工作目录)

 ---
# 2、beego
beego 是一个类似 Python 的 Tornado 框架，采用了 RESTFul 的设计思路，使用 Go 语言编写的一个极轻量级、高可伸缩性和高性能的 Web 应用框架。

项目链接：[https://github.com/astaxie/beego](https://github.com/astaxie/beego)

## 一、beego快速入门
建立一个 beego 的项目，然后运行起来。至少有6个步骤

1. bee 工具新建项目
2. 路由设置
3. controller 运行机制
4. model 逻辑
5. view 渲染
6. 静态文件处理

---
# 3、martini
一款快速构建模块化的 Web 应用的 Web 框架。

项目链接：[https://github.com/go-martini/martini](https://github.com/go-martini/martini)
