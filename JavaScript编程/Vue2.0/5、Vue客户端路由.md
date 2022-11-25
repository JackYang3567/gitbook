# 前端框架Vue编程

## 5、Vue客户端路由

### 5.1、 安装 
* 命令行安装:
  在终端（或命令行）运行安装，有如下两种方式：

  
#### 5.1.1、 NPM安装
```
npm install vue-router --save
```
#### 5.1.2、 Yarn安装
```
yarn add vue-router
```

### 5.2、 路由基本用法 
##### 1、 创建路由配置文件 
切换到项目根目录下 的src目录中，
```
$ mkdir router && cd router
$ touch index.js
```
编辑 src/router/index.js 加入如下内容：
````
// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)  // Vue.use() 明确地安装路由功能

// 1. 定义 (路由) 组件。  可以从其他文件 import 进来
import Home from '../views/Home.vue'
import C from '../views/C.vue'
import Agent from '../views/Agent.vue'
import Details from '../views/Details.vue'
import User from '../views/User.vue'

// 2. 定义路由  每个路由应该映射一个组件。

const router = new Router({
  mode: 'history', // 默认 hash 模式的URL中有#号
  base: process.env.BASE_URL,
  routes: [
    {
      path: '/',
      name: 'home', // 命名路由
      component: Home
    },
    {
      path: '/a',
      redirect: '/b'
      // 重定向:   从 /a 重定向到 /b
    },
    {
      path: '/c',
      component: C,
      // 别名:  /c 的别名是 /d，意味着，当用户访问 /d 时，URL 会保持为 /d，
      //但是路由匹配则为 /c，就像用户访问 /c 一样。
      alias: '/d'
    },
    {
      // 动态路径参数 以冒号开头
      path: '/user/:id',
      component: User
    },
    {
      path: '/about',
      name: 'about',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
    },
    {
      path: '/agent',
      name: 'agent',
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "about" */ '../views/Agent.vue'),
      children: [
        {
          // 嵌套路由
          // 当 /agent/agent 匹配成功，
          // Agent 会被渲染在 agent 的 <router-view> 中
          path: 'agent',
          component: Agent
        },
        {
          // 当  /agent/details 匹配成功
          // Details 会被渲染在 agent 的 <router-view> 中
          path: 'agent-details',
          component: Details
        }
      ]
    },
    {
      path: '/products',
      name: 'products',
      // route level code-splitting
      // this generates a separate chunk (products.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "products" */ '../views/Products.vue')
    },
    {
      path: '/users',
      name: 'users',
      // route level code-splitting
      // this generates a separate chunk (users.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "users" */ '../views/User.vue')
    },
    {
      path: '/signup',
      name: 'signup',
      // route level code-splitting
      // this generates a separate chunk (users.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "users" */ '../views/SignUp.vue')
    },
    {
      path: '/signin',
      name: 'signin',
      // route level code-splitting
      // this generates a separate chunk (users.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "users" */ '../views/SignIn.vue')
    },
    {
      path: '/forgot-password',
      name: 'forgot-password',
      // route level code-splitting
      // this generates a separate chunk (users.[hash].js) for this route
      // which is lazy-loaded when the route is visited.
      component: () => import(/* webpackChunkName: "users" */ '../views/ForgotPassword.vue')
    },
    {
      // 会匹配所有路径
      path: '*',
      name: 'not-found',
      component: () => import(/* webpackChunkName: "404" */ '../views/NotFound.vue')
    }
  ]
})

export default router
````

#####　2、 在根实例挂载路由　
在项目的src/main.js文件中挂载路由：
```
import Vue from 'vue'
import App from './App.vue'
import router from './router'   //必须
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,    //必须
  store,
  render: h => h(App)
}).$mount('#app')

```
##### 3、用 &lt;router-view/&gt;渲染路由匹配到的组件 
使用项目的src/App.vue文件布局(layout)页面：
```
<template>
  <div id="app">
    <Header />
    <DropdownMenu />
    <Sidebar />
    <Modal />
    <main >
       <router-view />    //必须
    </main>
    <FooterFloatBar />
    
    <Footer />
    <BackToTop bgColor="#f90808" svgFillColor="#2c3e50"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/layouts/Headerbar.vue'
import Footer from '@/layouts/Footerbar.vue'
import FooterFloatBar from '@/layouts/FooterFloatBar.vue'
import Modal from '@/layouts/Modal.vue'
import Sidebar from '@/layouts/Sidebar.vue'
import DropdownMenu from '@/layouts/DropdownMenu.vue'
import BackToTop from '@/layouts/BackToTop.vue'

export default {
  name: 'home',
  components: {
    Header,
    Footer,
    FooterFloatBar,
    Modal,
    Sidebar,
    BackToTop,
    DropdownMenu
  }
}
</script>
<style  src="../public/css/style.css" ></style>
<style scoped>
#app {
 
  }
</style>
```
##### 4、使用 router-link 组件来导航 
在模板中使用 router-link 组件来导航  
通过传入 `to` 属性指定链接  
&lt;router-link&gt; 默认会被渲染成一个 `<a>` 标签

#### 5.2.1、 HTML5 History 模式 
vue-router 默认使用 URL hash 来存储路径，也就是带有“#”号，
如: http://www.xxxx.com/#about。而且还会跳转。  
使用HTML5 History API ,无须跳转就能更新页面的URL.
```
const router = new Router({
  mode: 'history', // 默认 hash 模式的URL中有#号
  base: process.env.BASE_URL,
  routes: [ ....]
})

```


#### 5.2.2、 动态路由 
一个“路径参数”使用冒号 : 标记。当匹配到一个路由时，  
参数值会被设置到 this.$route.params，可以在每个组件内使用。
```
 routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
```
一个路由中设置多段“路径参数”，对应的值都会设置到 $route.params 中  

|模式	|匹配路径	|$route.params|
|: ------|: -----------|:----------------------------|
|/user/:username|	/user/evan|	{ username: 'evan' }|
|/user/:username/post/:post_id|	/user/evan/post/123	|{ username: 'evan', post_id: '123' }|

#### 5.2.3、 响应路由变化 
当使用路由参数时，例如从 /user/foo 导航到 /user/bar，原来的组件实例会被复用。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。不过，这也意味着组件的生命周期钩子不会再被调用。  
使用 beforeRouteUpdate 导航守卫：

```
<template>
  <div v-if="state==='loading'">
     Loading user ....
  </div>
  <div>
     <h1> User : {{userInfo.name}}</h1>
  </div>
</template>
<script>
  export default {
      data: () =>({
          state: 'loading',
          userInfo: undefined
      }),
      mounted(){
          this.init();
      },
      beforeRouteUpdate(to , from, next){
          this.state = 'loading';
          this.init();
          next();    
      },
      methods:{
          init() {
              fetch(`/api/user/${this.$route.params.userId}`)
              .then((res) => res.json())
              .then((data)=>{
                  this.userInfo = data;
              })
          }
      }
  }
</script>
```

#### 5.2.4、 路由参数作为组件属性传入 
在组件中使用 $route 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。

使用 props 将组件和路由解耦：

**取代与 $route 的耦合**
```
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User }
  ]
})
```

**通过 props 解耦**
```
const User = {
  props: ['id'],    
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',  
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})
```
这样你便可以在任何地方使用该组件，使得该组件更易于重用和测试。

##### 5.2.4.1、布尔模式
如果 props 被设置为 true，route.params 将会被设置为组件属性。

##### 5.2.4.2、对象模式
如果 props 是一个对象，它会被按原样设置为组件属性。当 props 是静态的时候有用。

```
const router = new VueRouter({
  routes: [
    { 
        path: '/promotion/from-newsletter', 
        component: Promotion, 
        props: { newsletterPopup: false } }
  ]
})
```

##### 5.2.4.3、函数模式
你可以创建一个函数返回 props。这样你便可以将参数转换成另一种类型，将静态值与基于路由的值结合等等。
```
const router = new VueRouter({
  routes: [
    { path: '/search', 
    component: SearchUser, 
    props: (route) => ({ query: route.query.q }) }
  ]
})
```
URL /search?q=vue 会将 {query: 'vue'} 作为属性传递给 SearchUser 组件。

请尽可能保持 props 函数为无状态的，因为它只会在路由发生变化时起作用。如果你需要状态来定义 props，请使用包装组件，这样 Vue 才可以对状态变化做出反应。

#### 5.2.5、嵌套路由 
在 VueRouter 的参数中使用 children 配置：
```
routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
```
#### 5.2.6、 重定向和别名 
##### 5.2.6.1、重定向
重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b：
```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})
```
重定向的目标也可以是一个命名的路由：
```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: { name: 'foo' }}
  ]
})
```
甚至是一个方法，动态返回重定向目标：
```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```
##### 5.2.6.2、别名
/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。
```
const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})
```
“别名”的功能让你可以自由地将 UI 结构映射到任意的 URL，而不是受限于配置的嵌套路由结构。

#### 5.2.7、链接导航 

#### 5.2.8、tag 属性 

#### 5.2.9、active-class 属性 

#### 5.2.10、原生事件 

#### 5.2.11、编程式导航 

### 5.3、路由高级用法 

#### 5.3.1、导航守卫 

#### 5.3.2、路由独享守卫 

#### 5.3.3、组件内部守卫 

#### 5.3.4、路由顺序 
同一个路径可以匹配多个路由，
此时，匹配的优先级就按照路由的定义顺序：谁先定义的，谁的优先级就最高。  
当使用通配符路由时，请确保路由的顺序是正确的，也就是说含有通配符的路由应该放在最后。


#### 5.3.5、404 页面 
含有通配符的路由应该放在最后。
```
 {
      // 会匹配所有路径
      path: '*',
      name: 'not-found',
      component: () => import(/* webpackChunkName: "404" */ '../views/NotFound.vue')
    }
```
#### 5.3.6、路由命名 
有时候，通过一个名称来标识一个路由显得更方便一些，特别是在链接一个路由，或者是执行一些跳转的时候。  
你可以在创建 Router 实例的时候，在 routes 配置中给某个路由设置名称。
```
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})
```

要链接到一个命名路由，可以给 router-link 的 to 属性传一个对象：
```
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```

这跟代码调用 router.push() 是一回事：

```
router.push({ name: 'user', params: { userId: 123 }})
```
这两种方式都会把路由导航到 /user/123 路径。
