# Vue Router

>  Vue Router 是 [Vue.js](http://cn.vuejs.org/) 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌。

### 官网示例

```html
<div id="app">
    <h1>Hello App!</h1>
    <p>
        <!-- 使用 router-link 组件来导航. -->
        <!-- 通过传入 `to` 属性指定链接. -->
        <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
        <router-link to="/foo">Go to Foo</router-link>
        <router-link to="/bar">Go to Bar</router-link>
        <!-- 路由出口 -->
        <!-- 路由匹配到的组件将渲染在这里 -->
        <router-view></router-view>
    </p>
</div>
```

```vue
<script type="text/javascript">

    // 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

    // 1. 定义 (路由) 组件。
    // 可以从其他文件 import 进来
    const Foo = {template: '<div>foo</div>'}
    const Bar = {template: '<div>bar</div>'}

    // 2. 定义路由
    // 每个路由应该映射一个组件。 其中"component" 可以是
    // 通过 Vue.extend() 创建的组件构造器，
    // 或者，只是一个组件配置对象。
    // 我们晚点再讨论嵌套路由。
    const routes = [
        {path: '/foo', component: Foo},
        {path: '/bar', component: Bar}
    ]

    // 3. 创建 router 实例，然后传 `routes` 配置
    // 你还可以传别的配置参数, 不过先这么简单着吧。
    const router = new VueRouter({
        routes // (缩写) 相当于 routes: routes
    })

    // 4. 创建和挂载根实例。
    // 记得要通过 router 配置参数注入路由，
    // 从而让整个应用都有路由功能
    const app = new Vue({
        el: '#app',
        router,
    });
</script>
```

js:

1. 定义路由组件
2. 定义路由
3. 创建router实例，然后传routes
4. 创建和挂载根实例

html：

 	1.  <router-link to="/foo">Go to Foo</router-link>
       	1.  使用router-link组件来导航，其会被渲染成a标签
       	2.  to指定routes中定义的path
	2.  <router-view></router-view> 
     	1.  路由出口，routes中配置的组件显示在这里





