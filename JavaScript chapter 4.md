# JavaScript chapter 4

- 理解基本类型和引用类型的值
- 理解执行环境
- 理解垃圾收集

## 4.1 基本类型和引用类型的值

- JavaScript中有两种不同类型的值：**基本类型值和引用类型值**

- 基本数据类型是按值访问，引用类型的值是保存在内存中的对象

- 在操作对象是，实际上是在操作对象的引用而不是实际的对象

- JavaScript中string类型的数值不是引用类型的

- 引用类型和基本类型的定义是类似的，创建一个变量并为该变量赋值

- 但是对不同类型可以执行的操作则大相径庭，我们可以对引用类型的值添加方法和属性

  ```JavaScript
  var person = new Object(); //创建一个引用类型的数值
  person.name = "ssssss"; // 为数值类型的数值添加属性
  alert(person.name); // 输出"sssss"
  ```

- 但是我们不能为一个基本类型添加属性，虽然这样不会报错

  ```JavaScript
  var name = "ssss"; // 创建了一个String类型的变量
  name.age = 10; // 为一个基本类型添加一个属性
  alert(name.age); // undefined
  ```

- 除了操作不同外，引用类型和基本类型复制变量的方法也不同

  ```JavaScript
  var num1 = 5;
  var num2 = num1;
  alert(num2); // 输出5
  num2 = 6;
  alert(num1); // 输出5
  alert(num2); // 输出6
  ```

  ![image-20210127121545830](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210127121545830.png)

- 两个变量在内存中有自己独立的空间，不会互相影响

- 而对于引用类型变量来说，复制变量会复制他们的指针，他们会指向同一个对象

  ```javascript
  var obj1 = new Object();
  var obj2 = obj1;
  obj1.name = "ssss";
  alert(obj2.name); // "ssss"
  ```

  ![image-20210127121939351](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210127121939351.png)

- 他们是内存中同一个对象的映射，所以会互相影响

- 传递参数

  - JavaScript中所有的参数都是按值传递的

  - 基本数据类型的传递规则如下

    ​	

    ```javascript
    function addTem(num){ // 复制变量
    	num += 10;
    	return num;
    }
    var num = 10;
    var res = add(10);
    alert(num); // 输出10，没有变化
    alert(res); //输出20
    ```

  - 引用类型的传递规如下

    ```javascript
    function setName(obj){
    	obj.name = "ssss";
    }
    var person = new Object();
    setName(person);
    alert(person.name); // "ssss"
    ```

  - 对象也是按值传递的

    ```javascript
    function setName(obj){
    	obj.name = "ssss";
    	obj = new Object(); // 这里改变了对象的指向
    	obj.name = "aaaa";
    }
    var person = new Object();
    setName(person);
    alert(person.name); // 输出"ssss"
    ```

  - 可以把JavaScript函数的参数想象成为局部变量

- 类型检测

  - 用typeof检测null和引用类型对象都会返回object

  - 在检测引用类型的值时，当我们需要检测它是什么类型的对象时，可以使用instanceof

    ```javascript
    result = variable instanceof constructor // 使用格式 会返回一个Boolean类型的值
    
    alert(person instanceof Object); // person是Object吗
    alert(colors instanceof Array);  // colors是Array吗
    alert(pattern instanceiof RegExp);  // pattern是RegExp吗
    // 根据规定，所有引用类型都是Object，使用instanceof都会返回true
    ```

## 4.2  执行环境和作用域

- 每一个执行环境都对应一个变量对象，在环境中定义的使用变量和函数都会保存在这个对象中我们无法访问这个对象，但是解析器在后台会使用它

- 全局执行环境是最外围的一个执行环境，在web浏览器中，全局执行环境被认为是window对象

- 当这个环境对象中的代码执行完毕后，这个环境对象也会被销毁。全局执行环境直到网页被关闭后才会被销毁

- 每个函数都会有自己的执行环境，后台用堆栈实现

- 当代码在一个环境中执行时，会创建变量对象的一个作用链，对执行环境有权访问的所有变量和函数的有序访问

- 作用链的最前端时当前环境对象，最末段是全局对象。在访问变量或者函数是，会一层层的去查询。找不到会报错

  ```JavaScript
  
  var color = "bule";
  function changeColor(){
  	if(color == "blue"){
  		color = "red";
  	}else color = "blue";
  }
  changeColor();
  
  alertColor();
  alert("Color is now" + color); 
  // 该程序中访问color时的作用链有两个元素，函数自己的变量对象（包含arguments对象）和全局变量对象。color在全局变量中找到
  ```

- 局部作用域定义的变量可以在基本环境与全局变量互换使用

  ![image-20210127131019565](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210127131019565.png)

- 以上程序的作用链如下图

  ![image-20210127131059632](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210127131059632.png)

- 内部环境可以通过作用链访问所有的外部环境。但是外部环境不能访问内部环境的任何变量和函数。这些环境的联系是线性的，有次序的

- 延长作用链：有一些语句可以在作用链前端添加一个变量对象，这个变量是临时的

  - try-catch语句和catch块
  - with语句

- 没有块级作用域

  - JavaScript没有块级作用域

    ```javascript
    if(true){
    	var color = "blue"; // 这个变量被定义在了全局环境中
    }
    alert(color); // "blue"
    
    for(var i = 0;i < 10;i++){ // 这个i是定义在全局环境中的
    	doSomething(i);
    }
    alert(i); // 10
    ```

- 声明变量

  - var声明的变量会被自动添加到最接近的环境中，在with语句中最接近的环境就是函数环境

    如果一个变量没有用var声明，那么该变量贵被添加到全局变量中

  - 在JavaScript中不推荐不声明变量就直接使用，在严格模式下这样的操作会直接报错

- 查询标识符

  ```javascript
  var color = "blue";
  function getcolor(){
  	return color;
  }
  
  ```

## 4.3  垃圾收集

- Javascript有自动垃圾收集机制，垃圾收集器会安装固定时间间隔周期性的执行这一操作。
- 使用标记来标记无用的变量，具体实现一共有两种方法
  - 标记清除：这是JavaScript中最常用的方式
  - 引用计数：追踪每一个变量使用的次数
- 性能问题：不推荐自己调用垃圾回收
- 内存管理：
  - 分配给web浏览器的的内存一般比桌面应用的更多，这是出于安全性的考虑
  - 解除引用不意味着马上回收，解除引用的真正作用是为了让值脱离执行环境

