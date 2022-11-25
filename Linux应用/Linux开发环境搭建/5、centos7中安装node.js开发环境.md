# 1、先安装环境依赖
```
 yum install libtool automake autoconf gcc-c++ openssl-devel
```
# 2、安装Git
```
 yum install git
```

# 3、安装nvm管理node版本
- 1)、安装前准备,打开下列文件，在其中加上映射

```
# 185.199.108.133  raw.githubusercontent.com

vim /etc/hosts
```
- 2)、到 https://github.com/nvm-sh/nvm 找最新版nvm

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```
或
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```
- 3)、下载完成后加入系统环境

```
source   ~/.bashrc
```

- 4)、接着就是查看需要的node版本，查看可用的node版本

```
nvm ls-remote
```
- 5)、安装需要的node版本

```
 nvm install  v9.11.0
```
或者也可以支架安装node的最新稳定版. 通过

```
nvm install stable
```

- 6)、查看我们机器上面安装了那些node版本 执行命令

```
nvm list
```

- 7)、根据版本号切换node版本 执行 
 
```
nvm use v9.5.0
```

- 8)、设置默认的node版本 执行 
```
 nvm alias default v9.5.0
```

- 9)、查看当前使用的版本
执行 
```
nvm current
```
或  
```
 nvm ls
```