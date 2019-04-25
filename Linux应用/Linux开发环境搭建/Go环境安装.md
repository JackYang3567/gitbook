
# Linux开发环境搭建

## Go的安装

* 1、下载

访问[下载地址](https://studygolang.com/dl)，找到Linux下的最新稳定版本。鼠标右击复制链接：https://studygolang.com/dl/golang/go1.12.4.linux-amd64.tar.gz  

* 2、安装

打开终端在命令运行：
```
cd /usr/local/
mkdir apps       #创建安装目录 
cd apps
wget https://studygolang.com/dl/golang/go1.12.4.linux-amd64.tar.gz
tar -xvf go1.12.4.linux-amd64.tar.gz

创建工作目录 ，这里以vagrant环境为例，非vagrant的linux可创建 /data/goworks/src
cd /vagrant_data/
mkdir goworks/src -p && cd goworks/src
```

* 3、设置环境变量

```
vim /etc/profile
```

添加:

```
export GOROOT=/usr/local/apps/go
export GOPATH=/vagrant_data/goworks
export PATH=$PATH:$GOROOT/bin
export PATH=$PATH:$GOPATH/bin
```
保存:  
esc  
:wq  

假定你想要安装Go的目录为 $GOROOT。  
工作开发目录： $GOPATH  

* 4、验证Go环境是否搭建成功

```
cd /vagrant_data/goworks/src
mkdir helloworld && cd helloworld
vim main.go

添加如下代码：
package main
 
import "fmt"
 
func main() {
    fmt.Println("Hello, World!")
}
```
然后执行

```
go run ./main.go
```

如果报： bash: go: command not found

```
export PATH=$PATH:/usr/local/apps/go/bin
```