# Vue 
~~~
Vue.js  https://cn.vuejs.org
~~~
## 使用Vue CLI 脚手架创建一个vue项目、
~~~
vue create vue-demo
cd vue-demo
npm run servegit 
~~~

## vue文件夹的介绍

### build
保存一些webpack的初始化配置

### config
保存项目初始化的配置

### node_modules
是npm加载的项目依赖的模块

### src
是我们需要的开发的模块

### assets
用来放置图片等资源的

### components
用来放置组件文件

### app.vue
是项目的入口,相当于一个组件

### main.js
是项目的核心文件

### static
用来放置静态资源目录

### index.html
是首页入口文件

### package.json
是项目配置文件，里面写有启动打包、版本等命令


## vue的一些介绍

### template标签
template是html5的一个新元素，主要用于保存客户端中的内容，表现为浏览器解析该内容但不渲染出来，可以将一个模板视为正在被存储以供随后在文档中使用的一个内容片段。

### 单文件组件
vue的单文件相当于一个页面中的组件，包含了关于该组件的html-css-js文件集合，这么做的目的有利于项目的管理和整合，官方说法是有构建步骤。
在<template/>标签下只能有一个子节点元素，如果写多个如<div/>这样的标签则会报错。

### .vue文件可包含html-css-js，webpack自动打包成三个文件
在.vue文件中，dom结构可以写在<template/>标签下，而针对该dom结构的样式文件则作为<template/>标签的兄弟元素<style/>存在，同样的控制该dom结构的脚本程序写在另一个兄弟元素<script/>之中，这样一来，每个组件自己对应的结构样式都在同一个文件之中，便不会与其它的组件搞混了。

### style标签
<style/>标签包含scoped和module属性，分别表示css作用域和css模块，一般会写上scoped属性，表示样式仅对当前组件以及其子组件的模板部分生效

### script标签中的export default
<script/>标签下第一行代码是export default {……}，这是ES6新增的模块部分的语法，采用模块的方式，每个文件都自成一个模块，采用export和import来暴露和引用接口。一个文件或模块中，export 和 import可以有多个，但export default只能有一个，使用该命令之后别的模块引用时就可以不需要知道所要加载的模块变量名

### export default
export default下可以写包括变量和方法，对象等，只要是想作为开放的接口都可以写，在.vue文件中一般写上data() {}以及method等,data指的是在该组件中定义的模板数据，而如果你对<template/>中的元素绑定了点击方法，如<button @click="login">



## vue打包

npm run build
npm install -g serve
serve dist
访问: http://localhost:5000

~~~
父页引入子页面组件
1. import 引入子组件
2. 在components声明成标签
   components: {
        HelloWorld
     }
3. <HelloWorld msg="Hello Vue!"/>  使用: 则动态传值

子组件接受
1. props声明接受
export default {
    props: {
        msg: String
    }
}
2. 在使用 
~~~



## 回车监听事件

~~~
@keyup.enter
enter键up触发的方法
<input v-on:keyup.enter="submit">

<input @keyup.enter="submit">


注意！！！如果用了封装组件的话，比如element，这个时候使用按键修饰符需要加上.native

比如：

<el-input v-model="account" placeholder="请输入账号" @keyup.enter.native="search()"></el-input>

~~~



## 鼠标移动事件

~~~
onmouseenter
onmouseleave

onmouseover
onmouseout

当有两个div时   一个大的嵌套一个小的
  ------------------------------
  |      -------------------    |
  |      |                 |    |
  |      |                 |    |
  |      |                 |    |
  |      -------------------    |
  |                             |
  -------------------------------

当鼠标进入大的div时，onmouseenter，onmouseover 都会触发
当鼠标从大的div进入到小的div时，onmouseout 触发
当鼠标从小的div退出到大的div时，onmouseover 触发
只有当鼠标离开大的div时，onmouseleave 才触发
~~~



## 计算属性 computed

~~~
计算属性 可以做计算值
computed:{
  size(){
    // 数组的操作
    return this.arr.reduce((preTotal,label) => preTotal + (label.status?1:0), 0)
  }
}

定义一个数组
arr: Array
arr: [
  label:{
    title: 'abc',
    status: ture
    }
]
直接取 {{size}}

筛选 arr数组中label为可用的,在放到原来的数组中
this.arr = this.arr.filter(label => label.status)
arr

~~~



## 缓存 localStorage

~~~
存值存的是文本字符串,使用JSON转成想要的格式
JSON.parse(window.localStorage.getItem('key') || '[]')
从localStorage取值 
window.localStorage.getItem('key')
~~~

## 监事  watch

~~~
data(){
  arr: []
}
watch: { // 监视
  arr: {
    deep: true, //深度监视
    handler: function (newValue, oldValue) {
      // 最新的值存储在localStorage中
      window.localStorage.setItem('key', JSON.stringify(newValue))
    }
  }
}
~~~

# 自定义事件
~~~
第一种写法:
父组件:
<Todo @todo="todo"/>
子组件:
this.$emit('todo') // 触发监听

父组件 @todo="todo" 传递函数,绑定监听
子组件 this.$emit('todo') 触发事件
this.$emit('函数名称', value) value可以是传递的值


第二种写法:
父组件:
<Todo ref="son"/>
mounted(){ // 执行异步代码
  this.$on('函数名称', 回调函数)
  this.$refs.son.$on('todo', this.todo)
}

methods:{
  todo (){

  }
}
~~~

~~~
使用 VueResource插件

引入  import VueResource from 'vue-resource'
声明使用插件  Vue.use(VueResource)
 this.$http.get(url).then(
   response => {
     // 成功
   },
   response => {
     // 失败
   }
 )

 使用axios
 直接引入 import axios from 'axios'
  axios.get(url).then(
    response => {
     // 成功
   }
  ).catch(error =>{
    // 失败
  })
~~~


~~~
同级组件  兄弟组件传值   发布/订阅


发布消息   import PubSub from 'pubsub-js'
          PubSub.publish('消息名称', 消息内容)

订阅消息   import PubSub from 'pubsub-js'
          PubSub.subscribe('search', (msg, data) =>{

          })
~~~


~~~
vue中数组的操作

变异方法
push() 从数组末尾添加值。
pop() 删除并返回数组的最后一个元素。
shift() 把数组的第一个元素从其中删除，并返回第一个元素的值。
unshift() 向数组的开头添加一个或更多元素，并返回新的长度。
splice() 向/从数组中添加/删除项目，然后返回被删除的项目。
sort() 对数组的元素进行排序。
reverse() 用于颠倒数组中元素的顺序。


替换数组
filter() 创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。
concat() 用于连接两个或多个数组。
slice() 可从已有的数组中返回选定的元素。


过滤数组使用filter

从数组中取出一一对应的值  map
注意  {} 表示函数体
      ({})  表示对象
const arr = []
arr = array.map(item => ({
  url: item.htmlUrl
}))
~~~

~~~
异步执行方法，去得结果
方法() {
      return new Promise((resolve, reject) => {
        api(参数)
          .then(res => {
            resolve(res.data)
          })
          .catch(e => {
            reject(e)
          })
      })
    }
    
使用：
方法().then(res =>{
   res
})
~~~
