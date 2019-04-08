# 前端框架Vue编程

## 六、Vuex状态管理

Vuex的使用步骤：

### 第一步 ：安装 
 * 命令行安装:
  在终端（或命令行）运行安装，有如下两种方式：

#### NPM
```
npm install vuex --save
```
#### Yarn
```
yarn add vuex
```

### 第二步：组织store文件结构
确保当前在项目目录下。
 * 1）、创建store文件结构
 ```
 cd src
 mkdir store && cd store
 touch index.js
 ```

 * 2）、导入Vuex插件。
 编辑 src/store/indes.js文件，包含如下内容：

 ```
    import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

 ```
 * 3）、创建一个 store。

  在src/store/indes.js文件，添加如下代码：
 ```
    const store = new Vuex.Store({
        state: {
            count: 0
        },
        mutations: {
            increment (state) {
                state.count++
            }
        }
    })
 ```
### 第三步：应用store
  * 1）、在入口文件main.js中导入组织好的store文件
```
    import Vue from 'vue'
    import App from './App.vue'
    import router from './router'
    import store from './store'

    Vue.config.productionTip = false

    new Vue({
        router,
        store,
        render: h => h(App)
    }).$mount('#app')

```

### 概念 


### State 及其辅助函数 


### State 辅助函数 

### Getter 

### Getter 辅助函数 

### Mutation 

### Mutation 辅助函数 

### Mutation 必须是同步函数

### Action 

### Action 辅助函数 

### 参数解构 

### Promise 与 Action 

### Module 

### 项目文件结构 

### 带命名空间的模块 

### 严格模式

### 表单处理
