---
title: my_sql
date: 2016-06-24 22:36:05
tags: 
- sql
categories: 
- "数据库"
---

## 数据库介绍

1. 之前的数据是怎么存储的：存储在文本文件中`data.json`

- 缺点1：数据存取不方便，不利于维护和扩展，当数据量大了之后，无法直接通过打开文件的形式对数据进行操作；
- 缺点2：数据存储比较分散，无法进行集中式管理；
- 缺点3：安全性较低，由于数据是直接存储在文本文件中的，所有无法进行数据的加密，存在安全隐患；

1. Sql（Structured Query Language）数据库：提供了安全机制、便于通过**Sql语句**对数据直接进行操作。

- 支持 结构化查询语言（Sql）的数据库，叫做 `Sql数据库`
- `Sql`是一种查询语言，能够很方便的对数据进行CRUD；

1. 常见的数据库的分类

- 传统的关系型数据库（Sql数据库）：Oracle（甲骨文 Java）、DB2、MySql、MS SQL Server、Sqlite【关系型数据库，对于大量数据的存取效率很高】
- 现在比较流行的非关系型数据库（No-Sql数据库）：Redis(内部以键值对形式存储数据，是内存数据库)、CouchDB、MongoDb（可以把数据对应到实际的物理磁盘，MongoDB使用JS来操作数据）【一般当作中间层来使用，对于少量数据存取速度非常快，但是当数据多了之后，效率就变慢】

## 安装配置`PHPStudy`、`navicat`

1. PHPStudy傻瓜式安装：默认的用户名是`root`，默认的密码也是`root`
2. navicat傻瓜式安装、一键激活（建议安装navicat时候选择默认安装路径，方便一键激活）
3. 关系型数据库的整体介绍：

- MySql中的数据库服务是什么
- MySql中的数据库是什么：一个数据服务中通常包含一个或多个数据库。每个数据库由名字来进行区分；
- MySql中的数据库表是什么：一个数据库通常包含一个或多个表。每个表由一个名字标识（例如“客户”或者“订单”）。表包含带有数据的记录（行）。
- 数据库服务就相当于是一个国家；数据库表相当于是省份；数据库表相当于是省份中的市；

## 数据库可视化工具`navicat`的基本使用

1. 打开和关闭数据库连接
2. 创建用户、设置用户权限
3. 新建数据库、新建表、设计表（设置字段类型）、设置Id自增、日期自动插入

- 新建`users`用户表，表字段为：id、name、age、gender、address、isdel
- Id自增：设置为主键，勾选`自动递增`
- 主键：是用来标识数据表中每一行数据的唯一性的，确保独一无二性。

1. 创建表并添加字段：

```
    新建一张 Users 表
    表中有 6 个 字段【注意：在JS中每个对象身上有很多属性，当这个对象的数据，存储到数据中之后，这些属性，就被叫做 字段】

    id  用户 id
    number   ->  Int(整数类型)
    Id必须要有，同时不能重复
    主键：是用来唯一标识一条数据的，标识数据具有唯一性，不能重复
    注意：在一个表中，一般只有一个主键来标识唯一性
    如果勾选了Int 类型的 Id为 自动增长，则每次写入数据的时候，可以不提供id，数据库会自动写入一个Id

    name  用户名
    string   ->    varchar(可变长度的字符)
    不能为空

    age  年龄
    number  ->  Int

    gender  性别
    string    ->    varchar

    address 地址
    string    ->    varchar

    isdel   是否被删除
    bool   ->   boolean    tinyint
```

## 使用Sql语句对数据库执行基本操作

```
-- 这是注释

-- 插入一条数据
-- 写入一条数据，用户名是 小红 年龄是 13 性别是 女 地址是 深圳
-- 插入数据的语法 INSERT INTO 表名 (字段1, 字段2,...) VALUES (字段1的值, 字段2的值,....)
-- INSERT INTO users (name, age, gender, address) VALUES ('小红', 13, '女', '深圳')

-- 插入数据  用户名 大红 年龄26 性别 女 地址 上海
-- INSERT INTO users (name, age, gender, address) VALUES ('大红', 26, '女', '上海')

-- 插入数据 用户名 escook  年龄 30
-- INSERT into users (name, age)  VALUES ('escook', 30)

-- 修改数据
-- UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
-- UPDATE users set gender='男' WHERE id=5

-- 修改 id 为 5 的那一条数据，将 性别改为女 ， 地址改为 铁岭， isdel改为 1
-- update users set gender='女', address='铁岭', isdel=1 where id=5

-- 删除数据  语法：DELETE FROM 表名称 WHERE 列名称 = 值
-- 删除id 为5 的这一条数据
-- delete from users where id=5

-- 查询 指定的列（字段）
-- select name, age, gender from users

-- 查询表中的所有数据  * 代表所有字段
-- select * from users

-- 查询表中 名字为 zs 的用户
-- select id, name, age from users where name='zs'

-- 查询表中 name 为 zs 和 name 为 ls 的数据
-- SELECT * from users where name='zs' or name='ls'

-- 查询 表中，name 为 zs 并且 age 为 12 的数据
-- select * from users where name='zs' and age=12

-- 查询表中，name 为zs 或者 address 为 广州 的用户
-- select * from users where name='zs' or address='广州'

-- 查询 表中 年龄 以 2开头 的用户
-- select * from users where age like '2%'

-- 查询表中，name 以 红 结尾的数据 【模糊查询用 like， 精确查询用 =】
-- select * from users where name like '%红'

-- 查询表中，名字中有 s 的用户
-- select * from users WHERE name like '%s%'

-- 查询表中所有用户，并按照 年龄 从小到大排序
-- 注意：使用 order by 进行排序，默认是升序排序，升序排序用 asc  降序排序用 desc
-- select * from users ORDER BY age asc

-- 查询表中所有数据，按照age 降序排序
-- select * from users ORDER BY age desc

-- 查询表中 性别为女的用户，并按照 age 降序排序
-- 注意：如果一条语句中同时涉及到了 where 和 order by ，则先写 where 后写 order by
-- select * from users where gender='女' ORDER BY age desc

-- 查询表中，gender 不为 女 的用户
-- select * from users where gender!='女'

-- 查询表中，所有 address 不为 null 的用户
-- select * from users where address is not NULL

-- 查询表中 gender 为 null 的数据
-- select * from users where gender is NULL

-- 查询 id 在 3 ~ 6 区间内的所有数据
-- select * from users where id >=3 and id <=6
-- 注意：BETWEEN AND 必须把小值写的前面，大值写到后面，而且查询时候，是包含这两个区间的
-- select * from users where id BETWEEN 3 and 6

-- 根据订单表中的用户Id，查询出来每个订单所属的用户名
-- select orders.orderid, orders.ordertitle, users.name from orders LEFT JOIN users ON orders.userId=users.id
```

## 使用`node.js`代码的方式进行增删改查

使用命令行执行`npm install mysql --save`安装操作MySQL数据库的模块；

### 连接数据库

```
// 导入MySQL模块
var mysql = require('mysql');

// 创建一个数据库连接
var connection = mysql.createConnection({
    user: 'root',
    password: '123456',
    database: 'mydb'
});

// 连接数据库
connection.connect();
```

### 基本查询操作

```
var sqlStr = 'select * from heros';
connection.query(sqlStr, function (err, results, fields) {
    if (err) throw err;
    console.log(results.length);
});
```

### 在查询语句中使用参数

```
// 获取客户端传递过来的查询参数
var id = 8;
var name = '小红';

// 拼接查询参数
connection.query('select * from heros where id="' + id + '" and name="' + name + '"', function (err, results, fields) {
    if (err) throw err;
    console.log(results.length);
});
```

### 使用参数化查询语句

```
// 通过问号的形式拼接查询参数，问号相当于占位符，将来，传递的真实的数据会替换掉问号所在的区域
// 真实参数列表可以通过数组的形式进行传递，问号占位符所代表的参数顺序，就是实际数组中每一项的作用
const sqlStr = 'select count(*) from heros where id=? and name=?';
connection.query(sqlStr, [id, name], function (err, results, fields) {
    if (err) throw err;
    console.log(results[0]['count(*)']);
});
```

### 添加数据

```
// 插入数据
var sqlStr = 'insert into heros (name, gender, avatar) values (?, ?, ?)';
connection.query(sqlStr, ['小小', '女', 'img/119.jpg'], function(err, results, fields){
    if(err) throw err;
    console.log(results);
});
```

便捷的插入数据：

```
var user = { name: '尼古拉斯凯奇', age: 54, gender: '男', address: '美国' };
connection.query('insert into users set ?',user , function (err, result, fields) {
  if (err) throw err;
  console.log(result);
});
```

### 更新数据

```
var sqlStr = 'update heros set name=?, gender=? where id=?';
connection.query(sqlStr, ['大大', '男', 12], function(err, results, fields){
    if(err) throw err;
    console.log(results);
});
```

便捷的更新数据：

```
var user = {
  id:6,
  age:9,
  name:'OK'
}
connection.query('update users_copy set ? where id=?', [user, 6], function(err, results){
  if(err) throw err;
  console.log(results);
});
```

### 删除数据

#### 硬删除

```
// 数据硬删除，执行成功之后，匹配到的数据记录，将会从表中删除
connection.query('delete from heros where id=12', function(err, results, fields){
    if(err) throw err;
    console.log(results);
});
```

#### 软删除

```
// 数据软删除，通过给表添加isdel字段，来标识数据记录是否被删除，true表示被删除，false表示未删除
// 数据软删除的好处：能最大限度地保留数据的原始性
connection.query('update heros set isdel=? where id=?', [true, 10], function(err, results, fields){
    if(err) throw err;
    console.log(results);
});
```

## 用户列表案例

### body-parser 中间件

- 注意：一定要把 body-parser 注册的过程，放到 注册路由之前，否则不生效

1. 导入 解析 表单 Post 提交上来数据的 一个第三方 中间件
   - `var bodyParser = require('body-parser');`
2. 注册一下这个第三方中间件
   - 其中，extended: false 表示不使用第三方的插件去解析表单数据，而是使用 Node 内置的 querystring 来解析 数据
   - `app.use(bodyParser.urlencoded({ extended: false }));`
3. 分析 body-parser 内部的实现原理：
   1. 由于他是一个中间件，所以能够拿到 req 和 res 这两个对象；
   2. 拿到 req 之后，这个中间件，调用了 req.on('data', (chunk)=>{}) 和 req.on('end',()=>{})
   3. 在这两个事件内部，body-parser中间件，将 post 过来的数据进行了一下解析，解析完毕后拿到一个数据对象
   4. 把解析出来的数据对象，通过自定义属性的形式， 追加为了 req.body 

## 相关文章

- [MDN - JSON.stringify()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [MDN - FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)
- [MDN - FormData](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData)
- [Express - 中文网](http://www.expressjs.com.cn/)
- [Express - 英文官网](http://expressjs.com/)
- [Node.js 教程](http://www.runoob.com/nodejs/nodejs-tutorial.html)
- [菜鸟教程 - Express 4.x API 中文文档](https://www.runoob.com/w3cnote/express-4-x-api.html)
- [Express.js 4.0 的路由（Router）功能用法教學](https://blog.gtwang.org/programming/learn-to-use-the-new-router-in-expressjs-4/)
- [github - art-template](https://github.com/aui/art-template)
- [github - express-art-template](https://github.com/aui/express-art-template)
- [github - ejs](https://github.com/mde/ejs)
- [W3School - Sql教程](http://www.w3school.com.cn/sql/sql_insert.asp)