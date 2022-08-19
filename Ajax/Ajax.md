### 一、了解Ajax

​	Ajax能让网页与服务器之间实现**数据交互**

### 二、jQuery中的Ajax

​	![1657122746695](E:\笔记\Ajax\Ajax.assets\1657122746695.png)

1. #### $.get() 函数的语法

   ```
   $.get(url,[data],[callback])
   ```

   

2. #### $.post() 函数的语法

   ```
   $.post(url,[data],[callback])
   ```

3. #### $.ajax() 函数的语法

   ```
   $.ajax({
       type:'',	//请求方式，GET 或 POST
       url:'',		//请求的url地址
       data:{},	//这次请求要携带的数据
       success:function(res){}	//请求成功之后的回调函数
   })
   ```

### 三、接口

​	使用Ajax请求数据时，被请求的URL地址，就叫做**数据接口**（简称：**接口**）

1. 接口文档

   接口的说明文档，它是我们调用接口的依据

2. 接口文档的组成部分

   1. **接口名称**：用来标识各个接口的简单说明
   2. **接口URL**：接口的调用地址
   3. **调用方式**：接口的调用方式。如GET 和 POST
   4. **参数格式**：接口需要传递的参数，每个参数必须包含参数名称、参数类型、是否必选、参数说明
   5. **响应格式**：接口的返回值的详细描述，一般包含数据名称、数据类型、说明
   6. 返回示例（可选）：通过对象的形式，例举服务器返回数据的结构

### 四、form表单

1. #### action

   用来规定提交表单时，向何处发送表单数据

2. #### method

   用来规定以何种方式把表单数据提交到 action URL

   默认情况下值为：get

   **注意：**①get方式适合用来提交少量的、简单的数据

   ②post方式适合用来提交大量的、复杂的、或包含文件上传的数据

3. #### enctype

   用来规定在 发送表单数据之前如何对数据进行编码

   ![1657199110928](E:\笔记\Ajax\Ajax.assets\1657199110928.png)

4. #### target

   用来规定在何处打开 action URL

   ![1657198857219](E:\笔记\Ajax\Ajax.assets\1657198857219.png)


### 五、通过Ajax提交表单数据

1. #### 监听表单提交事件

   方式一：

   ```
   $('#form1').submit(function(e){
   				alert('监听到了表单的提交事件')
   			})
   ```

   方式二：

   ```
   $('#form1').on('submit',function(e){
   				alert('监听到了表单的提交事件')
   			})
   ```

   

2. #### 阻止表单提交事件

   ```
   .preventDefault()
   ```

3. 快速获取表单中的数据

   serialize() 函数:可以一次性获取到表单中的所有数据

   ```
   $(selector).serialize()
   ```

   **注意：**使用serialize()获取表单数据时，必须为每个表单添加**name**属性

### 六、模板引擎

​	根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面

​	优点：     ①减少了字符串的拼接操作

​			②使代码结构更清晰

​			③使代码更易于阅读与维护

1. #### art-template的使用步骤

   1. 导入art-template
   2. 定义数据
   3. 定义模板
   4. 调用template函数
   5. 渲染 HTML结构

2. art-template标准语法

   1. 原文输出

      ```
      {{ @ value }}
      ```

   2. 条件输出

      ```
      {{if value }} 按需输出的内容 {{/if}}
      ```

      ```
      {{if v1 }} 按需输出的内容 {{else if v2 }} 按需输出的内容 {{/if}}
      ```

   3. 循环输出

      ```
      {{each 数组名}}
      	{{$index}} {{$value}}
      {{/each}}
      ```

   4. 过滤器

      ![1657247019583](E:\笔记\Ajax\Ajax.assets\1657247019583.png)

      ```
      {{ value | filterName }}
      ```

      定义过滤器的基本语法：

      ```
      template.defaults.imports.filterName = function(value){/* return 处理的结果*/}
      ```

   5. **补时间案例**

      ```
      // 给时间补零的函数
          function padZero(n) {
              if (n < 10) {
                  return '0'+n
              } else {
                  return n
              }
          }
      
        // 定义格式化时间的过滤器
        template.defaults.imports.dateFormat = function (dtStr) {
          var dt = new Date(dtStr);
      
          var y = dt.getFullYear();
          var m = padZero(dt.getMonth() + 1);
          var d = padZero(dt.getDate());
      
          var hh = padZero(dt.getHours());
          var mm = padZero(dt.getMinutes());
          var ss = padZero(dt.getSeconds());
      
          // return 'yyy-mmm-ddd hh:mm:ss'
          return y + "-" + m + "-" + d + " " + hh + ":" + mm + ":" + ss;
        };
      ```


### 七、正则与字符

1. 基本语法

   exec() 函数用于 检索字符串中的正则表达式的匹配

   如果字符串中有匹配的值，则返回该匹配值，否则返回null

   ```
   RegExpOject.exec(string)
   ```

2. 提取分组

   正则表达式 ()  包起来的内容表示一个分组，可以通过分组来提取自己想要的内容

   ![1657261127402](E:\笔记\Ajax\Ajax.assets\1657261127402.png)

3. 字符串的replace 函数

   replace() 函数用于在字符串中用一些字符 替换另一些字符

   ```
   var result = '123456'.replace('123','abc')	//得到的 result 的值为字符串abc456
   ```

4. 使用while循环replace

   ![1657263358384](E:\笔记\Ajax\Ajax.assets\1657263358384.png)

### 八、XMLHttprequest的基本使用

​	通过XMLHttprequest可以请求**服务器上的数据资源**

1. 使用xhr发起GET请求

   步骤：

   ①创建xhr对象

   ②调用xhr.open()函数

   ③调用xhr.send()函数

   ④监听xhr.onreadystatechange事件

   ![1657267915806](E:\笔记\Ajax\Ajax.assets\1657267915806.png)

2. 了解xhr对象的readyState属性

   用来表示**Ajax请求所处的状态**

   ![1657267992230](E:\笔记\Ajax\Ajax.assets\1657267992230.png)

3. 查询字符串

   ![1657268356621](E:\笔记\Ajax\Ajax.assets\1657268356621.png)

4. URL编码与解码

   ①encodeURI() 编码的函数

   ②dencodeURI() 解码的函数

   ![1657268872532](E:\笔记\Ajax\Ajax.assets\1657268872532.png)

5. 使用xhr发起POST请求

   1. 使用xhr发起GET请求

      步骤：

      ①创建xhr对象

      ②调用xhr.open()函数

      ③设置 **Content-Type** 属性 （固定写法） 

      ④调用xhr.send()函数

      ⑤监听xhr.onreadystatechange事件

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

### 九、数据交换格式

​	服务器与客户端之间进行**数据传输与交换的方式**

1. ## JSON

   JavaScript对象和数组的字符串表示法

   **本质就是字符串**

2. JSON的两种结构

   1. 对象结构

   2. 数组结构

      数据的类型：

      ​	**数字，字符串，布尔值，null，数组，对象**6中类型

3. JSON和JS对象的关系

   ![1657277157307](E:\笔记\Ajax\Ajax.assets\1657277157307.png)

4. JSON和JS对象的互转

   1. 从JSON字符串转换为JS对象，使用JSON.parse() 方法。

      把字符串转换为 数据对象的过程，叫做反序列化

      ![1657277259332](E:\笔记\Ajax\Ajax.assets\1657277259332.png)

   2. 从JS对象转换为JSON字符串，使用JSON.stringify() 方法。

      把数据对象转换为字符串的过程，叫做序列化

      ![1657277323860](E:\笔记\Ajax\Ajax.assets\1657277323860.png)

      
