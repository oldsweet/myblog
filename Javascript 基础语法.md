# Javascript 基础语法



# 1.数据类型

```JavaScript
var str = "hello world"; // 声明了一个字符串
```

```JavaScript
var str = ”hello world";
str = 100; // 这个时候str是Number
```

- **可以使用typeof来检查一个变量的类型**

```javascript
var a = 100;
alert(typeof(a)); // 输出一个变量的类型

```

### Number

- Number.MAX_VALUE 

  - 表示Number的最大值

    ```javascript
    输出：1.7976931348623157e+308
    ```

  - 大于该数就是Infinity

    ```javascript
    var a = Number.MAX_VALUE
    alert(a + 1)
    // 输出Infinity
    ```

  - 但是该数仍然是Number类型

    ```javascript
    var a = Number.MAX_VALUE
    alert(typeof(a*a))
    // 输出Number
    ```

  - ```javascript
    Number.MIN_VALUE; // 最小的正数
    ```

  - 在js中整数基本上可以保证正确，如果js进行小数运算，可能会出现精度问题。不要调用js进行精度要求比较高的运算

- NaN

  - Not a Number

    ```javascript
    var s1 = "hello";
    var s2 = "world";
    alert(s1 * s2);
    // 输出NaN
    ```

    ```javascript
    
    var a = NaN;
    var b = "NaN";
    alert(typeof(a)); // 输出Number
    alert(typeof(b)); // 输出string
    ```

### Boolean

- 布尔值只有两个，主要用来进行逻辑判断

- ```javascript
  var b = false;
  var a = true;
  ```

### Null

- Null 类型的值只有一个，就是null

- null专门用来表示一个空的 **对象**

  ```javascript
  var a = null;
  alert(typeof a);
  // 输出object
  ```

### undefined

- 当一个声明变量没有赋值，那它就是一个undefine类型



## summary

```javascript
	var soco = "hello world";
    alert(soco);
    alert(typeof soco) // 表示String类型

    var t = 100;
    alert(100);
    alert(typeof t);  // 表示Number数据类型
    alert(Number.MAX_VALUE); 

    var t;
    alert(t); // 输出undefine
    alert(typeof(t)); // 表示undefine 类型
    
    var t = false;
    alert(typeof t); // Boolean数据类型
    alert(t) // 输出false

     var t = null;
     alert(t); // 输出null
     alert(typeof t) // 输出object
     // null数据类型表示一个空对象

    var a = NaN;
    alert(typeof a); // 输出number

    var t = Number.MAX_VALUE * Number.MAX_VALUE ;
    alert(t); // 输出Infinity 超出了Number类型表示的最大值
    alert(typeof t); // 输出number 还是一个number类型的数
```

## 数据类型转换

**类型转换是将其他数据类型转换为String**

- 转换为string

  - 方法一——调用toString函数

    - 调用被转换的数据类型的toString方法

      ```javascript
        var a = 123;
         var s1 = a.toString();  // 类型转换，返回一个string类型的值
      
         alert(typeof s1); // 输出string
         alert(s1); // 输出“123”
      ```

    - 该方法不会影响原变量，自会将将一个string变量返回

    - 但是注意，null和undefined这两个值没有toString方法

      ~~~javascript
       var a = null;
        alert(a.toString()); // 会报错
      
        var b = undefined;
        alert(b.toString()); // 也会报错
      ~~~

  - 方法二——调用String函数

    - 对于number和Boolean来说和toString一样

    ~~~JavaScript
    var a = 123;
    var b = String(a); // 如toString
    
    
    alert(b) // 输出“123”
    alert(typeof b) // 输出string  
    ~~~

    - 与toString不同的是

      ```javascript
         var t = undefined;
              var a = String(t);
      
              alert(a); // 输出“undefined”
      
              var t = null;
              var a = String(t);
              alert(a); // 输出“null”
      
      ```

### 将其它数据类型转换为number类型

- 调用Number（）函数来转换

   

  ```javascript
  var a = "123";
  b = Number(a); // 纯数字，就转换为number。
  
  var a = "    ";
  var b = Number(a);
  alert(b);   // 遇到空串或者空白串就转换为0
  alert(typeof b); // Number
  
  var a = "abc";
  var b = Number(a);
  alert(b);   // 当遇到非字符时转换为NaN
  alert(typeof b); // 输出NaN
  
  var a = false;
  b = Number(a);
  alert(b); // 输出0
  alert(typeof b); // 数据类型为number   true --> 1  false --> 0
  
  var a = undefined;
  var b = Number(a);
  alert(b);
  alert(typeof b); // 输出Number
  
  var a = null;
  var b = Number(b);
  alert(b);// 输出一个NaN
  alert(typeof b); // 输出Number
  
  var a = null;
  var b = Number(a);
  alert(b);// 输出0
  alert(typeof b); // 输出number
  
  var a = undefined;
  var b = Number(a);
  alert(b);// 输出NaN
  alert(typeof b); // 输出number
  ```

- paserInt 和 paserFloat

  **当遇到非数字的时候就会退出检索**

  - paserInt

    ```javascript
          var a = "1000px";
          var b = parseInt(a); // 得到一个整数
          alert(b); // 输出1000
          alert(typeof b);
    
          var a = "px";
          var b = parseInt(a);
          alert(b); // NaN
          alert(typeof b); // number
    
          var a = "100.100px";
          var b = parseInt(a);
          alert(b); // 100 获取一个整数
          alert(typeof b); // number
    ```

  - paserFloat

    ```javascript
            var a = null;
            var b = parseFloat(a); // 获取一个浮点数，当参数不是字符串时先换为字符串，再转换
            alert(b); // NaN
            alert(typeof b) // number
    ```

    

