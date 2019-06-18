# MongoDB 数据库操作
## 1、查看 MongoDB 版本号的三种方法
### 1.1、使用 mongo 或者 mongod 命令来查看版本号
```
mongo --version
mongod --version
```
### 1.2、在 shell 里使用查询函数来查询
```
db.version()
```
### 1.3、使用命令登入系统时，返回版本信息
```
/usr/local/mongodb/bin/mongo --version
```

## 2、Win10环境下MongoDB 4.0版本
### 2.1、MongoDB3.6.5版本下载[https://www.mongodb.com/download-center/community](https://www.mongodb.com/download-center/community)
```
https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-2008plus-ssl-4.0.10-signed.msi
```
### 2.2、创建一个无空格的英文安装目录
```
e:
mkdir mongodb
```
### 2.3、点击下载好的安装程序安装
>选择自定义安装，将安装目录指向 上一步创建的目录》
>注意，一定不要勾选最后一步的左下角的 install MongoDB compass 
#### 2.3.1、安装过程中报错：  

Service 'MongoDB Server' (MongoDB) failed to start,
Verify that you have sufficient privileges to start system services.
#### 2.3.2、报错解决方法  
```
Ctrl + Win,
services.msc
```
打开(services.msc)服务界面,找到MongoDB Server，右键->属性->登录，登录身份选择本地系统账户(L)。
设置完成后自己手动启动MongoDB Server服务，或者在刚刚正在安装的MongoDB弹窗提示点击Retry重试，安装程序会帮你启动MongoDB Server服务。