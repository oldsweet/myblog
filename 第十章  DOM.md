# 第十章 	DOM

- 本章内容
  - 理解包含不同层次节点的DOM
  - 使用不同的节点类型
  - 克服浏览器兼容性问题的各种陷阱
- DOM是针对htl和xml文档的一个api，他描绘了一个层次化的一个节点树。

## 10.1 节点层次

​	DOM可以将任何html或xml文档描绘成为一个由多层节点构成的结构

- 文档节点是每个节点的根节点。

### 10.1.1 Node类型

每一个节点都有一个nodetype属性。用来表明节点的类型。节点裂隙由在node类型中定义的下列12个数值常量来表示

![image-20210228154405733](C:\Users\Libaisonm\AppData\Roaming\Typora\typora-user-images\image-20210228154405733.png)

通过比较上面这些常量，可以很容易确定节点的类型

```javascript
 window.onload = function(){
        if(document.getElementsByClassName('box')[0].nodeType == 1){
            alert('this is a node');
        }
     }
```

1. nodeName 和 nodeValue属性

   要了解节点的具体信息。可以使用nodeName和NodeValue这两个属性。

   ```javascript
    var someNode = document.getElementsByClassName('box')[0];
          alert(someNode.nodeName); // 这样可以获取到节点的名称（大写表示)
          alert(someNode.nodeValue); // 元素节点nodename保存的都是null
   ```

2. 节点关系

   - 每个节点都有一个childNodes属性