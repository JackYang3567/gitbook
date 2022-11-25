# 前端框架Vue编程

## 8、环境错误

### 8.1、环境错误解决vue-cli脚手架访问出现“Invalid Host header”
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

### 8.2、使用vuex的时候,出现this.$store为undefined
或 mapActions映射的方法 'loginAction' of undefined  

解决办法： this指向的解决方法
```
import { mapState,mapActions } from 'vuex'
let self =this;
export default {
	  methods: {
       ...mapActions('auth',[
        'loginAction'
      ]),
	    signin: function () { 
             ....
            //self.$store.dispatch('auth/loginAction')
            self.loginAction(res.data.data)
            .....
          },
       },
     created(){
		self = this;
  }
}

```

### 8.3、控制台报错 [WDS] Disconnected!