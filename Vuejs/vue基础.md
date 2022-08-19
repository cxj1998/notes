## （一）Vue模板语法

### 	一.指令	

#### 	1、v-cloak指令

+ 插值表达式存在的问题：‘闪动’
+ 解决方案：使用 v-cloak 指令
+ 原理：先隐藏，替换好值之后再显示最终的值

![1657550304597](E:\笔记\Vuejs\assets\1657550304597.png)

#### 	2、数据绑定指令

+ **v-text** 填充纯文本
+ v-html 填充HTML片段
+ v-pre 填充原始信息

#### 	3、数据响应式

+ ##### 如何理解响应式

  + html5中的响应式（屏幕尺寸的变化导致样式的变化）
  + 数据的响应式（数据的变化导致页面内容的变化）
+ ##### 什么是数据绑定

  + 数据绑定：将数据填充到标签中
+ ##### **v-once** 只编译一次

  + 显示内容之后不再具有响应功能

#### 	4、双向数据绑定

+ ##### 双向数据绑定——v-model

+ ##### **MVVM 设计思想**

  + M（model）
  + V（view）
  + VM（View-Model）

  ![1657551434021](E:\笔记\Vuejs\assets\1657551434021.png)

#### 	5、事件绑定

+ ##### Vue处理事件——**v-on（简写：@）**

+ ##### 事件函数的调用方式

  + 直接绑定函数名称

    + ```
      <button @click="handle">按钮2</button>
      ```

  + 调用函数

    + ```
      <button @click="handle()">按钮3</button>
      ```

+ ##### 事件函数参数传递

  + **$event**：事件对象（实参）
  + **event**：默认参数（形参）
  + 事件绑定-参数传递
    + 如果事件直接绑定函数名称，那么默认会传递事件对象作为事件函数的第一个参数
    + 如果事件绑定函数调用，那么事件对象必须作为最后一个参数显示传递，并且事件对象的名称必须是$event 

#### 6、事件修饰符

+ ##### .stop阻止冒泡

  + ```
    <button @click="handle()">跳转</button>
    ```

    

+ ##### .prevent阻止默认行为

  + ```
    <button @click.stop="handle">跳转</button>
    ```

#### 7、按键修饰符

+  ##### .enter 回车键

  + ```
    <input v-on:keyup.enter="submit">
    ```

    

+ ##### .delete 删除键

  + ```
    <input v-on:keyup.delete="handle">
    ```

#### 8、自定义按钮修饰符

+ ##### 全局config.keyCodes 对象

  + ```
    Vue.config.keyCodes.f1=112
    ```


#### 9、属性绑定

+ ##### 动态处理属性

  + ```
    v-bind指令
    <a v-bind:href="url"></a>
    缩写形式
    <a :href="url"></a>
    ```

+ ##### v-model 的低层实现原理分析

  + ```
    <input type="text" v-bind:value="msg" v-on:input="msg=$event.target.value"
    ```

#### 10、样式绑定

+ ##### class样式处理

  + ###### 对象语法

  + ```
    <div v-bind:class="{ active: isActive}"></div>
    ```

  + ###### 数组语法

  + ```
    <div v-bind:class="{ activeClass,errorClass}}"></div>
    ```

+ ##### style样式处理

  + ###### 对象语法

  + ```
    <div v-bind:style="{ color:activeColor,fontSize:fontSize}"></div>
    ```

  + ###### 数组语法

  + ```
    <div v-bind:style="[baseStyles,overrridingStyles]"></div>
    ```

#### 11、分支循环结构

+ ##### 分支结构

  + v-if
  + v-else
  + v-else-if
  + v-show

+ ##### v-if 与 v-show 的区别

  + v-if 控制元素是否渲染到页面
  + v-show 控制元素是否显示

+ ##### 循环结构

  + ###### v-for 遍历数组

    + ```
      <li v-for="item in list">{{item}}</li>
      ```

    + 

    ```
    <li v-for="{item,index} in list">{{item}} + '---' + {{index}}</li>
    ```

  + ###### key的作用：帮助Vue区分不同的元素，从而提高性能

    + ```
      <li :key="item.id" v-for="{item,index} in list">{{item}} + '---' + {{index}}</li>
      ```

  + ###### v-for 遍历对象

    + ```
      <div v-for="(value, key, index) in object"></div>
      ```

  + ###### v-if 和 v-for 结合使用

    + ```
      <div v-if="value==12" v-for="(value, key, index) in object"></div>
      ```




#### 11、表单域修饰符

+ ##### number：转化为数值

+ ##### trim：去掉开始和结尾的空格

+ ##### lazy：将input事件切换为change事件

```
<input v-model.number="age" type="number">
```

#### 12、自定义指定

+ ##### 自定义指令的语法规则（获取元素焦点）

  + ```
    Vue.directive("focus", {
            inserted: function (el) {
              // 获取元素焦点
              el.focus();
            },
          });
    ```

+ ##### 自定义指令用法

  + ```
    <input type="text" v-focus>
    ```

+ ##### 带参数的自定义指令（改变元素背景色 ）

  + ```
    Vue.directive('color',{
            inserted:function(el,binding){
                el.style.backgroundColor = bind.value.color;
            }
          })
    ```

+ ##### 指令的用法

  + ```
    <input type="text" v-color="{color:'orange'}">
    ```

+ ##### 局部指令

  + ```
    directives: {
              focus: {
                // 指令的定义
                inserted: function (el) {
                  el.focus();
                },
              },
            },
    ```

#### 13、计算属性

+ ##### 计算属性的用法

  + ```
    computed: {
              reversedMessage: function () {
                return this.msg.split("").reverse().join("");
              },
            },
    ```

+ ##### 计算属性与方法的区别

  + 计算属性是基于他们的依赖进行缓存的
  + 方法不存在缓存

#### 14侦听器

+ 侦听器的应用场景
  + 数据变化时执行异步或开销较大的操作
+ 侦听器的用法
  + ![1657680733700](E:\笔记\Vuejs\assets\1657680733700.png)

#### 15、过滤器

+ ##### 自定义过滤器

  + ```
    vue.filter('过滤器名称'，function（value）{
        //过滤器业务逻辑
    })
    ```

+ ##### 过滤器的使用

  + ```
    <div>{{msg | upper}</div>
    <div>{{msg | upper | lower}</div>
    <div v-bind:id="id | formatId"></div>
    ```

+ ##### 局部过滤器

  + ```
    filters:{
        capitalize:function(){}
    }
    ```

+ ##### 带参数的过滤器

  + ```
    Vue.filter('format',function(value,arg1){
        //value 就是过滤器传递过来的参数
    })
    ```

    

+ ##### 过滤器的使用

  + ```
    <div>{{date | format('yyyy-MM-dd')}}</div>
    ```

#### 16生命周期

+ ##### 主要阶段

  + ![1657693977502](E:\笔记\Vuejs\assets\1657693977502.png)



## （二）组件化开发

### 一、组件注册

#### 1、全局组件注册语法

![1657698291715](E:\笔记\Vuejs\assets\1657698291715.png)

#### 2、组件用法

![1657698456895](E:\笔记\Vuejs\assets\1657698456895.png)

#### 3、组件注册注意事项

1. **data必须是一个函数**

2. **组件模板内容必须是单个跟元素**

3. **组件模板内容可以是模板字符串**

4. **组件命名方式**

   1. 短横线方式

      ```
      Vue.component('hello-world',{});
      ```

      

   2. 驼峰方式

      ```
      Vue.component('HelloWorld',{});
      ```

#### 4、局部组件注册

![1657700418867](E:\笔记\Vuejs\assets\1657700418867.png)

### 二、组件间数据交互

#### 1、父组件向子组件传值

+ 组件内部通过 props 接收传递过来的值
  + ![1657704185349](E:\笔记\Vuejs\assets\1657704185349.png)
+ 父组件通过属性将值传递给子组件
  + ![1657704198693](E:\笔记\Vuejs\assets\1657704198693.png)
+ props 属性名规则
  + ![1657704841045](E:\笔记\Vuejs\assets\1657704841045.png)
+ pros属性值类型
  + ![1657705635487](E:\笔记\Vuejs\assets\1657705635487.png)

#### 2、子组件向父组件传值

+ 子组件通过自定义事件向父组件传递信息
  + ![1657705790659](E:\笔记\Vuejs\assets\1657705790659.png)
+ 父组件监听子组件的事件
  + ![1657705823384](E:\笔记\Vuejs\assets\1657705823384.png)
+ 子组件通过自定义事件向父组件传递信息（带参数）
  + ![1657714998113](E:\笔记\Vuejs\assets\1657714998113.png)
+ 父组件监听子组件的事件（带参数）
  + ![1657715042095](E:\笔记\Vuejs\assets\1657715042095.png)

#### 3、非父子组件间传值

![1657715682424](E:\笔记\Vuejs\assets\1657715682424.png)

+ 单独的事件中心管理组件间通信
  + ![1657715659008](E:\笔记\Vuejs\assets\1657715659008.png)
+ 监听事件与销毁事件
  + ![1657715669003](E:\笔记\Vuejs\assets\1657715669003.png)
+ 触发事件
  + ![1657715716717](E:\笔记\Vuejs\assets\1657715716717.png)

#### 4、组件插槽

​	标签中间的内容是通过插槽动态变化的

+ 插槽位置
  + ![1657719419928](E:\笔记\Vuejs\assets\1657719419928.png)
+ 插槽内容
  + ![1657719434199](E:\笔记\Vuejs\assets\1657719434199.png)
+ 具名插槽
  + 插槽定义
    + ![1657719482387](E:\笔记\Vuejs\assets\1657719482387.png)
  + 插槽内容
    + ![1657719501323](E:\笔记\Vuejs\assets\1657719501323.png)
+ 作用域插槽
  + 插槽定义
    + ![1657720064930](E:\笔记\Vuejs\assets\1657720064930.png)
  + 插槽内容
    + ![1657720075010](E:\笔记\Vuejs\assets\1657720075010.png)

## （三）前后端交互模式

### 一、Promise 用法

#### 1、Promise 概述

​	Promise的异步编程的一种解决方案，从语法上来讲，Promise是一个对象，从它可以获取异步操作的消息

##### 	使用Promise主要有以下好处：

+ 可以避免多层异步调用嵌套问题（回调地狱）
+ Promise 对象提供了 简洁的API，使得控制异步操作更加容易

#### 2、Promise基本用法

+ 实例化Promise对象，构造函数中传递函数，该函数用于处理异步任务
+ **resolve**和**reject**两个参数用于处理成功和失败两种情况，并通过**p.then**获取处理结果
+ ![1657794023471](E:\笔记\Vuejs\assets\1657794023471.png)

#### 3、基于Promise处理Ajax请求

+ 处理原生Ajax
  + ![1657794600181](E:\笔记\Vuejs\assets\1657794600181.png)
+ 发送多个Ajax请求
  + ![1657795504780](E:\笔记\Vuejs\assets\1657795504780.png) 

#### 4、Promise常用的API

+ 实例方法
  + ![1657796244907](E:\笔记\Vuejs\assets\1657796244907.png)
  + ![1657796280577](E:\笔记\Vuejs\assets\1657796280577.png)
+ 对象方法
  + ![1657796575025](E:\笔记\Vuejs\assets\1657796575025.png)
  + ![1657796595101](E:\笔记\Vuejs\assets\1657796595101.png)

### 二、接口调用-fetch用法

#### 1、fetch概述

+ 基本特性
  + 更加简单点的获取数据方式，可以看做是xhr 的升级版
  + 基于Promise实现
+ 语法结构
  + ![1657812613174](E:\笔记\Vuejs\assets\1657812613174.png)

#### 2、fetch请求参数

+ 常用配置选项
  + ![1657812937814](E:\笔记\Vuejs\assets\1657812937814.png)
  + ![1657812950965](E:\笔记\Vuejs\assets\1657812950965.png)
+ GET请求方式的参数传递
  + ![1657883716639](E:\笔记\Vuejs\assets\1657883716639.png)
  + ![1657883761091](E:\笔记\Vuejs\assets\1657883761091.png)
+ DElETE请求方式的参数传递
  + ![1657884607923](E:\笔记\Vuejs\assets\1657884607923.png)
+ POST请求方式的参数传递
  + ![1657884708724](E:\笔记\Vuejs\assets\1657884708724.png)
  + ![1657888375975](E:\笔记\Vuejs\assets\1657888375975.png)
+ PUT请求方式的参数传递
  + ![1657890600344](E:\笔记\Vuejs\assets\1657890600344.png)

#### 3、fetch响应结果

+ 响应数据格式
  + text()：将返回处理成字符串类型
  + json()：返回结果和JSON.parse(responseText)一样
  + ![1657890762348](E:\笔记\Vuejs\assets\1657890762348.png)

### 三、接口调用-axios用法

#### 1、axios的基本用法

![1657889393075](E:\笔记\Vuejs\assets\1657889393075.png)

#### 2、axios的参数传递

+ GET传递参数（三种方法）
  + 通过URL传递参数
  + 通过params选项传递参数
  + ![1657899375085](E:\笔记\Vuejs\assets\1657899375085.png)
+ DELETE传递参数（三种方法）
  + ![1657899337622](E:\笔记\Vuejs\assets\1657899337622.png)
+ POST传递参数
  + 通过选项传递参数（默认传递的是json格式的数据）
    + ![1657899836524](E:\笔记\Vuejs\assets\1657899836524.png)
  + 通过URLSearchParams传递参数（application/x-www-form-urlencoded）
    + ![1657899908158](E:\笔记\Vuejs\assets\1657899908158.png)
+ PUT传递参数
  + 参数传递与post类似
    + ![1657901532001](E:\笔记\Vuejs\assets\1657901532001.png)



#### 3、axios的响应结果

+ 响应结果的主要属性
  + data：实际响应回来的数据
  + headers：响应头信息
  + status：响应状态码
  + statusText：响应状态信息
  + ![1657902046526](E:\笔记\Vuejs\assets\1657902046526.png)

#### 4、axios的全局配置

+ ![1657902169615](E:\笔记\Vuejs\assets\1657902169615.png)

#### 5、axios拦截器

+ 请求拦截器
  + 在请求发出之前设置一些信息
  + ![1657931246571](E:\笔记\Vuejs\assets\1657931246571.png)
  + ![1657931257403](E:\笔记\Vuejs\assets\1657931257403.png)
+ 响应拦截器
  + 在获取数据之前对数据做一些加工处理
  + ![1657931345042](E:\笔记\Vuejs\assets\1657931345042.png)
  + ![1657931353353](E:\笔记\Vuejs\assets\1657931353353.png)

### 四、接口调用-async/await用法

#### 1、async/await 的基本用法

+ ![1657932328101](E:\笔记\Vuejs\assets\1657932328101.png)
+ ![1657932337336](E:\笔记\Vuejs\assets\1657932337336.png)

#### 2、async/await 处理多个异步请求

+ 多个异步请求的场景
+ ![1657933245321](E:\笔记\Vuejs\assets\1657933245321.png)

### 五、路由的基本概念与原理

#### 1、路由

+ 后端路由
  + 概念：根据不同的用户URL请求，返回不同的内容
  + 本质：URL请求的地址与服务器资源之间的对应关系
  + ![1657936321867](E:\笔记\Vuejs\assets\1657936321867.png)
+ SPA（Single Page Application）
  + ![1657936366358](E:\笔记\Vuejs\assets\1657936366358.png)
+ 前端路由
  + 概念：根据不同的用户事件，显示不同的页面内容
  + 本质：用户事件与事件处理函数之间的对应关系
  + ![1657936501558](E:\笔记\Vuejs\assets\1657936501558.png)

#### 2、Vue Router

![1657938923779](E:\笔记\Vuejs\assets\1657938923779.png)

#### 3、基本使用步骤

1. 引入相关的库文件

   ![1657939053134](E:\笔记\Vuejs\assets\1657939053134.png)

2. 添加路由连接

   ![1657939069474](E:\笔记\Vuejs\assets\1657939069474.png)

3. 添加路由填充位

   ![1657939086573](E:\笔记\Vuejs\assets\1657939086573.png)

4. 定义路由组件

   ![1657939100339](E:\笔记\Vuejs\assets\1657939100339.png)

5. 配置路由规则并创建路由实例

   ![1657939112748](E:\笔记\Vuejs\assets\1657939112748.png)

6. 把路由挂载到Vue根实例中

   ![1657939132419](E:\笔记\Vuejs\assets\1657939132419.png)

#### 3、路由重定向

​	用户在访问地址A 的时候，强制用户跳转到地址 C，从而展示特定的组件页面，通过路由规则的 redirect 属性，指定一个新的路由地址，可以很方便地设置路由的重定向：

![1657944959272](E:\笔记\Vuejs\assets\1657944959272.png)

#### 4、vue-router嵌套路由

+ 嵌套路由功能分析
  + ![1657945425272](E:\笔记\Vuejs\assets\1657945425272.png)
+ 嵌套路由用法
  + 父路由组件模板
    + 父级路由链接
    + 父组件路由填充位
    + ![1657945509005](E:\笔记\Vuejs\assets\1657945509005.png)
  + 子路由模板
    + 子级路由链接
    + 子级路由填充位
    + ![1657945561132](E:\笔记\Vuejs\assets\1657945561132.png)
  + 嵌套路由配置
    + 父级路由通过 children 属性配置子级路由
    + ![1657945608354](E:\笔记\Vuejs\assets\1657945608354.png)

#### 5、vue-router动态路由匹配

+ 动态匹配路由的基本用法

  ![1657946732774](E:\笔记\Vuejs\assets\1657946732774.png)

+ 路由组件传递参数

  + props的值为布尔类型
    + ![1657947494035](E:\笔记\Vuejs\assets\1657947494035.png)
  + props的值为对象类型
    + ![1657947534237](E:\笔记\Vuejs\assets\1657947534237.png)
  + props的值为函数类型
    + ![1657947656429](E:\笔记\Vuejs\assets\1657947656429.png)

#### 6、vue-router命名路由

+ 命名路由的配置规则
  + ![1657948751927](E:\笔记\Vuejs\assets\1657948751927.png)

#### 7、vue-router编程式导航

+ 页面导航的两种方式
  + 声明式导航：通过点击链接实现导航的方式
    + ![1657949079666](E:\笔记\Vuejs\assets\1657949079666.png)
  + 编程式导航：通过调用JavaScript形式的API实现导航的方式
    + ![1657949118083](E:\笔记\Vuejs\assets\1657949118083.png)
    + 常用的编程式导航API如下：
      + ![1657949178860](E:\笔记\Vuejs\assets\1657949178860.png)
      + ![1657949187138](E:\笔记\Vuejs\assets\1657949187138.png)
    + router.push()方法的参数规则
      + ![1657949225177](E:\笔记\Vuejs\assets\1657949225177.png)

## （四）vue脚手架

### 一、Vue脚手架的基本用法

​	Vue 脚手架 用于 快速生成 Vue 项目基础架构，其官网地址为：https://cli.vuejs.org/zh/

### 	1.使用步骤

+ 安装3.x版本的vue 脚手架
  + ![1658473475924](E:\笔记\Vuejs\assets\1658473475924.png)



### 	2.基于3.x 版本的脚手架 创建vue项目

![1658473555815](E:\笔记\Vuejs\assets\1658473555815.png)

### 	3.Vue脚手架的自定义配置

+ 通过package.json配置项目
  + ![1658474137690](E:\笔记\Vuejs\assets\1658474137690.png)
+ 通过单独的配置文件配置项目
  + 在项目的跟目录创建文件 vue.config.js
  + 在该文件中进行相关配置，从而覆盖默认配置
  + ![1658474212393](E:\笔记\Vuejs\assets\1658474212393.png)



## （六）Element-UI 的基本使用

​	

```
官方地址：
https://element.eleme.io/#/zh-CN
```

### 	1、基于命名行方式手动安装

+ 安装依赖包 npm i element-ui -S
+ 导入 Element-UI 相关资源
+ ![1658474590849](E:\笔记\Vuejs\assets\1658474590849.png)

### 	2、基于图形界面自动安装

![1658474636290](E:\笔记\Vuejs\assets\1658474636290.png)