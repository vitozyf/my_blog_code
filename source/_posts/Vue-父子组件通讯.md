---
title: Vue-父子组件通讯
date: 2017-03-04 21:56:54
tags: 
- js
- vue
categories: 
- frame
- vue
---

## 父子组件通讯

- 当部分重复的功能在每一个组建中都使用的时候，可以将该功能抽成一个子组件，包含这个子组件的组件则为父组件

### 父组件如何集成子组件

1. 新建子组件(如subcomment.vue)

2. 集成到父组件(参考:`https://cn.vuejs.org/v2/guide/components.html`)

   1. 在父组件中导入子组件

      ```javascript
      import subCommon from "../subcomponents/comment.vue";
      ```

      ​

   2. 在父组件中注册子组件,属性为注册名，直接使用，值为引入进来的子组件

      ```javascript
      export default {
        components:{
                    subcomment:subcomment 
                   }
      }
      ```

   3. 在我们父组件的template中使用子组件，就可以将子组件集成进来了

      ```javascript
       <subCommon :newsInfoId="this.$route.params.id"></subCommon>
      ```

### 父组件如何把值传给子组件

- 参考:`https://cn.vuejs.org/v2/guide/components.html#构成组件`

- 子组件(接收方)

  - 在Vue对象中，通过props声明，声明它期待获得的数据

    ```javascript
     export default {
    		props:['commentId']
     }
    ```

- 父组件(发送发)

  - 在使用子组件的时候，通过属性名称=值的方式，将值传给子组件

    ```javascript
    <subcomment :commentId="this.$route.params.newsId"></subcomment>
    ```


---

**父组件利用props往子组件传输数据**

- 父组件：

  ```javascript
  <div>
    <child v-bind:my-message="parentMsg"></child>//注意传递参数时要用—代替驼峰命名，HTML不区分大小写
  </div>
  ```

- 子组件：

  ```javascript
  Vue.component('child', {
    // camelCase in JavaScript
    props:{myMessage},
    template: '<span>{{ myMessage }}</span>'
  })
  ```

  > 如上所示，父组件在模板中引用子组件，通过v-bind传递参数myMessage，值为parentMsg，其可以为父组件中的动态属性，同时不用v-bind直接myMessage="hello传递静态值给子组件，则传递的值就是hello字符串。在利用props实现传值的过程中理论上是要实现单向传递，即父组件改变相关参数的值，子组件也相应变化，但是子组件对参数的改变不应该影响父组件。**但是当props中接收的是父组件传递的引用类型（对象或者是数组）时，在子组件中对数据改变时，父组件中的数据也会相应的改变，因为两者是指向的同一地址内存。**如果不想子组件的改变影响父组件可以利用深拷贝，将接受的数据进行深拷贝后在子组件中使用，而不直接操作接受的数据。深拷贝可以直接利用ES6中的obj=Object。assign（{},myMessage）（在computed中定义），这样子组件的改动将不会影响到父组件。

**子组件向父组件传递参数利用事件机制**

子组件通过this.$emit()派发事件，父组件利用v-on对事件进行监听，实现参数的传递

- 子组件：

  ```javascript
  this.$emit('changeCart',event.target)/*向父组件派发事件，同时传递参数event.target,后面的参数的个数不限*/
  ```

- 父组件：

  ```javascript
  <v-cartcontrol :food="food" v-on:changeCart="changeCart"></v-cartcontrol>
  ```

  **同时当有组件嵌套时则需要利用该机制一层一层的触发到指定层，不然直接在顶层监听子组件的子组件的事件是监听不到的，需要先向父组件派发，父组件在向上层触发**

