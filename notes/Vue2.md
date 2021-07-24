## Vue2



### 修饰符

#### lazy



### number



### trim



### 组件

#### 父子组件间方法调用

1. 父组件访问子组件
   * $children
   * $refs
2. 子组件访问父组件
   * $parent

#### slot 插槽

对组件进行扩展, `<slot></slot>` 插槽占位, 插槽相对于组件对 DOM 更细分

使用:

> ​	/* 单个插槽使用 */
>
> ```vue
> <div id="app">
>     <cpn></cpn>
>     <cpn><span>我是插槽</span></cpn>
>     <cpn></cpn>
> </div>
> <template>
> 	<div>
>         <p>
>             
>     </p>
>     </div>
> 	/* slot 里可以设置默认值 */
> 	<slot><button>
>         按钮
>     </button></slot>
> </template>
> 
> /* 多个插槽使用==>具名插槽,给插槽具名 */
> <div id="app">
>     <cpn></cpn>
>     <cpn>
>         <span  v-slot="slot1">我是插槽</span>
>     	<button v-slot="slot2">
>             按钮
>         </button>
>     </cpn>
>     <cpn></cpn>
> </div>
> <template>
> 	<div>
>         <p>
>             
>     </p>
>     </div>
> 	/* slot 里可以设置默认值 */
> 	<slot name="slot1"></slot>
> 	<slot name="slot2"></slot>
> </template>
> 
> ```

作用域插槽: 一般组件本身的数据只能组件本身显示, 插槽可以将子组件的数据传入父组件或父级, 并对数据进行处理, 再通过插槽显示在子组件中

> ```vue
> <div id="app">
>     <cpn>
>     	<template slot-scope="slot">
>         	<span>{{ slot.data }}子组件数据</span>
>         </template>
>     </cpn>
> </div>
> 
> <template>
> 	<div>
>         <p>
>             子组件
>     </p>
>     </div>
> 	<slot :data="childdata" name="handler"></slot>
> </template>
> ```

### 模块化



### webpack

基于 node.js 的打包工具



> npm install save-dev vue-loader vue-template-compiler

#### Plugin 插件



### Vue-CLi

安装 Vue-CLi3

`npm install -g @vue-cli`

转到 Vue-CLi2

`npm install -g @vue/cli-init`

初始化 vue

`vue init webpack vuecli2test` vue-cli2

`vue create vuecli3test` vue-cli3

### vue router

安装

`npm install vue-router --save`

#### 修改 url 并且不刷新页面

```js
// 将 url 依次压入栈中, 可以用过 back() forward() go() 操作栈中的 url
history.pushState({}, "", 'home')
history.back() // 出栈一个 url , 浏览器中 url 变成栈中的 url
history.forward() // 进栈一个 url
history.go(Number) // 为正数时压栈,负数时进栈
// 替换掉当前 url
history.replaceState({}, "", 'home')
// 
loction.hash('home')
```

#### url 映射

vue 中 url 和组件的映射

通过 router-link 全局组件绑定 url

再用 router-view 显示组件内容

```vue
<template>
	<router-link to="/home">首页</router-link>
	<router-view></router-view>
</template>
// to="" 属性绑定 url
// tag="" 属性指定 router-link 渲染成什么标签,默认 a 标签
// replace 属性将设置成 history.replaceState() 模式
// active-class="" 将 router-link 的默认 class,同样也可以在 router 路由中添加 linkActiveClass 属性
```

### 守卫

全局守卫

`router.beforeEach(func) / router.aftereach`

路由独享守卫

组件守卫



### Vuex

安装

`npm install vuex --save`

创建

`const vuex = new vuex.store({})`

参数

* state
* getters
* mutations
* actions
* modules
* plugins
* strict: boolean

### axios

#### 请求方式

* axios(config)
* axios.request(config)
* axios.get(url[, config])
* axios.delet(url[, config])
* axios.head(url[, config])
* axios.post(url[,data[,config]])
* axios.put(url[,data[, config]])
* axios.patch(url[ data[, cofig]])







### 生态

* Quasar
* Element Plus
* Ant Design Vue
* Vuetify
* Nuxt 3
* vite
* VuePress/vitePress
* Volar 类型检查 + vue-tsc
