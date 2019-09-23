# 什么是vuex

### 官方解释

>  Vuex是一个专门为Vue.js应用程序开的**<font color=red>状态管理模式</font>**。
>
> 它采用集中式存储管理应用的所有组件的状态并以响应的规则保证以一种可预测的方式发生变化

###  Vuex是vue框架中状态管理。

>  什么是“状态管理模式”？
>
> 把组件的共享状态抽取出来，以一个全局单例模式管理。在这种模式下，我们的组件树构成了一个巨大的“视图”，不管在树的哪个位置，任何组件都能获取状态或者触发行为！这就是“状态管理模式”。

​																																			[转自链接](http://www.imooc.com/article/284778)

* 理解：vuex是当前应用的数据仓库，用来保存所有组件的共享数据。



### 应用场景

1. 多个视图依赖于同一个状态（读取数据）
   * 多组件的数据共享，例如用户信息在不同的页面都能拿到
2. 来自不同视图的行为需要改变同一个状态（更改数据）
   * 在不同的组件中需要改变同一个数据状态

### Vuex的属性

1. State

   	* 数据存放的地方
      	* state里面存放的数据是响应式的，Vue组件从store中读取数据，若是store中的数据发生改变，依赖这个数据的组件也会发生更新

2. Getter（对state属性的派生，如同vue实例中computed对data中属性的派生）

   	* 用来获取数据，getters 可以对State进行计算操作，它就是Store的计算属性
      	* 虽然在组件内也可以做计算属性，但是getters 可以在多组件之间复用

3. Mutation

   ​	用来修改数据

4. Action

   ​	用来提交Mutation，

### 安装Vuex

1. 安装vuex包：npm install vuex

2. 创建vuex实例：new Vuex.store()

3. main.js中将vuex实例挂载到vue对象上

   注：vue3.0帮我们创建好了一个store.js的文件夹，并且也挂载到了main.js的vue实例中

   ```vue
   import Vue from 'vue'
   import Vuex from 'vuex'
   
   Vue.use(Vuex)
   
   export default new Vuex.Store({
     state: {
   
     },
     mutations: {
   
     },
     actions: {
   
     }
   })
   ```

   ```vue
   import Vue from 'vue'
   import App from './App.vue'
   import router from './router'
   import store from './store'
   
   Vue.config.productionTip = false
   
   new Vue({
     router,
     store,/*vuex*/
     render: h => h(App)
   }).$mount('#app')
   ```



### 实现点击按钮自增

1. store.js 添加

   ```vue
   export default new Vuex.Store({
     state: {
       count: 0,
     },
     /*修改数据*/
     mutations: {
       countIncrease(state) {
         state.count++;
       },
     },
     actions: {}
   })
   ```

2. 在组件中拿到state中count的值

   ```vue
   this.$store.state.count
   ```

   ```html
   <h1>count:{{count}}</h1>
   <button @click="add">点击自增</button>
   ```

   ```vue
   computed: {
         /*将vuex中state的count值显示到HTML上*/
         count() {
           return this.$store.state.count;
         }
       },
       methods:{
         /*每次点击，提交Mutation中的countIncrease方法修改vuex中state中的count值*/
         add(){
           this.$store.commit("countIncrease");
         }
       },
   ```

### 在其他组件中给vuex中的数据赋值

1. store.js

   ```vue
   state: {
     name: ''
   },
   /*修改数据*/
   mutations: {
     /*val接受其它组件传递过来的参数*/
     nameFuZhi(state, val) {
       state.name = val;
     }
   },
   ```

2. 其他组件指定值

   ```vue
   fuzhi() {
     this.$store.commit("nameFuZhi","wade");
   }
   ```



### vuex四大金刚

​			[四大金刚](https://www.cnblogs.com/m2maomao/p/9954640.html)

### vuex辅助方法

​			[辅助方法](https://www.cnblogs.com/Free-Thinker/p/10718474.html)

​			注：将store中的四大金刚映射到要使用的组件中，有点类似重命名，简化使用，而不用写

​			this.$store.state.property来获取state中的属性 。。。。。

​			import { mapGetters, mapState } from "vuex";

​			

​			state  ：...mapState(['p1','p2','p3'])

​			getter：...mapGetters(['g1','g2'])			

