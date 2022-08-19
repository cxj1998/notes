## 一、XMLHttprequest的基本使用

​	通过XMLHttprequest可以请求**服务器上的数据资源**

------

### 	1、使用xhr发起GET请求

##### 		步骤：

​		①创建xhr对象

​		②调用xhr.open()函数

​		③调用xhr.send()函数

​		④监听xhr.onreadystatechange事件

​	![](E:\笔记\Ajax\Ajax加强.assets\1657267915806.png)

### 	2、了解xhr对象的readyState属性

​		用来表示**Ajax请求所处的状态**

​	![](E:\笔记\Ajax\assets\1657267992230.png)

### 	3、查询字符串

![](E:\笔记\Ajax\assets\1657268356621.png)

### 	4、URL编码与解码

+ **encodeURI()** 编码的函数

+ **dencodeURI()** 解码的函数

  ![](E:\笔记\Ajax\assets\1657268872532.png)

### 5、使用xhr发起POST请求

#### 	步骤：

​	①创建xhr对象

​	②调用xhr.open()函数

​	③设置 **Content-Type** 属性 （固定写法） 

​	④调用xhr.send()函数

​	⑤监听xhr.onreadystatechange事件

```
// 1.创建 xhr 对象
      var xhr = new XMLHttpRequest();

      // 2.调用 open 函数
      xhr.open("POST", "http://www.liulongbin.top:3006/api/addbook");

      // 3.设置 Content-Type 属性
      xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

      // 4.调用 send 函数
      xhr.send("bookname=水浒传&author=施耐庵&publisher=上海图书出版社");

      // 5.监听事件
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log(xhr.responseText);
        }
      };
```

## 二、数据交换格式

​	服务器与客户端之间进行**数据传输与交换的方式**

### 1、JSON

​	JavaScript对象和数组的**字符串表示法**

### 2、JSON的两种结构

+ **对象结构**

+ **数组结构**

  数据类型：**数字，字符串，布尔值，null，数组，对象**6中类型

### 3、JSON和JS对象的关系

![](E:\笔记\Ajax\assets\1657277094986.png)

### 4、JSON和JS对象的互转

+ 从JSON字符串转换为JS对象，使用**JSON.parse()** 方法。

  + 把字符串转换为 数据对象的过程，叫做反序列化

    ![](E:\笔记\Ajax\assets\1657277259332.png)

+ 从JS对象转换为JSON字符串，使用**JSON.stringify()** 方法。

  + 把数据对象转换为字符串的过程，叫做序列化

    ![](E:\笔记\Ajax\assets\1657277323860.png)

## 三、封装自己的Ajax函数

### 1、要实现的效果

![1657288727195](E:\笔记\Ajax\assets\1657288727195.png)

### 2、定义option 参数选项

​	itheima() 函数是我们自定义的Ajax函数，它接收一个配置对象作为参数，配置对象中可以配置如下属性：

+ method——请求的类型
+ url——请求的url地址
+ data——请求携带的数据
+ success——请求成功之后的回调函数

### 3、处理data函数

​	需要把data对象，转化成查询字符串的格式，从而提交给服务器，因此提前定义 resolveData 函数如下：

![1657289014285](E:\笔记\Ajax\assets\1657289014285.png)

### 4、定义itheima函数

​	在itheima() 函数中，需要创建xhr对象，并监听 onreadystatechange事件：

![1657289480589](E:\笔记\Ajax\assets\1657289480589.png)

### 5、判断请求的类型

​	不同的请求类型，对应xhr对象的不同操作，因此需要对请求类型进行 if...else...的判断：

![1657289935643](E:\笔记\Ajax\assets\1657289935643.png)

​			