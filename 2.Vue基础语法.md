## Vue 基础语法

### 内容概述

- 插值操作
- 绑定属性
- 计算属性
- 事件监听
- 条件判断
- 循环遍历
- 案例
- v-model

### Mustache(读音: 吗 斯 踏 区)

- 我们已经学习过了，可以通过 Mustache 语法(也就是双大括号)。
- Mustache: 胡子/胡须 {

## 插值操作

- v-once
- v-html
- v-text
- v-pre
- v-cloak

* 如何将 data 中的文本数据，插入到 HTML 中呢？
* 我们可以像下面这样来使用，并且数据是响应式的
  ![1595388919_1_.jpg](https://i.loli.net/2020/07/22/AF5I7RgEzVbBKQr.png)
  ![1595388980_1_.jpg](https://i.loli.net/2020/07/22/ICDMWYBSFZPOyNK.png)

### v-once

- 在某些情况下，我们可能不希望界面随意的跟随改变

  - 这个时候，我们就可以使用一个 Vue 的指令**v-once**

- 什么指令?

  - 在 vue 中有大家要区分一下指令和语法表达式
  - **v-once**该指令后面不需要跟任何表达式(比如之前的 **v-for** 后面是由跟表达式的)
  - 该指令表示元素和组件(组件后面才会学习)只渲染一次，不会随着数据的改变而改变。

```html
<body>
  <div id="app">
    <h2 v-once>{{name}}</h2>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        name: "李小龙",
      },
    })
  </script>
</body>
```

### v-html

- 某些情况下，我们从服务器请求到的数据本身就是一个 HTML 代码

  - 如果我们直接通过{{}}来输出，会将 HTML 代码也一起输出。
  - 但是我们可能希望的是按照 HTML 格式进行解析，并且显示对应的内容。

- 如果我们希望解析出 HTML 展示

  - 可以使用 v-html 指令

    - 该指令后面往往会跟上一个 string 类型
    - 会将 string 的 html 解析出来并且进行渲染

```html
<body>
  <div id="app">
    <h2 v-html="link"></h2>
    <h2>{{link}}</h2>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        link: `<a href='http://www.baidu.com'>这里是百度aka 摆渡</a>`,
      },
    })
  </script>
</body>
```

### v-text

- v-text 作用和 Mustache 比较相似：都是用于将数据显示在界面中
- v-text 通常情况下，接受一个 string 类型

```html
<body>
  <div id="app">
    <h2 v-text="name"></h2>
    <h2>{{name}}</h2>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        name: "李小龙",
      },
    })
  </script>
</body>
```

![1595390436_1_.jpg](https://i.loli.net/2020/07/22/5NgBAmv9DE8SpCX.png)

### v-pre

v-pre 用于跳过这个元素和它子元素的编译过程，用于显示原本的 Mustache 语法。
比如下面的代码：

- 第一个 h2 元素中的内容会被编译解析出来对应的内容
- 第二个 h2 元素中会直接显示{{name}}

```html
<body>
  <div id="app">
    <h2>{{name}}</h2>
    <h2 v-pre>{{name}}</h2>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        name: "李小龙",
      },
    })
  </script>
</body>
```

![1595399407_1_.jpg](https://i.loli.net/2020/07/22/eK3ZIvk9ulyJ8mq.png)

### v-cloak

在某些情况下，我们浏览器可能会直接显然出未编译的 Mustache 标签。

- 这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 [v-cloak] { display: none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

```html
<style>
  [v-cloak] {
    display: none;
  }
</style>

<body>
  <div id="app">
    <h2>{{name}}</h2>
    <h2 v-cloak>{{name}}</h2>
  </div>
  <script>
    setTimeout(() => {
      let app = new Vue({
        el: "#app",
        data: {
          name: "李小龙",
        },
      })
    }, 2000)
  </script>
</body>
```

## 属性绑定

- 前面我们学习的指令主要作用是将值插入到我们模板的内容当中。
- 但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定。
  - 比如动态绑定 a 元素的 href 属性
  - 比如动态绑定 img 元素的 src 属性
- 这个时候，我们可以使用 **v-bind** 指令：
  - 作用：动态绑定属性
  - 缩写：**:**
  - 预期：any (with argument) | Object (without argument)
  - 参数：attrOrProp (optional)

下面，我们就具体来学习 v-bind 的使用。

### v-bind 基础

- **v-bind** 用于绑定一个或多个属性值，或者向另一个组件传递 props 值(这个学到组件时再介绍)
- 在开发中，有哪些属性需要动态进行绑定呢？
  - 还是有很多的，比如图片的链接 src、网站的链接 href、动态绑定一些类、样式等等
- 比如通过 Vue 实例中的 data 绑定元素的 src 和 href，代码如下：

```html
<body>
  <div id="app">
    <a v-bind:href="link">这里是百度aka 摆渡</a>
    <img v-bind:src="imgUrl">{{name}}</img>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        imgUrl: "https://i.loli.net/2020/07/22/eK3ZIvk9ulyJ8mq.png",
        link: 'https://www.baidu.com/'
      }
    })
  </script>
</body>
```

### v-bind 语法糖

**v-bind** 有一个对应的语法糖，也就是简写方式
在开发中，我们通常会使用语法糖的形式，因为这样更加简洁。

简写方式如下：

```html
  <div id="app">
    <a :href="link">这里是百度aka 摆渡</a>
    <img :src="imgUrl">{{name}}</img>
  </div>
```

### v-bind 绑定 class

- 很多时候，我们希望动态的来切换 class，比如：
  - 当数据为某个状态时，字体显示红色。
  - 当数据另一个状态时，字体显示黑色。
- 绑定 class 有两种方式：

  - 对象语法
  - 数组语法

- 绑定方式：**对象语法**
  - 对象语法的含义是:class 后面跟的是一个对象。
- 对象语法有下面这些用法：

```html
<div id="app">
  <!-- 用法一：直接通过{}绑定一个类 -->
  <h2 :class="{'active': isActive}">Hello World</h2>

  <!-- 用法二：也可以通过判断，传入多个值 -->
  <h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>

  <!-- 用法三：和普通的类同时存在，并不冲突 -->
  <!-- 注：如果isActive和isLine都为true，那么会有title/active/line三个类 -->
  <h2 class="title" :class="{'active': isActive, 'line': isLine}">
    Hello World
  </h2>

  <!-- 用法四：如果过于复杂，可以放在一个methods或者computed中 -->
  <!-- 注：getClasses是一个方法使用时不能省略掉括号 ()  -->
  <h2 class="title" :class="getClasses()">Hello World</h2>
  <!-- 注：classes是一个计算属性使用计算属性时些处可以省略掉括号 ()  -->
  <h2 class="title" :class="classes">Hello World</h2>
</div>
```

- 绑定方式：**数组语法**
  - 数组语法的含义是:class 后面跟的是一个数组。
- 数组语法有下面这些用法：

```html
<div id="app">
  <!-- 用法一：直接通过[]绑定一个类 -->
  <h2 :class="['active']">Hello World</h2>

  <!-- 用法二：也可以通过判断，传入多个值 -->
  <h2 :class="['active','line']">Hello World</h2>

  <!-- 用法三：和普通的类同时存在，并不冲突 -->
  <!-- 注：如果isActive和isLine都为true，那么会有title/active/line三个类 -->
  <h2 class="title" :class="['active', 'line']">Hello World</h2>

  <!-- 用法四：如果过于复杂，可以放在一个methods或者computed中 -->

  <!-- 注：getClasses是一个方法使用时不能省略掉括号 ()  -->
  <h2 class="title" :class="getClasses()">Hello World</h2>
  <!-- 注：classes是一个计算属性使用计算属性时些处可以省略掉括号 ()  -->
  <h2 class="title" :class="classes">Hello World</h2>
</div>
```

### v-bind 绑定 style

- 我们可以利用 v-bind:style 来绑定一些 CSS 内联样式。
- 在写 CSS 属性名的时候，比如 font-size
  - 我们可以使用驼峰式 (camelCase) fontSize
  - 或短横线分隔 (kebab-case，记得用单引号括起来) ‘font-size’
- 绑定 class 有两种方式：
  - 对象语法
  - 数组语法

```html
<div id="app">
  <!-- 
    动态绑定时CSS属性使用小驼峰,
    如果使用‘-’ 写法需要加单引号'font-size' 而不是font-size,
    使用'-'时会解析成运算符号，
    且value 使用单引号时会解析成字符串，不使用单引号时解析成变量
  -->
  <a v-bind:href="baidu" :style="{'font-size':fontSize}">百度一下</a><br />
  <a v-bind:href="baidu" :style="{'font-size':'50px'}">百度一下</a><br />
  <a v-bind:href="baidu" :style="getStyle()">百度一下</a><br />
  <!-- 数组语法 -->
  <a v-bind:href="baidu" :style="[style1,style2]">百度一下</a><br />
</div>
```

### 什么是计算属性？

- 我们知道，在模板中可以直接通过插值语法显示一些 data 中的数据。
- 但是在某些情况，我们可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示
  - 比如我们有 firstName 和 lastName 两个变量，我们需要显示完整的名称。
  - 但是如果多个地方都需要显示完整的名称，我们就需要写多个{{firstName}} {{lastName}}
- 我们可以将上面的代码换成计算属性 . OK，我们发现计算属性是写在实例的 computed 选项中的

```html
<body>
  <div id="app">
    {{fullName}}
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        firstName: "Kobe",
        lastName: "Bryant",
      },
      computed: {
        fullName() {
          return this.firstName + " " + this.lastName
        },
      },
    })
  </script>
</body>
```

### 计算属性的 setter 和 getter

- 每个计算属性都包含一个 getter 和一个 setter

在上面的例子中，我们只是使用 getter 来读取。
在某些情况下，你也可以提供一个 setter 方法（不常用）。
在需要写 setter 的时候，代码如下：

```html
<body>
  <div id="app">
    {{fullName}}
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        firstName: "Kobe",
        lastName: "Bryant",
      },
      computed: {
        //使用getter 和 setter时 fuallName要使用对象面不是function
        //不使用getter 和 setter时,默认使用的是getter所以computed里常看到都是以function存在
        fullName: {
          //基本上很少使用set属性，需要改变计算属性时，直接改变data属性的值 计算属性就会改变
          set: function (value) {
            console.log(value)
          },
          get: function () {
            return this.firstName + " " + this.lastName
          },
        },
      },
    })
  </script>
</body>
```

### 计算属性的缓存

- 我们可能会考虑这样的一个问题：
  - methods 和 computed 看起来都可以实现我们的功能，
  - 那么为什么还要多一个计算属性这个东西呢？
  - 原因：计算属性会进行缓存，如果多次使用时，计算属性只会调用一次。
    我们来看下面的代码：

```html
<body>
  <div id="app">
    {{fullName}} {{fullName}} {{fullName}} {{fullName}} {{getFullName}}
    {{getFullName}} {{getFullName}} {{getFullName}}
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        firstName: "Kobe",
        lastName: "Bryant",
      },
      methods: {
        getFullName() {
          console.log("methods")
          return this.firstName + " " + this.lastName
        },
      },
      computed: {
        fullName() {
          console.log("computed")
          return this.firstName + " " + this.lastName
        },
      },
    })
  </script>
</body>
```

## 事件监听

- 在前端开发中，我们需要经常和用于交互。

  - 这个时候，我们就必须监听用户发生的时间，比如点击、拖拽、键盘事件等等
  - 在 Vue 中如何监听事件呢？使用 **v-on** 指令

- v-on 介绍
  - 作用：绑定事件监听器
  - 缩写：@
  - 预期：Function | Inline Statement | Object
  - 参数：event

下面，我们就具体来学习 v-on 的使用。

### v-on 基础

这里，我们用一个监听按钮的点击事件，来简单看看 v-on 的使用
下面的代码中，我们使用了 v-on:click="number++”
另外，我们可以将事件指向一个在 methods 中定义的函数

- v-on 也有对应的语法糖：
- v-on:click 可以写成 **@click**

```html
<body>
  <div id="app">
    <div>{{number}}</div>
    <button v-on:click="number++">+</button>
    <button @click="number--">-</button><br />
    <button v-on:click="add">+</button>
    <button @click="substract">-</button>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        number: 0,
      },
      methods: {
        add() {
          this.number++
        },
        substract() {
          this.number--
        },
      },
    })
  </script>
</body>
```

### v-on 参数

- 当通过 methods 中定义方法，以供@click 调用时，需要注意参数问题：
- 情况一：如果该方法不需要额外参数，那么方法后的()可以不添加。
  - 但是注意：如果方法本身中有一个参数，那么会默认将原生事件 event 参数传递进去
- 情况二：如果需要同时传入某个参数，同时需要 event 时，可以通过\$event 传入事件。

```html
<body>
  <div id="app">
    <div>{{number}}</div>
    <button v-on:click="number++">+</button>
    <button @click="number--">-</button><br />
    <button v-on:click="add">+</button>
    <button @click="substract(20,$event)">-</button>
  </div>
  <script>
    let app = new Vue({
      el: "#app",
      data: {
        number: 0,
      },
      methods: {
        add(event) {
          console.log(event)
          this.number++
        },
        substract(number, event) {
          console.log(event)
          console.log(number)
          this.number -= number
        },
      },
    })
  </script>
</body>
```

### v-on 修饰符

- 在某些情况下，我们拿到 event 的目的可能是进行一些事件处理。
- Vue 提供了修饰符来帮助我们方便的处理一些事件：

  - .stop - 调用 event.stopPropagation()。
  - .prevent - 调用 event.preventDefault()。
  - .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。
  - .native - 监听组件根元素的原生事件。
  - .once - 只触发一次回调。

  ```html
  <div id="app">
    <div @click='btnClickOut()'>我在外面
      <!-- 禁用冒泡 .stop-->
      <button @click.stop='btnClickIn()'>我在里面</button>
    </div>
    <br>
    <form action="https://www.baidu.com">
      <input type="submit" value="提交"></input>
      <!-- 禁用默认事件 .prevent 执行指定事件-->
      <input type="submit" value="提交" @click.prevent='btnSubmitPre()'></input>
    </form>
    <!-- 禁用默认事件 .prevent 没有表达式 -->
    <form action="https://www.baidu.com" @submit.prevent>
      <input type="submit" value="提交"></input>
    </form>

    <!-- 监听某个键盘按键按下 -->
    <input type="text" @keyup.enter='keyUp()'></input>

    <!-- .once 只能点击一次-->
    <button @click.once='btnClickOnce'>once</button>
  </div>
  ```

## 条件判断

- v-if
- v-else-if
- v-else

这三个指令与 JavaScript 的条件语句 if、else、else if 类似。
Vue 的条件指令可以根据表达式的值在 DOM 中渲染或销毁元素或组件

### v-if

- v-if 的原理：

  - v-if 后面的条件为 false 时，对应的元素以及其子元素不会渲染。
    也就是根本没有不会有对应的标签出现在 DOM 中。

- v-if 的使用
- v-if v-else 的结合使用
- v-else-if 的使用

### 小案例

我们来做一个简单的小案例：
用户再登录时，可以切换使用用户账号登录还是邮箱地址登录。
类似如下情景：
![1595409030_1_.png](https://i.loli.net/2020/07/22/aYD6zNpKe1rBfH4.png)

在家思考一下怎么做这个东西?

- 小问题：

  - 如果我们在有输入内容的情况下，切换了类型，我们会发现文字依然显示之前的输入的内容。
  - 但是按道理讲，我们应该切换到另外一个 input 元素中了。
  - 在另一个 input 元素中，我们并没有输入内容。
  - 为什么会出现这个问题呢？

- 解答

  - 这是因为 Vue 在进行 DOM 渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。
  - 在上面的案例中，Vue 内部会发现原来的 input 元素不再使用，直接作为 else 中的 input 来使用了。

- 解决方案：
  - 如果我们不希望 Vue 出现类似重复利用的问题，可以给对应的 input 添加 key
  - 并且我们需要保证 key 的不同

### v-show

- v-show 的用法和 v-if 非常相似，也用于决定一个元素是否渲染：
- v-if 和 v-show 对比
- v-if 和 v-show 都可以决定一个元素是否渲染，那么开发中我们如何选择呢？
  - v-if 当条件为 false 时，根本不会有对应的元素在 DOM 中。
  - v-show 当条件为 false 时，仅仅是将元素的 display 属性设置为 none 而已。
- 开发中如何选择呢？
  - 当需要在显示与隐藏之间切片很频繁时，使用 v-show
  - 当只有一次切换时，通过使用 v-if

## 循环遍历

- 当我们有一组数据需要进行渲染时，我们就可以使用 v-for 来完成。

  - v-for 的语法类似于 JavaScript 中的 for 循环。
  - 格式如下：item in items 的形式。

- 我们来看一个简单的案例：
- 如果在遍历的过程中不需要使用索引值
  - v-for="date in dateList"
  - 依次从 dateList 中取出 date，并且在元素的内容中，我们可以使用 Mustache 语法，来使用 date

```html
<div v-for="date in dateList">
  {{date}}
</div>
```

- 如果在遍历的过程中，我们需要拿到元素在数组中的索引值呢？
  - 语法格式：v-for=(item, index) in items
  - 其中的 index 就代表了取出的 item 在原数组的索引值。

```html
<div id="app">
  <ul>
    <li v-for="(item, index) in dateList">value={{item}},index={{index}}</li>
  </ul>
</div>
```

### v-for 遍历对象

v-for 可以用户遍历对象：
比如某个对象中存储着你的个人信息，我们希望以列表的形式显示出来。

```html
<body>
  <div id="app">
    <ul>
      <li v-for="item in userInfo">value={{item}}</li>
    </ul>
    <ul>
      <!-- (value,key) -->
      <li v-for="(item,key) in userInfo">value={{item}},key={{key}}</li>
    </ul>
    <ul>
      <!-- (value,key,index) -->
      <li v-for="(item,key,index) in userInfo">
        value={{item}},key={{key}},index={{index}}
      </li>
    </ul>
    <ul>
      <!-- 属性过多时不建议这样写 -->
      <li>{{userInfo.name}}</li>
      <li>{{userInfo.age}}</li>
      <li>{{userInfo.height}}</li>
    </ul>
  </div>

  <script src="../../vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        userInfo: {
          name: "张无忌",
          age: "18",
          height: "1.88",
        },
      },
    })
  </script>
</body>
```
