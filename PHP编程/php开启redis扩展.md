# 1、php开启redis扩展

## 1.1、安装redis
git下载地址https://github.com/MSOpenTech/redis/releases

## 1.2、测试redis

windows 运行（快捷键：windows键+R键），输入【cmd】命令，进入DOC操作系统窗口；

进入redis安装目录使用命令

## 1.2.1、开启redis守护进程(进入redis安装目录)
```
redis-server.exe redis-windows-conf
```
## 1.2.2、进入redis客户端(进入redis安装目录)
```
redis-cli.exe 
```

## 1.3、 安装php的redis扩展

下载地址https://pecl.php.net/package/redis 
根据phpinfo()信息选择适当的redis扩展压缩包

## 1.4、将redis扩展包的php_redis.dll和php_redis.pdb两个文件放在ext文件夹  
## 1.5、修改php.ini文件
```
extension=php_redis.dll
```
## 1.6、验证是否开启redis扩展
查看phpinfo()信息，搜索redis

## 1.7、php连接并测试redis数据库(记得开启redis服务)
新建test.php
```
<?php
 $redis = new Redis();
 $redis->connect('127.0.0.1',6379); 
 $redis->set('name','klc');
 echo $redis->get('name');
?>
```
访问test.php,输出klc,测试通过