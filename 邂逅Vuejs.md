## 邂逅Vuejs

### 内容概述

* 认识Vuejs
    - 为什么学习Vuejs
    - 简单认识一下Vuejs
* Vuejs安装方式
    - CDN引入
    - 下载和引入
    - NPM安装管理
* Vuejs初体验
    - Hello Vuejs
    - Vue列表展示
    - 案例：计数器
* Vuejs的MVVM
    - Vue中的MVVM

### 为什么学习Vuejs?

* 公司新项目决定使用Vue的技术栈。
* 目前招聘前端的需求中，10个有8个都对Vue有或多或少的要求。
* 当然，作为学习者我们知道Vuejs目前非常火，可以说是前端必备的一个技能。

### 简单认识一下Vuejs

* Vue (读音 (v 依 又)，类似于 view)，不要读错。

* Vue是一个渐进式的框架，什么是渐进式的呢？

    - 渐进式意味着你可以将Vue作为你应用的一部分嵌入其中，带来更丰富的交互体验。

    - 或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统。

    - 比如Core+Vue-router+Vuex，也可以满足你各种各样的需求。

* Vue有很多特点和Web开发中常见的高级功能
    - 解耦视图和数据
    - 可复用的组件
    - 前端路由技术
    - 状态管理
    - 虚拟DOM
* 这些特点，你不需要一个个去记住，我们在后面的学习和开发中都会慢慢体会到的，一些技术点我也会在后面进行讲解。
* 学习Vuejs的前提？
    - 从零学习Vue开发，并不需要你具备其他类似于Angular、React，甚至是jQuery的经验。
    - 但是你需要具备一定的HTML、CSS、JavaScript基础。

* Vue.js安装

使用一个框架，我们第一步要做什么呢？安装下载它
安装Vue的方式有很多：
方式一：直接CDN引入
你可以选择引入开发环境版本还是生产环境版本

``` 
<!-- 开发环境版本，包含了有帮助的命令行警告 --> 
<script src = "https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> 
<!--生产环境版本， 优化了尺寸和速度 --> 
<script src = "https://cdn.jsdelivr.net/npm/vue"></script>
```

方式二：下载和引入
```
//开发环境 
https://vuejs.org/js/vue.js 
//生产环境 
https://vuejs.org/js/vue.min.js
```
方式三：NPM安装
后续通过webpack和CLI的使用，我们使用该方式。
