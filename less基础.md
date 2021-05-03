# less基础

less是一种动态样式语言，属于css预处理器的范畴，它扩展了css语言

增加了变量，Mixin（混合） 、函数等特性，使css 更易维护和扩展

less 既可以在客户端上运行，也可以借助node.js在服务器端运行



less的中文官网：http://lesscss.cn/

bootstrap中less教程：http://www.bootcss.com/p/lesscss/



less编译工具

​	koala 官网：www.koala-app.com

## 一、less中的注释

- 以 // 开头的注释，不会被编译到css文件中
- 以/**/包裹的注释会被编译到css文件中

## 二、变量

- 使用@来声明一个变量：@pink：pink
  - 作为普通属性值来使用：直接使用@pink
  - 作为选择器和属性名：#@{selector的值} 的形式
  - 作为url：@{url}
  - 变量的延迟加载（特殊）
    - 按照作用域加载，变量全部解析完在进行赋值 

## 三、less的嵌套规则

- 基本嵌套规则
- &的使用（代表平级）

## 四、less的混合

混合就是将一系列属性从一个规则集引入到另一个规则集的方式

- 普通混合

- 不带输出的混合

- 带参数的混合

- 带参数并且有默认值的混合

- 带多个参数的混合

- 命名参数

- 匹配模式

  ```less
  .triangle(@_){//@_ 匹配模式，调用.triangle时，每次都先执行@_参数的triangle
      width: 0px;
      height: 0px;
      overflow: hidden;
  }
  
  .triangle(T,@c,@w){
      border-width: @w;
      border-style: dashed dashed solid dashed;
      border-color: transparent transparent @c transparent;
  }
  ```

- arguments变量

  ```less
  .border(@w,@style,@c){
  	border:@arguments
  }
  #wrap .sjx{
      .border(1px,solid,black)
  }
  ```


## 五、less计算

less可以在编辑阶段就进行数值计算，从而不需要引用calc命令在运行时计算，提高效率

## 六、less的避免编译

```less
padding(~"cacl(100px + 100)");
```

**切记：变量在less中属于块级作用域，延迟加载**

## 七、less总结

- 变量
  - @
  - 变量的延迟加载
  - 变量是块级作用域

- 嵌套
  - &：平级

- 混合
  - 将一系列的规则集引入到另一个规则集中
  - 混合的定义在less规则中有明确的指定，使用 . 的形式来定义
  - 普通混合
    - 编辑到原生css中
  - 不带输出的混合
    - 加双括号
  - 带参数的混合
    - 带默认值的混合
  - 匹配模式
  - arguments

- 计算
  - 加减乘除
  - 计算的一方带单位就可以

- 继承

  - 性能比混合高
  - 灵活度比混合低

