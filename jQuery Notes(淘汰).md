# jQuery Notes

## 一、jQuery概述

### 1.1 JavaScript库

- 常见的JavaScript库

  - jQuery
  - prototype
  - YUI
  - Dojo
  - Ext JS
  - 移动端的zepto

  这些库都是对原生的JavaScript的封装，内部都是用JavaScript实现的

### 1.2 jQuery的概念

- jQuery是一个快速的，简洁的JavaScript库，设计宗旨就是“write less，Do More”，即倡导写更少的代码，做更多的事情

  j就是JavaScript；

  query 查询；

  把js中的dom操作做了封装，我们可以快速的查询使用里面的功能

- jQuery封装了JavaScript常用的功能代码，优化了dom操作，事件处理，动画设计和Ajax交互

- 学习jQuery本质：就是学习调用这些函数（方法）

- jQuery加快了开发速度，可以非常方便的调用和使用他

### 1.3 jQuery的优点

- 轻量级
- 跨浏览器兼容
- 链式编程，隐式迭代
- 对事件、样式、动画支持，大大简化了dom操作
- 支持插件扩展开发，有着丰富的第三方插件

## 二、jQuery的基本使用

### 2.1 jQuery的入口函数

```javascript
$(function(){
    ...//此处是页面dom加载完成的入口
})
```

```javascript
$(document).ready(function(){
    ...//此处是页面dom加载完成的入口
})
```

- 等着dom结构渲染完毕即可执行内部代码，不惜等到所有外部资源加载完成，jQuery帮我们完成了封装（推荐）
- 相当于原生js中的DOMContentLoaded
- 不同于原生js中的load事件是等页面文档、外部的js文件、css文件、图片加载完毕才执行内部代码

### 2.2 jQuery的顶级对象$

- $是jQuery的别称，在代码中可以使用jQuery代替$，但一般为了方便，通常都直接使用$
- $是jQuery的顶级对象，相当于原生JavaScript中的window，把元素利用$包装成jQuery对象，就可以调用jQuery的方法

### 2.3 jQuery对象和DOM对象

- 用原生js获取来的对象就是dom对象

- jQuery方法获取的元素就是jQuery对象

  - jQuery对象本质是：利用$对dom对象包装后产生的对象（伪数组形式存储）

- 注意：

  - jQuery对象只能使用jQuery方法，DOM对象则使用原生的JavaScript属性和方法
  - jQuery对象不能使用js的属性和方法

- DOM对象与jQuery对象之间是可以相互转换的

  - 因为原生js比jQuery更大，原生的一些属性和方法jQuery没有给我们封装，要想使用这些方法和属性就需要把jQuery对象转换为DOM对象才能使用

  - DOM对象转换为jQuery对象：$(DOM对象)

    ```javascript
    $('div')
    ```

  - jQuery对象转换为DOM对象（两种方式）

    ```javascript
    $('div')[index] //index是索引号
    ```

    ```javascript
    $('div').get(index) //index是索引号
    ```

## 三、jQuery选择器

### 3.1 基础选择器

原生js获取元素方式很多，很杂，而且兼容性情况不一致，因此jQuery给我们做了封装，是获取元素统一标准

```javascript
$("选择器") //里面选择器直接写css选择器即可，但是要加引号
```

### 3.2 jQuery设置样式

```javascript
$('div').css('属性'，'值')
```

### 3.3 隐式迭代（重要）

- 遍历内部DOM元素（伪数组形式存储）的过程叫做隐式迭代
- 理解：
  - 给匹配到的所有元素进行循环遍历，执行相应的方法，而不是我们再进行循环，简化我们的操作，方便我们调用
  - 隐式迭代就是把匹配的所有元素内部进行循环遍历，给每一个元素添加css这个方法

### 3.4 jQuery筛选选择器

<img src="C:\Users\Tan\AppData\Roaming\Typora\typora-user-images\image-20210301102723939.png" alt="image-20210301102723939" style="zoom:50%;" />

## 四、jQuery 样式操作

### 4.1 操作css方法

jQuery可以使用css方法来修改简单元素样式；也可以操作类，操作多个样式

- 参数值写属性名，则是返回属性值

  ```javascript
  $(this).css('color');
  ```

- 参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号

  ```javascript
  $(this).css('color','red');
  ```

- 参数可以是对象形式，方便设置多组多组样式，属性名和属性值冒号隔开，属性可以不用加引号

  ```javascript
  $(this).css({'color':'white','font-size':'20px'});
  ```


### 4.2 类操作与className区别

- 原生js中className会覆盖元素原先里面的类名
- jQuery里面类操作只会对指定类进行操作，不影响原先的类名

## 五、jQuery效果

### 5.1 显示隐藏效果

- 显示语法规范

  ```javascript
  show([speed,[easing],[fn]])
  ```

- 显示参数

  - 参数可以省略，无动画直接显示
  - speed：三种预定速度之一的字符串("slow","normal","fast")或者标识动画时长的毫秒数值(如：1000)
  - easing：（Optional）用来指定切换效果，默认是“swing”，可用参数“linear”
  - fn：回调函数，在动画完成时执行的函数，每个元素执行一次

### 5.2 动画队列及其停止排队的方法

- 动画或效果队列
  - 动画或者效果一旦出发就会执行，如果多次触发，就会造成多个动画画着效果排队执行
- 停止排队
  - stop() 方法用于停止动画或效果
  - 注意：stop()写到动画或者效果的前面，相当于停止结束上一次的动画

### 5.3 自定义动画animate

- 语法

  ```javascript
  animate(params,[speed],[easing],[fn])
  ```

- 参数

  - params：想要更改的样式属性，以对象形式传递，必须写，属性名可以不用带引号，如果是符合属性则需要采取驼峰命名法（borderLeft）其余参数都可以省略
  - speed：三种预定速度之一的字符串("slow","normal","fast")或者标识动画时长的毫秒数值(如：1000)
  - easing：（Optional）用来指定切换效果，默认是“swing”，可用参数“linear”
  - fn：回调函数，在动画完成时执行的函数，每个元素执行一次