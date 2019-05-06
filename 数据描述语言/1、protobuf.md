# 数据描述语言
## 一、protobuf
### 1.1、protobuf定义

> protobuf是Protocol Buffers的简称, 是Google公司开发的一种数据描述语言，类似于XML能够将结构化数据序列化，用于各种结构化信息存储和交换  

### 1.2、protobuf的作用
> 用于各种结构化信息存储和交换

### 1.3、protobuf的使用
#### 1.3.1、在node.js中使用protobuf

##### 1.3.1.1、安装protobuf.js
```
# npm install protobufjs [--save --save-prefix=~]

```
##### 1.3.1.2、导入protobuf.js
```
var protobuf = require("protobufjs");
```
##### 1.3.1.3、在.proto 文件之中定义数据结构
> 定义一些数据和结构放在一个 .proto 文件之中。每一个protocol buffer 信息都是一小段结构，包含了一些字段。