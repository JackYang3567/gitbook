# 前端框架Vue编程

## 七、环境错误

### 7.1、环境错误解决vue-cli脚手架访问出现“Invalid Host header”
在项目根目录下创建文件vue.config.js，然后填入如下内容：
```
module.exports = {
    devServer: {
        host: '0.0.0.0',
        hot: true,
        disableHostCheck: true,
    },
}
```