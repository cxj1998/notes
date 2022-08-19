一、在项目中操作数据库的步骤

1. 安装操作MySQL数据库的第三方模块（mysql）

   ```
   npm i mysql
   ```

   配置mysql模块

   ```
   // 1、导入 mysql 模块
   const mysql = require("mysql");
   
   // 2、建立与 mysql 数据库的连接关系
   const db = mysql.createPool({
     host: "127.0.0.1", //数据库 IP 的地址
     user: "root", //登录数据库的账号
     password: "admin123", //登录数据库的密码
     database: "my_db_01", //指定要操作哪个数据库
   });
   ```

   

2. 通过mysql模块连接到 MySQL数据库

3. 通过mysql模块执行SQL语句

4. ```
   //测试 mysql 模块能否正常工作
   db.query('select 1', (err, results)=>{
       // mysql 模块工作期间报错
       if(err) return console.log(err.message)
       // 能够成功执行 SQL语句
       console.log(results);
   })
   ```

二、操作MySQL数据库

1. 查询数据

   ```
   select * from users
   ```

   ![1657189703404](E:\笔记\数据库\mysql模块.assets\1657189703404.png)

   **注意**：如果执行的是select查询语句，则执行的结果是数组

2. 插入数据

   ```
   insert into users (username,password) values (?,?)
   ```

   ![1657189782455](E:\笔记\数据库\mysql模块.assets\1657189782455.png)

   注意：如果执行的是 insert into插入语句，则 results 是一个对象；可以通过 **affectedRows** 属性，来判断是否插入数据成功

   - 插入数据的便捷方式

     ```
     insert into users set ?
     ```

     ![1657190702694](E:\笔记\数据库\mysql模块.assets\1657190702694.png)

3. 更新数据

   ```
   update users set username=?,password=? where id=?
   ```

   ![1657191139676](E:\笔记\数据库\mysql模块.assets\1657191139676.png)

   - 更新数据的便捷方式

     ```
     update users set ? where id=?
     ```

     ![1657192019609](E:\笔记\数据库\mysql模块.assets\1657192019609.png)

4. 删除数据

   ```
   delete from users where id=?
   ```

   ![1657192065828](E:\笔记\数据库\mysql模块.assets\1657192065828.png)

5. 标记删除

   执行update语句，将这条数据对应的status字段标记为删除即可

   ```
   const sqlStr = 'update users set status=? where id=?
   ```

   ![1657192337762](E:\笔记\数据库\mysql模块.assets\1657192337762.png)