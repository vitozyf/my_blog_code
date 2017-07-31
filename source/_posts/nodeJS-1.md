---
title: nodeJS
date: 2016-08-23 22:32:53
tags: 
-  "node"
categories: 
-  "后台"
---

## path模块

1. path.join([...paths])方法

   - 作用：将给定的零散的路径片段，经过处理和规范化，最终得到一个完整的路径。

   - 有一个规则：如果路径片段中包含`./`或者`/`或者不带`/`，那么path.join直接把他们拼接起来；如果路径片段中带有`../`或多个`../`，那么这些`../`会将前面的路径给抵消掉。

     ```javascript
     path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
     // 返回: '/foo/bar/baz/asdf'
     path.join('foo', {}, 'bar');
     // 抛出 'TypeError: Path must be a string. Received {}'
     ```

2. path.basename(path,[...name])

   - 返回一个 `path` 的最后一部分

     ```javascript
     path.basename('/foo/bar/baz/asdf/quux.html');
     // 返回: 'quux.html'

     path.basename('/foo/bar/baz/asdf/quux.html', '.html');
     // 返回: 'quux'
     ```

3. path.dirname(path)

   - 永远把path字符串中的最后一个当做文件，返回的路径是最后一个文件之前的

     ```javascript
     path.dir("a/b/c/d")
     //把d当做文件，得到返回值为d的路径字符串 "a/b/c/"
     path.dirname('/foo/bar/baz/asdf/quux');
     // 返回: '/foo/bar/baz/asdf'
     ```

4. path.extname(path)

   - 获取文件扩展名,即从 `path` 的最后一部分中的最后一个 `.`（句号）字符到字符串结束。如果 `path` 的最后一部分没有 `.` 或 `path` 的文件名（见 `path.basename()`）的第一个字符是 `.`，则返回一个空字符串。

     ```javascript
     path.extname('index.html');// 返回: '.html'
     path.extname('index.coffee.md');// 返回: '.md'
     path.extname('index.');// 返回: '.'
     path.extname('index');// 返回: ''
     path.extname('.index');// 返回: ''
     ```

## 302重定向

- ```javascript
  res.writeHeader(302, { 'Location': '/' });
  res.end();
  ```

### data事件

- 每当客户端向服务器通过 post 提交数据的时候，都会触发 req 对象的 data 事件

- 我们可以通过 data 事件的 回调函数，拿到【分片传输】过来的数据

- 客户端发送的数据量可大可小，所以 data 事件可能会触发 1 到 多次

```javascript
var data = '';
      req.on('data', (chunk) => {
        data += chunk;
});
```

- 当 req 的 end 事件被触发的时候，就表示这次 post 提交的数据传输完毕了

- 这次数据传输完毕之后，最完整的数据在 data 中保存着

  ```javascript
   req.on('end', () => {})
  ```

## Node模块-querystring查询字符串

- querystring.parse(str[, sep[, eq[, options]]])

  - `str` 要解析的 URL 查询字符串。

  - `sep`用于界定查询字符串中的键值对的子字符串。默认为 `'&'`。

  - `eq`用于界定查询字符串中的键与值的子字符串。默认为 `'='`。

  - `querystring.parse()` 方法能把一个 URL 查询字符串（`str`）解析成一个键值对的集合。

    ```javascript
    例子，查询字符串 querystring.parse('foo=bar&abc=xyz&abc=123') 被解析成：
    {
      foo: 'bar',
      abc: ['xyz', '123']
    }
    ```

## JSON.stringify( )

- `JSON.stringify()` 方法将一个JavaScript值转换为一个JSON字符串，如果指定了一个replacer函数，则可以替换值，或者如果指定了一个replacer数组，可选地仅包括指定的属性。

- 参数

  - `value`

    将要序列化成 一个JSON 字符串的值。

  - `replacer` 可选

    如果该参数是一个函数，则在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理；如果该参数是一个数组，则只有包含在这个数组中的属性名才会被序列化到最终的 JSON 字符串中；如果该参数为null或者未提供，则对象所有的属性都会被序列化；关于该参数更详细的解释和示例，请参考[使用原生的 JSON 对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_native_JSON#The_replacer_parameter)一文。

  - `space` 可选

    指定缩进用的空白字符串，用于美化输出（pretty-print）；如果参数是个数字，它代表有多少的空格；上限为10。该值若小于1，则意味着没有空格；如果该参数为字符串(字符串的前十个字母)，该字符串将被作为空格；如果该参数没有提供（或者为null）将没有空格。

- 返回值 

  - 一个表示给定值的JSON字符串。

    ```javascript
    JSON.stringify(foo, ['week', 'month']);  
    // '{"week":45,"month":7}', 只保留“week”和“month”属性值。

    JSON.stringify({ uno: 1, dos : 2 }, null, '\t')
    // '{            \
    //     "uno": 1, \
    //     "dos": 2  \
    // }'
    ```

    ​

## 相关文章

- [felixge/node-formidable](https://github.com/felixge/node-formidable)
- [Node中使用 302 重定向](https://stackoverflow.com/questions/4062260/nodejs-redirect-url)
- [Nodejs基础：路径处理模块path总结](http://www.cnblogs.com/chyingp/p/node-learning-guide-path.html)
- [FormData 对象的使用](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)
- [深入浅出ES6（六）：解构 Destructuring](http://www.infoq.com/cn/articles/es6-in-depth-destructuring/)
- [MDN - Array.prototype.some()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
- [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)