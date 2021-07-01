# JavaScript Chapter 3

- 语法

- 数据类型

- 流控制语句

- 函数

  ## 3.1 语法

  - 区分大小写 ：大量的借鉴了c的格式
  - 标识符： 指的是函数，变量，属性的名字
    - 格式与c相同
    - JavaScript标识采用驼峰大小写的格式
    - 不能把关键字，保留字，true，false，null作为标识符
  - 注释：JavaScript的注释和c一样
  - 严格模式：在代码块的顶部加上  **"use strict"**可以启用严格模式
  - 最后一个语句没有；也可支持编译，但是不推荐

  ## 3.2 关键字和保留字

  - 关键字：描述一组特定用途的关键字，可以用来表示控制语句的开始和结束，或者执行一些特定的操作
  - 保留字： 他们将来可能被用来作为关键字
  - JavaScript使用关键字作为标识符的时候，会导致“Identifier Expected”错误

  ## 3.3 变量

  - JavaScript的变量是松散类型的

    ```JavaScript
    var num1; // 这样就是创建了一个局部变量
    var num2 = 10; // 创建了一个局部变量并进行初始化
    
    num = 10; // 这样的变量被创建成为全局变量
    // 如下例
    
    function test(){
        num = 10;
    }
    test();
    alert(num); // 输出为10，num被创建为全局变量
    
    /*
    *	这样的创建并不被推荐使用，会导致后面的代码维护困难
    *	在严格模式下，会导致ReferenceError
    */
    ```

  - 可以使用一条语句定义多个变量

    ```javascript
    var a = "sss",
    	b = 10,
    	c = 'h';
    // 这样就初始化了三个变量
    ```

  - 在严格模式下，不能定义eval和arguments的变量

  ## 3.4 数据类型

  - JavaScript中有5种简单数据类型（也称基本数据类型）：Undefined，Null，Boolean，Number，String

  - 还有一种复杂数据类型——Object，Object本质上是一种无序的名值对组成的

  - JavaScript数据类型具有动态性，因此没有再定义其他数据类型的必要了

  - typeof 操作符 

  - typeof是一个操作符，而不是一个函数

    - “undefined” ——这个值没有定义
    - “boolean” —— 这个值是布尔值
    - “string” —— 这个值是字符串
    - ”number“ ——如果这个值是数值
    - ”object“ —— 如果这个值是对象或null;
    - ”function“ —— 如果这个值是函数
    - typeof的操作对象可以是变量也可以是数值字面量
    - null被认为是一个空的对象引用

  - Undefined类型

    - Undefined只有一个值那就是”undefined“，在使用var声明变量却没有对其加工初始化时，这个变量的值就是”undefined"

      ```JavaScript
      var message;
      alert(message); // 输出的就是undefined
      // undefined字面量的主要目的就是为了比较
      // undefined的引入就是为了区分未定义的变量和空对象
      ```

    - 包含undefined值的变量与未定义的变量还是不一样的

      ```javascript
      var message;
      
      // var a; 这个变量没有定义
      alert(message); // 输出undefined
      alert(a); // 报错
      ```

    - 虽然输出结果不一样，但是typeof操作符操作的结果是一样的

      ```javascript
      var message;
      
      // var a; 未定义的变量 
      alert(typeof message)； // 输出undefined
      alert(typeof a); // 输出undefined
      /* 
      *	在实际的操作中建议显式的初始化，这样就可以很好的区分是没定义还是为初始化
      */
      ```

  - Null 类型

    - Null类型只有一个字面量，就是null。从逻辑的角度看，null**表示一个空对象指针** 

      ```javascript
      var tem = null;
      alert(typeof tem); // 输出Object
      ```

    - 如果一个变量要用来表示对象，应该初始化为"null",这样就可以很好区分对象和简单数据类型

    - 实际上undefined是派生自undefined的

      ```JavaScript
      alert(null == undefined); // 输出true
      ```

  - Boolean 类型

    - 该类型只有两个字面量true和false

    - 转调函数Boolean()

      ```javascript
      var message = "Hello world";
      var messageAsBoolean = Boolean(message); // messageAsBoolean被转换为true
      
      // 这种转换对控制流语句十分重要
       if(message){
           
       }
      // 运行这个程序会有警告，自动调用了Boolean()函数
      ```

  - Number 类型

    - 该类型使用754标准来表示
    - 可以通过10进制，2进制，8进制，16进制来表示，在算数运算时都会被转换为10进制

