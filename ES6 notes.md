# ES6 notes

## 一、变量

### 1.1 let

- 声明变量
  - 变量不能重复声明
  - 块级作用域 全局，函数，eval
  - 不存在变量提升
  - 不影响作用域链

### 1.2 const

定义常量

- 一定要赋初始值
- 一般常量使用大写（潜规则）
- 常量值不能修改
- 块级作用域
- 对于数组和对象的元素修改，不算做对常量的修改，不会报错（指向的地址没有发生变化）

### 1.3 变量的解构赋值

- es6允许按照一定模式从数组和对象中提取值，对变量进行赋值，被称为解构赋值

- 数组的结构

  ```javascript
  const F4 = ['小沈阳','刘能','赵四','宋小宝'];
  let [xiao,liu,zhao,song] = F4;
  console.log(xiao);
  console.log(liu);
  console.log(zhao);
  console.log(song);
  ```

### 1.4 模板字符串

ES6 引入新的声明字符串的方式 [``] ' '  " "

- 声明

  ```js
  let str = `我也是一个字符串`
  ```

- 内容中可以直接出现换行符

- 变量拼接

  ```js
  let lovest = '魏翔'
  let out = `${lovest}是我心中的演员！`
  ```

### 1.5 简化对象写法

ES6中 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法，这样的书写更加简洁

```js
let name = 'zhangsan'
let change = function(){
	console.log('gaibianziji')
}
const school = {
    name,
    change,
    improve(){//函数声明不用写 :function
        console.log('womenkeyitigaojineng')
    }
}
```

### 1.6 箭头函数

=> 定义函数

- this 是静态的 ，this 始终是指向函数声明时所在作用域下的this的值  

- 不能作为构造实例化对象

  ```js
  let Person = (name,age)=>{
  	this.name = name;
  	this.age = age;
  }//错误的
  ```

- 不能使用 arguments 变量

- 箭头函数的简写

  - 省略小括号，当形参有且只有一个的时候

    ```js
    let add = n =>{
    	return n + n;
    }
    ```

  - 省略花括号，当代码体只有一条语句的时候，此时 return 必须省略，而且语句的执行结果就是函数的返回值

    ```js
    let pow = (n) => n*n;
    console.log(pow(8))//64
    ```

- 箭头函数适合与this无关的回调：定时器，数组的方法回调

- 箭头函数不适合与this 有关的回调，事件回调，对象的方法

### 1.7 函数参数的默认值设置

ES6允许给函数参数赋值初始值

- 形参初始值

  - 具有默认值的参数，一般位置都要靠后（潜规则）

- 与解构赋值结合

  ```js
  function connect({host="127.0.0.1",username,password,port}){
  	console.log(host)
      console.log(username)
      console.log(password)
      console.log(port)
  }
  connect({
      host:'atguigu'
      username:'root'
      password:'root'
      port:3304
  })
  ```

- ES6 引入rest 参数，用于获取函数的实参，用来代替arguments

  - ES5获取实参的方式

    ```js
    function data(){
    	console.log(arguments)
    }
    data('baizhi','ajiao','sihui')
    ```

  - rest参数

    ```js
    function data(...args){
    	console.log(args)
    }
    data('ajiao','baizhi','sihui')
    //返回的是一个数组，可以用数组的api
    ```

  - rest参数 必须要放到参数的最后

### 1.8 扩展运算符

... 扩展运算符能将[数组]转换为逗号分隔的[参数序列]

```js
const tfboys = ['yiyang','wangyuan','wangjuekai']
function chunwan(){
	console.log(arguments)
}
chunwan(...tfboys);//chunwan('yiyang','wangyuan','wangjuekai')
```

- 应用
  - 数组的合并
  - 数组的克隆
    - 浅拷贝
  - 将伪数组转换为真正的数组



## 二、Symbol

### 2.1 基本使用

- symbol特点
  - Symbol 的值是唯一的，用来解决命名冲突的问题
  - Symbol 值不能与其他数据进行运算
  - Symbol 定义的对象属性不能使用for…in 循环遍历 ，但是可以使用Reflect.ownKeys 来获取对象的所有键名
  - 注意：
    - 遇到唯一性的场景时要想到 Symbol

- Symbol内置值
  - Symbol.hasInstance 当其他对象使用 instanceof 运算符，判断是否为该对
    象的实例时，会调用这个方法
  - Symbol.isConcatSpreadable 对象的 Symbol.isConcatSpreadable 属性等于的是一个
    布尔值，表示该对象用于 Array.prototype.concat()时，
    是否可以展开。
  - Symbol.species 创建衍生对象时，会使用该属性
  - Symbol.match 当执行 str.match(myObject) 时，如果该属性存在，会
    调用它，返回该方法的返回值。
  - Symbol.replace 当该对象被 str.replace(myObject)方法调用时，会返回
    该方法的返回值。
  - Symbol.search 当该对象被 str.search (myObject)方法调用时，会返回
    该方法的返回值。
  - Symbol.split 当该对象被 str.split(myObject)方法调用时，会返回该
    方法的返回值。
  - Symbol.iterator 对象进行 for...of 循环时，会调用 Symbol.iterator 方法，
    返回该对象的默认遍历器
  - Symbol.toPrimitive 该对象被转为原始类型的值时，会调用这个方法，返
    回该对象对应的原始类型值。
  - Symbol. toStringTag 在该对象上面调用 toString 方法时，返回该方法的返
    回值
  - Symbol. unscopables 该对象指定了使用 with 关键字时，哪些属性会被 with
    环境排除。

## 三、迭代器

遍历器（Iterator）就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作。

- ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 循环
- 原生具备iterator接口的数据（可用for...of 遍历）
  - Array
  - Arguments
  - Set
  - Map
  - String
  - TypedArray
  - NodeList
- 工作原理
  - 创建一个指针对象，指向当前数据结构的起始位置
  - 第一次调用对象的 next 方法，指针自动指向数据结构的第一个成员
  - 接下来不断调用 next 方法，指针一直往后移动，直到指向最后一个成员
  - 每调用 next 方法返回一个包含 value 和 done 属性的对象
- 注意：
  - 需要自定义遍历数据的时候，要想到迭代器。

## 四、生成器

生成器函数是es6提供的 一种异步编程解决方案，语法行为与传统函数完全不同，是一种特殊的函数

```js
function * gen(){
	yield 'yizhimeiyouerduo'
    yield 'yizhimeiyouweiba'
    return 'zhenqiguai'
}
let iterator = gen()
console.log(iterator.next)
console.log(iterator.next)
console.log(iterator.next)
```

- 说明
  - *的位置没有限制
  - 生成器函数返回的结果是迭代器对象，调用迭代器对象的 next 方法可以得到yield 语句后的值
  - yield 相当于函数的暂停标记，也可以认为是函数的分隔符，每调用一次 next方法，执行一段代码
  - next 方法可以传递实参，作为 yield 语句的返回值

## 五、Promise

Promise 是 ES6 引入的**异步编程**的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

- Promise 构造函数: Promise (excutor) {}
- Promise.prototype.then 方法
- Promise.prototype.catch 方法

### 5.1 then

- 调用then方法，then方法的返回结果是promise对象，对象状态由回调函数的执行结果决定
  - 如果回调函数中返回的结果是 非promise类型的属性，状态为成功，返回值为对象的成功的值
- 满足链式调用

## 六、Set

- ES6 提供了新的数据结构 Set（集合）。它类似于数组，但成员的值都是唯一的，集合实现了 iterator 接口，所以可以使用『扩展运算符(...)』和『for…of…』进行遍历，集合的属性和方法：
  - size 返回集合的元素个数
  - add 增加一个新元素，返回当前集合
  - delete 删除元素，返回 boolean 值
  - has 检测集合中是否包含某个元素，返回 boolean 值
  - clear 清空集合，返回 undefined

## 七、Map

- ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map 也实现了terator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历。Map 的属性和方法：
  - size 返回 Map 的元素个数
  - set 增加一个新元素，返回当前 Map
  - get 返回键名对象的键值
  - has 检测 Map 中是否包含某个元素，返回 boolean 值
  - clear 清空集合，返回 undefined

## 八、class类

- ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。基本上，ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
- 构造方法，constructor名字不能修改
- static标注的属性和方法属于类而不属于实例化对象

## 九、数值扩展

### 9.1 八进制和二进制

ES6 提供了二进制和八进制数值的新的写法，分别用前缀 0b 和 0o 表示。

### 9.2 数值相关方法

- Number.isFinite() 用来检查一个数值是否为有限的
- Number.isNaN() 用来检查一个值是否为 NaN
- Number.parseInt() 与 Number.parseFloat()
  - ES6 将全局方法 parseInt 和 parseFloat，移植到 Number 对象上面，使用不变。
- Math.trunc()用于去除一个数的小数部分，返回整数部分。
- Number.isInteger() 用来判断一个数值是否为整数

## 十、对象扩展

- Object.is 比较两个值是否严格相等，与『===』行为基本一致（+0 与 NaN）
- Object.assign 对象的合并，将源对象的所有可枚举属性，复制到目标对象
- setPrototypeOf 可以直接设置对象的原型，getPrototypeOf获取

## 十一、模块化

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来。

### 11.1 模块化的好处

- 防止命名冲突
- 代码复用
- 高维护性

### 11.2 ES6模块化语法

- 模块功能主要由两个命令构成：export和import
  - export 命令用于规定模块的对外接口
  - import 命令用于输入其他模块提供的功能

- 暴露数据的方式

  - 分别暴露

    ```js
    export let school = '四川大学'
    export function teach(){
        console.log('我们可以教你技能')
    }
    ```

  - 统一暴露

    ```js
    let school = '四川大学'
    function findYou(){
    	console.log('找到你')
    }
    export{school,findYou}
    ```

  - 默认暴露

    ```js
    export default{
    	school:'四川大学',
    	change:function(){
    		console.log('改变自己')
    	}
    }
    ```

- 引入模块数据

  - 通用的导入方式

    ```js
    import * as m1 from "./src/js/m1.js"
    ```

  - 解构赋值形式

    ```js
    import {school,teach} from "./src/js/m1.js"
    import {school as guigu,findYou} from "./src/js/m2.js"
    import {default as m3} from "./src/js/m3.js"
    ```

  - 简便形式——针对默认暴露

    ```js
    import m3 from "./src/js/m3.js"
    ```

- 引入模块化的方式二

  ```js
  <script src="./src.js.app.js" type = "module"></script>
  ```

### 11.3 ES6模块代码转换

- 安装工具 babel-cli  babel-preset-env  browserify(webpack)
- npx babel src/js -d dist/js
- 打包 npx browserify dist/js/app.js -o dist/bundle.js

## 十二、ES8新特性

### 12.1 async 和 await

- async 函数
  - async 函数的返回值为 promise 对象
  - promise 对象的结果由 async 函数执行的返回值决定
- await 表达式
  - await 必须写在 async 函数中
  - await 右侧的表达式一般为 promise 对象
  - await 返回的是 promise 成功的值
  - wait 的 promise 失败了, 就会抛出异常, 需要通过 try...catch 捕获处理
- 对象方法扩展
  - Object.values 和 Object.entries
    - Object.values()方法返回一个给定对象的所有可枚举属性值的数组
    - Object.entries()方法返回一个给定对象自身可遍历属性 [key,value] 的数组
  - Object.getOwnPropertyDescriptors
    - 该方法返回指定对象所有自身属性的描述对象

## 十三、ES9的新特性

### 13.1 扩展运算符与rest参数

- Rest 参数与 spread 扩展运算符在 ES6 中已经引入，不过 ES6 中只针对于数组，
  在 ES9 中为对象提供了像数组一样的 rest 参数和扩展运算符

### 13.2 命名捕获分组

- ES9 允许命名捕获组使用符号『?<name>』,这样获取捕获结果可读性更强

  ```javascript
  let str = '<a href="http://www.atguigu.com">尚硅谷</a>'
  const reg = /<a href="(?<url>.*)">(?<text>.*)<\/a>/
  const result = reg,exec(str)
  console.log(result.groups.url)
  console.log(result.groups.text)
  ```

### 13.3 反向断言

- ES9 支持反向断言，通过对匹配结果前面的内容进行判断，对匹配进行筛选。

  ```js
  //声明字符串
  let str = 'JS5211314 你知道么 555 啦啦啦'
  //正向断言
  const reg = /\d+(?=啦)
  const result = reg.exec(str)
  //反向断言
  const reg = /(?<=么)\d+/
  const result = reg.exec(str)
  console.log(result)
  ```

### 13.4 dotAll模式

- 正则表达式中点.匹配除回车外的任何单字符，标记『s』改变这种行为，允许行
  终止符出现

  ```js
  let str = `
  <ul>
  	<li>
   		<a>肖生克的救赎</a>
   		<p>上映日期: 1994-09-10</p>
   	</li>
   	<li>
   		<a>阿甘正传</a>
   		<p>上映日期: 1994-07-06</p>
   	</li>
  </ul>`;
  //声明正则
  const reg = /<li>\s+<a>(.*?)<\/a>\s+<p>(.*?)<\/p>/;
  //加/s，g表示全局
  const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs;
  //执行匹配
  const result = reg.exec(str);
  let result;
  let data = [];
  while(result = reg.exec(str)){
   
  data.push({title: result[1], time: result[2]});
  }
  //输出结果
  console.log(data);
  ```

## 十四、ES11 新特性

- 私有属性

