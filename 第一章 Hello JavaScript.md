# 第一章 Hello JavaScript

- 当浏览器读取到script元素之后，不会以XHTML或者HTML的方式去接管，而是由浏览器的脚本引擎去接管script元素中的代码

- MIME编码可以去识别内容如何编码和指定格式的方式

- 早期的script标签还有language属性，用来表示语言的类型和版本，是一种跨浏览器技术

- script标签的charset可以用来脚本的字符编码集

- 将defer属性设置为”defer“可以加快浏览器的加载速度

- 将脚本放在最末端在一定程度上可以加快浏览器载入的速度，但是可维护性和可读性在一定程度上会变差

- 不是所有的浏览器都支持javascript

- ```javascript
   function hello(params) { // 定义了函数
         ....
      }
  ```

- 事件处理程序

  - onclick 鼠标单击事件
  - onmouseover 当鼠标悬停在某个元素上事件触发
  - onmouseout 当鼠标离开是触发
  - onfocus 当某个元素获取焦点是触发
  - onblur 当某个元素失去焦点时触发

- document可以表示页面上所有的元素

- document包含映射到页面上的集合，还提供了访问和修改网页的方法

- document的open方法可以打开要修改的HTML页面。

- writeln是write方法的变种，可以输出文本字符串到页面中。但是writeln可以输出后自动换行。close方法用来关闭文档。

- document对象是浏览器内置对象结构是BOM对象的一部分。

  