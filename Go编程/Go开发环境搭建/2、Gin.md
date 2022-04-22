# 2、Gin

## 2.0、介绍 {#安装}

Gin 是一个用 Go \(Golang\) 编写的 web 框架。是一个拥有更好性能的 API 框架,，速度提高了近 40 倍。

## 2.1、安装Gin {#安装}

要安装 Gin 软件包，需要先安装 Go 并设置 Go 工作区。

### 1.下载并安装 gin：

#### 1.1、先到Go 工作区 D:\vswork\go-work\src

```
$ go get -u github.com/gin-gonic/gin
```

#### 1.2、创建项目,使用vscode打开文件夹D:\vswork\go-work\src

```
$ mkdir ginpro
$ cd ginpro
```

#### 1.3、创建文件main.go

```
package main

import (
    "github.com/gin-gonic/gin"
    _"net/http"
)

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // 监听并在 0.0.0.0:8080 上启动服务
}
```

#### 1.4、运行go mod init ginpro 初始化项目

```
$ go mod init ginpro

    go: creating new go.mod: module ginpro
    go: to add module requirements and sums:
        go mod tidy

$ go mod tidy
```

#### 1.5、go run main.go 运行项目

```
$ go run main.go
```

#### 1.6、在浏览器中查看

```
http://localhost:8080/ping


{"message":"pong"}
```

#### 

## 2.2、Gin集成swagger {#安装}

## 2.3、安装 {#安装}

## 2.4、安装 {#安装}

## 2.5、安装 {#安装}

## 2.6、安装 {#安装}

## 2.7、安装 {#安装}

## 2.8、安装 {#安装}



