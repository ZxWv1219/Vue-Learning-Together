## 邂逅 Vuejs

### 内容概述

- 认识 Vuejs
  - 为什么学习 Vuejs
  - 简单认识一下 Vuejs
- Vuejs 安装方式
  - CDN 引入
  - 下载和引入
  - NPM 安装管理
- Vuejs 初体验
  - Hello Vuejs
  - Vue 列表展示
  - 案例：计数器
- Vuejs 的 MVVM
  - Vue 中的 MVVM

### 为什么学习 Vuejs?

- 公司新项目决定使用 Vue 的技术栈。
- 目前招聘前端的需求中，10 个有 8 个都对 Vue 有或多或少的要求。
- 当然，作为学习者我们知道 Vuejs 目前非常火，可以说是前端必备的一个技能。

### 简单认识一下 Vuejs

- Vue (读音 (v 依 又)，类似于  view)，不要读错。

- Vue 是一个渐进式的框架，什么是渐进式的呢？

  - 渐进式意味着你可以将 Vue 作为你应用的一部分嵌入其中，带来更丰富的交互体验。

  - 或者如果你希望将更多的业务逻辑使用 Vue 实现，那么 Vue 的核心库以及其生态系统。

  - 比如 Core+Vue-router+Vuex，也可以满足你各种各样的需求。

- Vue 有很多特点和 Web 开发中常见的高级功能
  - 解耦视图和数据
  - 可复用的组件
  - 前端路由技术
  - 状态管理
  - 虚拟 DOM
- 这些特点，你不需要一个个去记住，我们在后面的学习和开发中都会慢慢体会到的，一些技术点我也会在后面进行讲解。
- 学习 Vuejs 的前提？

  - 从零学习 Vue 开发，并不需要你具备其他类似于 Angular、React，甚至是 jQuery 的经验。
  - 但是你需要具备一定的 HTML、CSS、JavaScript 基础。

- Vue.js 安装

使用一个框架，我们第一步要做什么呢？安装下载它
安装 Vue 的方式有很多：
方式一：直接 CDN 引入
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

方式三：NPM 安装
后续通过 webpack 和 CLI 的使用，我们使用该方式。

### Hello Vuejs

- 我们来做我们的第一个 Vue 程序，体验一下 Vue 的响应式

```js
let app = new Vue({
  el: "#app",
  data: {
    name: "hello vuejs",
  },
})
```

- 我们来阅读 JavaScript 代码，会发现创建了一个 Vue 对象。
- 创建 Vue 对象的时候，传入了一些 options：{}
  - el 属性: 该属性决定了这个 Vue 对象挂载到哪一个元素上，很明显，我们这里是挂载到了 id 为 app 的元素上
  - data 属性：该属性中通常会存储一些数据,这些数据可以是我们直接定义出来的，比如像上面这样。也可以来自我们写的接口。

### Vue 列表显示

- HTML 代码中，使用 v-for 指令

该指令我们后面会详细讲解，这里先学会使用

```html
<div>
<ul>
<li v-for='item in books'>
{{item}}
<li>
<ul>
</div>
```

```js
let app = new Vue({
  el: "#app",
  data: {
    books: ["c语言入门到精通", "C#入门到精通", "java入门到放弃"],
  },
})
```

- 我们再也不需要在 JavaScript 代码中完成 DOM 的拼接相关操作了
- 而且，更重要的是，它还是响应式的。也就是说，当我们数组中的数据发生改变时，界面会自动改变。

### 案例：计数器

- 现在，我们来实现一个小的计数器
  - 点击 + 计数器+1
  - 点击 - 计数器 -1
- 这里，我们又要使用新的指令和属性了 - 新的属性：methods，该属性用于在 Vue 对象中定义方法。
  - 新的指令：@click, 该指令用于监听某个元素的点击事件，并且需要指定当发生点击时，执行的方法(方法通常是 methods 中定义的方法)
- 你可能会疑惑？
  - 这些@click 是什么东西？
  - Vue 对象中又是定义 el/data/methods，到底都有哪些东西可以定义，以及它们的作用是什么？
  - 这些疑惑在后续学习中都会一一解开。

### Vue 中的 MVVM

- 什么是 MVVM 呢？

  概念自己百度,我这里不做过多解释和说明

- 我们直接来看 Vue 的 MVVM
  ![1595317473_1_.jpg](https://i.loli.net/2020/07/21/mAOBoGZnyvlxMFV.png)

- View 层：
  - 视图层
  - 在我们前端开发中，通常就是 DOM 层。
  - 主要的作用是给用户展示各种信息。
- Model 层：
  - 数据层
  - 数据可能是我们固定的死数据，更多的是来自我们服务器，从接口上请求下来的数据。
- VueModel 层：
  - 视图模型层
  - 视图模型层是 View 和 Model 沟通的桥梁。
  - 一方面它实现了 Data Binding，也就是数据绑定，将 Model 的改变实时的反应到 View 中
  - 另一方面它实现了 DOM Listener，也就是 DOM 监听，当 DOM 发生一些事件(点击、滚动、touch 等)时，可以监听到，并在需要的情况下改变对应的 Data。

### 计数器的 MVVM

- 计数器的 MVVM
  - 我们的计数器中就有严格的 MVVM 思想
    - View 依然是我们的 DOM
    - Model 就是我们我们抽离出来的 obj
    - ViewModel 就是我们创建的 Vue 对象实例
- 它们之间如何工作呢？
  - 首先 ViewModel 通过 Data Binding 让 obj 中的数据实时的在 DOM 中显示。
  - 其次 ViewModel 通过 DOM Listener 来监听 DOM 事件，并且通过 methods 中的操作，来改变 obj 中的数据。
- 有了 Vue 帮助我们完成 VueModel 层的任务，在后续的开发，我们就可以专注于数据的处理，以及 DOM 的编写工作了。

### 创建 Vue 实例传入的 options

- 你会发现，我们在创建 Vue 实例的时候，传入了一个对象 options。
- 这个 options 中可以包含哪些选项呢？
  - [详细解析](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE)
- 目前掌握这些选项：
  - el:
    - 类型：string | HTMLElement
    - 作用：决定之后 Vue 实例会管理哪一个 DOM。
  - data:
    - 类型：Object | Function （组件当中 data 必须是一个函数）
    - 作用：Vue 实例对应的数据对象。
  - methods:
    - 类型：{ [key: string]: Function }
    - 作用：定义属于 Vue 的一些方法，可以在其他地方调用，也可以在指令中使用。

### Vue 的生命周期(重点)

![1595318187_1_.jpg](https://i.loli.net/2020/07/21/e1OdVcyPi7fIg5o.png)

![1595318250_1_.jpg](https://i.loli.net/2020/07/21/cInBlOMzSodQ8Ti.png)


![1595318461_1_.jpg](https://i.loli.net/2020/07/21/IyGVa9AEsJtUzec.png)