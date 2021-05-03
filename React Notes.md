# React Notes



## 一、React简介

### 1.1 官网

- 英文官网:[ https://reactjs.org/](https://reactjs.org/)
- 中文官网: https://react.docschina.org/

### 1.2 介绍

- 用于动态构建用户界面的 JavaScript 库(只关注于视图)
- 由Facebook开源

### 1.3 React的特点

- 声明式编码
- 组件式编码
- React Native编写原生应用
- 高效（优秀的Diffing算法）

### 1.4 React高效的原因

- 使用虚拟(virtual)DOM，不总是直接操作页面真实DOM
- DOM Diffing算法, 最小化页面重绘

## 二、React基本使用

### 2.1 相关js库

- react.js：React核心库

- react-dom.js：提供操作DOM的react扩展库

- babel.min.js：解析JSX语法代码转为JS代码的库

  ```javascript
  <!--引入react核心库-->
  <script type="text/javascript" src="../js/react.development.js"></script>
  <!--引入react-dom，用于支持react操作dom-->
  <script type="text/javascript" src="../js/react-dom.development.js"></script>
  <!--引入Babel，用于将jsx转换为js-->
  <script type="text/javascript" src="../js/babel.min.js"></script>
  ```


### 2.2 虚拟dom与真实dom

- React提供一些特殊的api来创建一些特殊的js对象

  ```javascript
  const dom = React.createElement('h1',{h1:'title','Hello React'})
  ```

  - 上面创建的就是一个简单的虚拟dom对象

- 虚拟DOM对象最终会被React转换为真实DOM

- 编码时基本只需要操作react的虚拟DOM相关数据，react会转换为真实DOM

- 虚拟DOM比较“轻”，真实DOM比较“重“，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性

### 2.3 jsx语法规则

全称为 JavaScript XML

- 定义虚拟DOM，不要写引号
- 标签中混入js表达式时要用{}
- 样式的类名指定不要用class，要用className
- 内联样式，要用style={{key:vlaue}}的形式去写
- 虚拟DOM只有一个根标签
- 标签必须闭合
  - 若小写字母开头，则将该标签转为html中的同名元素，若html中无该标签对应的同名元素，则报错
  - 若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错
- 基本语法规则
  - 遇到 <开头的代码, 以标签的语法解析: html同名标签转换为html同名元素, 其它标签需要特别解析
  - 遇到以 { 开头的代码，以JS语法解析: 标签中的js表达式必须用{ }包含
- babel.js的作用
  - 浏览器不能直接解析JSX代码, 需要babel转译为纯JS的代码才能运行
  - 只要用了JSX，都要加上**type="text/babel"**, 声明需要babel来处理

### 2.4 模块与组件、模块化与组件化

- 模块
  - 理解：向外提供特定功能的js程序, 一般就是一个js文件
  - 作用：复用js, 简化js的编写, 提高js运行效率
- 组件
  - 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)
  - 为什么要用组件： 一个界面的功能更复杂
  - 作用：复用编码, 简化项目编码, 提高运行效率

## 三、React面向组件编程

### 3.1 基本理解和使用

- 组件名必须首字母大写
- 虚拟DOM元素只能有一个根元素
- 虚拟DOM元素必须有结束标签

### 3.2渲染类组件标签的基本流程

- React内部会创建组件实例对象
- 调用render()得到虚拟DOM，并解析为真实DOM
- 插入到指定的页面元素内部

### 3.3 组件三大核心属性

#### 3.3.1 state

- 理解

  - state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)
  - 组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

- 强烈注意：

  - 组件中`render`方法中的`this`为组件实例对象

  - 组件自定义的方法中this为undefined，如何解决？

    - 强制绑定this: 通过函数对象的bind()方法

    - 箭头函数(必须写成赋值语句＋箭头函数的形式，箭头函数会放在实例自身上)

  - 状态数据，不能直接修改或更新(setState())

#### 3.3.2 props

- 理解	

  - 每个组件对象都会有`props`(properties的简写)属性
  - 组件标签的所有属性都保存在`props`中

- 作用

  - 通过标签属性从组件外向组件内传递变化的数据
  - 注意: 组件内部不要修改props数据

- 编码操作

  - 对props中的属性值进行类型限制喝必要性限制

    - 第一种方式（react v15.5 开始弃用）

    ```javascript
    Person.propTypes = {
     name: React.PropTypes.string.isRequired,
     age: React.PropTypes.number
    }
    ```

    - 第二种方式(需要引入`prop-types`库)，新方式

    ```javascript
    Person.propTypes = {
      name: PropTypes.string.isRequired,
      age: PropTypes.number. 
    }
    ```


#### 3.3.3 refs

- 理解：组件内的标签可以定义ref属性来标识自己

- 编码

  - 第一种形式：字符串形式的ref(效率低，可能考虑后期版本将其移除)

    ```javascript
    <input ref="input1"/>
    ```

  - 第二种形式：回调形式的ref（会将input1直接以属性的形式存放在实例自身上，调用时也是直接调用this，实例自身）

    ```javascript
    <input ref={c=>{this.input1 = c}}>
    ```

    - 关于回调refs的说明

      如果 `ref` 回调函数是以内联函数的方式定义的，在更新过程中它会被执行两次，第一次传入参数 `null`，然后第二次会传入参数 DOM 元素。这是因为在每次渲染时会创建一个新的函数实例，所以 React 清空旧的 ref 并且设置新的。通过将 ref 的回调函数定义成 class 的绑定函数的方式可以避免上述问题，但是大多数情况下它是无关紧要的。

  - 第三种形式：reateRef创建ref容器（推荐）

    ```javascript
    myRef = React.createRef()
    <input ref={this.myRef}/>
    ```

    - 说明：

      React.createRef调用后可以返回一个容器，该容器可以存储被ref所标识的节点，该容器是“专人专用的”，也是目前react最推荐的一种方式

### 3.4 事件处理

- 通过onXxx属性指定事件处理函数(注意大小写)

  - React使用的是自定义(合成)事件, 而不是使用的原生DOM事件——为了更好的兼容性

  - React中的事件是通过事件委托方式处理的(委托给组件最外层的元素)——为了更高效
- 通过event.target得到发生事件的DOM元素对象——不要过度的使用ref

### 3.5 高阶函数及函数柯里化

#### 3.5.1 高阶函数

- 如果一个函数符合下面两个规范的其中一个，那么该函数就是高阶函数
  - 若A函数，接受的参数是一个函数，那么A就可以称之为高阶函数
  - 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数
  - 常见的高阶函数有：
    - Promise
    - setTimeout
    - arr.map()

#### 3.5.2 函数的柯里化

- 通过函数调用继续返回函数的方式，实现多次接受参数最后统一处理的函数编码形式

### 3.6 组件的生命周期

#### 3.6.1 生命周期流程图

<img src="C:\Users\Tan\AppData\Roaming\Typora\typora-user-images\image-20210325161829059.png" alt="image-20210325161829059"  />

#### 3.6.2 生命周期的三个阶段（旧）

- 初始化阶段：由ReactDOM.render()触发---初次渲染
  - onstructor()
  - componentWillMount()
  - render()
  - componentDidMount() ===>常用
    - 一般在这个钩子中做一些初始化的事儿，例如：开启定时器，发送网络请求、订阅消息
- 更新阶段由组件内部this.setSate()或父组件重新render触发
  - shouldComponentUpdate()
  - componentWillUpdate()
  - render() ====>必须使用的一个
  - componentDidUpdate()
- 卸载组件：由ReactDOM.unmountComponentAtNode()触发
  - componentWillUnmount() ===>常用
    - 一般在这个钩子中都是做一些收尾的事儿，例如：关闭定时器，取消订阅消息

#### 3.6.3 生命周期的三个阶段（新）

<img src="C:\Users\Tan\AppData\Roaming\Typora\typora-user-images\image-20210325172343187.png" alt="image-20210325172343187" style="zoom:80%;" />

- 初始化阶段：由ReactDOM.render()触发---初次渲染
  - constructor()
  - getDerivedStateFromProps
  - render()
  - componentDidMount()

- 更新阶段： 由组件内部this.setSate()或父组件重新render触发
  - getDerivedStateFromProps
  - shouldComponentUpdate()
  - render()
  - getSnapshotBeforeUpdate
  - componentDidUpdate()
- 卸载组件：由ReactDOM.unmountComponentAtNode()触发
  - componentWillUnmount()

#### 3.6.4 重要的钩子

- render():初始化渲染或更新渲染调用
- componentDidMount:开启监听，发送ajax请求，设置定时器
- componentWillUnmount:做一些收尾工作，如：清理定时器

#### 3.6.5 即将废弃的钩子

- componentWillMount
- componentWillReceiveProps
- componentWillUpdate

现在使用会出现警告，下一个大版本需要加上UNSAFE_前缀才能使用，以后可能会被彻底废弃，不建议使用

### 3.7 DOM的Diffing算法

- 最小单元是span
- 分层次对比

#### 3.7.1 key的原理与使用

经典面试题：

​	1）react/vue 中的key有什么作用？（key的内部原理是什么）

​	2）为什么遍历列表时，key最好不要用index？

- 虚拟dom中key的作用：
  - 简单地说：key是虚拟dom对象的标识，在更新显示时，key起着极其重要的作用
  - 详细的说：当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟dom】，随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：
    - a. 旧虚拟dom中找到了与新虚拟dom相同的key：
      - 若虚拟dom中内容没有改变，直接使用之前的真是dom
      - 若虚拟dom中内容变化了，则生成新的真是dom，随后替换掉页面中跟之前的真是dom
    - b. 旧虚拟DOM中未找到与新虚拟DOM相同的key
      - 根据数据创建新的真实DOM，随后渲染到页面
- 用index作为key可能会引发的问题
  - 若对数据进行：逆序添加、逆序删除等破坏顺序操作：
    - 会产生没有必要的真实DOM更新 ==> 界面效果虽然没有问题，但是效率低下
  - 如果界面中还包含输入类 的DOM：（例如input框）
    - 会产生错误DOM更新 ==> 界面出现问题
  - 注意！
    - 如果不存在数据对对象的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的
- 开发中，该如何选择key？
  - 最好使用每条数据的唯一标识作为key，比如iid、手机号、身份证号 、学号等唯一值。
  - 如果确定只是简单的展示数据，那么我们选择用index也是可以的

## 四、React应用(基于react脚手架)

### 4.1 创建

使用create-react-app 创建react应用

### 4.2 react脚手架

- 脚手架: 用来帮助程序员快速创建一个基于xxx库的模板项目
  - 包含了所有需要的配置（语法检查、jsx编译、devServer…）
  - 下载好了所有相关的依赖
  - 可以直接运行一个简单效果
-  react提供了一个用于创建react项目的脚手架库: create-react-app
-  项目的整体技术架构为: react + webpack + es6 + eslint
- 使用脚手架开发的项目的特点: 模块化, 组件化, 工程化

### 4.3创建项目并启动

- 第一步：全局安装：npm -i create-react-app
- 第二步：切换到想创建项目的目录，使用命令：create-react-app hello-react
- 第三步：进入项目文件夹： cd hello-react
- 第四步：启动项目：npm start

### 4.4 react脚手架项目结构

- public----静态资源文件夹
  - favicon.icon ---网站页签图标
  - index.html --- 主页面
  - nabifest.json --- 应用加壳的配置文件
  - robots.txt --- 爬虫协议文件
- src——源码文件夹
  - App.css ——App组件的样式
  - App.js ---App组件
  - index.css ------ 样式
  - index.js --- 入口文件
  - reportWebVitals.js——页面性能分析文件（需要web-vitals库的支持）
  - setupTests.js——组件单元测试的文件（需要jest-dom库的支持）

### 4.5 功能界面的组件化编码流程

- 拆分组件：拆分界面，抽取组件
- 实现静态组件：使用组件实现静态页面效果
- 实现动态组件：
  - 动态显示初始化数据
    - 数据类型
    - 数据名称
    - 保存在哪个组件里？
  - 交互(从绑定事件监听开始)

### 4.6 组件的组合使用-TodoList案例

todoList案例相关知识点

- 拆分组件、实现静态组件，注意：className、style的写法
- 动态初始化列表，如何确定将数据放在那个组建的state中
  - 某个组件使用：放在其自身的state中
  - 某些组件使用：放在他们共同的父组件state中（官方称此操作为：状态提升）
- 关于父子之间通信：
  - 父组件 给 子组件 传递数据：通过props传递
  - 子组件 给 父组件 传递数据：通过props传递，要求父组件提前给子组件传递一个函数
- 注意defaultChecked 和 checked 的区别，类似的还有：defaultValue 和 value
- 状态在哪里，操作状态的方法就放在哪里

## 五、React 脚手架配置代理

### 5.1方法一

> 在package.json中追加如下配置

```json
"proxy":"http://localhost:5000"
```

- 说明：
  - 优点：配置简单，前端请求资源时可以不加任何前缀。
  - 缺点：**不能配置多个代理**。
  - 工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）

### 5.2方法二

- 第一步：创建代理配置文件

```
在src下创建配置文件：src/setupProxy.js
```

- 编写setupProxy.js配置具体代理规则：

```js
const proxy = require('http-proxy-middleware')

module.exports = function(app) {
  app.use(
    proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
      target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
      changeOrigin: true, //控制服务器接收到的请求头中host字段的值
      /*
      	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
      	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
      	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
      */
      pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
    }),
    proxy('/api2', { 
      target: 'http://localhost:5001',
      changeOrigin: true,
      pathRewrite: {'^/api2': ''}
    })
  )
}
```

- 说明：
  - 优点：可以配置多个代理，可以灵活的控制请求是否走代理。

  - 缺点：配置繁琐，前端请求资源时必须加前缀。

### 5.3 GitHub搜索案例相关知识点

- 设计状态是要考虑全面，例如带有网络请求的组件，要考虑请求失败怎么办

- ES6知识点：解构赋值+重命名

  ```js
  let obj = {a:{b:1}}
  const {a} = obj;//传统解构赋值
  const {a:{b}} = obj;//连续解构赋值
  const {a:{b:value}} = obj;//连续结构估值+重命名
  ```

- 消息订阅与发布机制

  - 先订阅，在发布（理解：有一种隔空对话的感觉）
  - 适用于任意组件之间的通信
  - 要在组件中的componentWillUnmount中取消订阅

- fetch发送请求(**关注分离的设计思想**)

  ```js
  try{
  	const response = await fetch(`/api1/search/users?q=${keyWord}`)
      const data = await response.json()
      console.log(data)
}catch(error){
      console.log('请求出错',error)
  }
  ```
  

## 六、React路由

### 6.1 相关理解

#### 6.1.1 SPA的理解

- 单页Web应用(single page web application , SPA)
- 整个应用只有一个完整的页面
- 点击页面中的链接不会刷新页面，只会做页面的局部更新
- 数据都需要通过Ajax请求获取，并在前端异步展现

#### 6.1.2 路由的理解

- 什么是路由？
  - 一个路由就是一个映射关系
  - key是路径，value可能是function 或 component
- 路由分类
  - 后端路由
    - 理解：value是function，用来处理客户端提交的请求
    - 注册路由：router.get(path,function(req,res))
    - 工作过程：当node接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据
  - 前端路由：
    - 浏览器端路由，value是component，用于展示页面内容
    - 注册路由：<Route path = "/test" component = {Test}>
    - 工作过程：当浏览器的path变为/test时，当前路由组件就会变成Test组件

### 6.2 路由的基本使用

- 明确好界面中的导航区、展示区

- 导航区的a标签改为Link标签

  ```html
  <Link to="/xxxxx">Demo</Link>
  ```

- 展示区写Route标签进行路径的匹配

  ```html
  Route path='/xxxxx' component={Demo/}
  ```

- <App>的最外侧包裹了一个<BrowserRouter>或<HashRouter>

### 6.3 路由组件与一般组件

- 写法不同：
  - 一般组件：<Demo/>
  - 路由组件：<Route path="/demo" component={Demo}/>

- 存放位置不同：

  - 一般组件：components
  - 路由组件：pages

- 接收到的props不同：

  - 一般组件：写组件标签时传递什么，就能收到什么	

  - 路由组件：接收到三个固定的属性

    - history:

    - 1. go: *ƒ go(n)*
      2. goBack: *ƒ goBack()*
      3. goForward: *ƒ goForward()
      4. push: *ƒ push(path, state)*
      5. replace: *ƒ replace(path, state)

    - location:

    - 1. pathname: "/about"
      2. search: ""
      3. state: undefined

    - match:

    - 1. params: {}
      2. path: "/about"
      3. url: "/about"

### 6.4 NavLink 与封装 NavLink

- NavLink可以实现路由链接的高亮，通过activeClassName指定样式名
- 标签体内容是一个特殊的标签属性
- 通过this.props.children 可以获取标签体内容

### 6.5 Switch的使用

- 通常情况下，path 和 component 是一一对应的关系
- Switch可以提高路由匹配效率(单一匹配)

### 6.6 解决多级路径刷新页面样式丢失的问题

- public/index.html 中 引入样式时不写 ./ 写 / （常用）
- public/index.html 中 引入样式时不写 ./ 写 %PUBLIC_URL% （常用）
- 使用HashRouter (不建议修改路由方式)

### 6.7 路由的严格匹配和模糊匹配

- 默认使用的时模糊匹配（简单记：【输入的路径】必须包含要【匹配的路径】，且顺序要一致）
- 开启严格匹配：<Route exact = {true} path="/about" component={About}>
- 严格匹配不要随便开启，需要的时候再开，有些时候开启会导致无法继续匹配二级路由

### 6.8 Redirect的使用

- 一半写在所有路由注册的最下方，当所有路由都无法匹配时，跳转到Redirect指定的路由

- 具体编码：

  ```js
  <Switch>
      <Route path="/about" component={About}/>
      <Route path="/home" component={Home}/>
      <Redirect to="/about"/>
  </Switch>
  ```


### 6.9 嵌套路由

- 注册子路由时要写上父路由的path值
- 路由的匹配是按照注册路由的顺序进行的

### 6.10向路由组件传递参数

- params参数

  - 路由链接(携带参数)

    ```html
    <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>{msgObj.title}</Link>
    ```

  - 注册路由(声明接受)

    ```html
    <Route path="/home/message/detail/:id/:title" component={Detail}/>
    ```

  - 接收参数

    ```js
    const {id,title} = this.props.match.params
    ```

- search参数

  - 路由链接（携带参数）
  
    ```html
    <Link to={`/home/message/detail/?id=${msgObj.id}&title=${msgObj.title}`}>{msgObj.title}</Link>
    ```
  
  - 注册路由（无需声明，正常注册即可）
  
    ```js
    <Route path="/home/message/detail" component={Detail}/>
    ```
  
  - 接收参数
  
    ```jsx
    const {search} = this.props.location
    ```
  
  - 备注
  
    获取到的search是urlencode编码字符串，需要借助querystring解析
  
    ```jsx
    import qs from 'querystring'
    ```
  
    - 两个方法
  
      `querystring.stringify()` 方法通过遍历对象的自身属性从给定的 `obj` 生成 URL 查询字符串
  
      `querystring.parse()` 方法将 URL 查询字符串 `str` 解析为键值对的集合
  
- state参数(与组件的state没有关系)

  - 路由链接（携带参数）

    ```html
    <Link to={{pathname:`/home/message/detail`,state:{id:msgObj.id,title:msgObj.title}}}>{msgObj.title}</Link>
    ```

  - 注册路由（无需声明，正常注册即可）

    ```js
    <Route path="/home/message/detail" component={Detail}/>
    ```

  - 接收参数

    ```jsx
    const {id,title} = this.props.location.state
    ```

  - 备注

    - 刷新也可以保留住参数

### 6.12 编程式路由导航

- 借助`this.props.history`对象上的API对操作路由跳转、前进、后退

  ```
  this.props.history.push()
  this.props.history.replace()
  this.props.history.goBack()
  this.props.history.goForward()
  this.props.history.go()
  ```

### 6.13 BrowserRouter 与 HashRouter 的区别

- 底层原理不一样
  - BrowserRouter 使用的是H5的history API ，不兼容IE9及以下的版本
  - HashRouter 使用的是URL的哈希值
- path的表现形式不一样
  - BrowserRouter的路径中没有#，例如：localhost:3000/demo/test
  - HashRouter的路径包含#，例如：localhost:3000/#/demo/test
- 刷新后对路由state参数的影响
  - BrowserRouter 没有任何影响，因为state保存在history对象中。
  - HashRouter刷新后会导致路由state参数的丢失(**十分要注意**)。
- 备注
  - HashRouter可以用于解决一些路径错误相关的问题

## 七、React UI组件库

https://ant.design/index-cn 蚂蚁金服组件库

## 八、Redux

### 8.1 redux理解

#### 8.1.1 学习文档

https://www.redux.org.cn/中文网

#### 8.1.2 Redux 简介、

- redux是一个专门用于做状态管理的JS库（不是react插件库），多组件共享
- 它可以用在react，angular，vue的该项目中，但基本与react配合使用
- 作用：集中式管理react应用中过多个组件共享的状态

#### 8.1.3 什么情况下需要使用redux

- 某个组件的状态 ，需要让其他组件可以随时拿到（共享）
- 一个组件需要改变另一个组建的状态（通信）
- 总体原则：能不用就不用，如果不用比较吃力才会考虑使用

#### 8.1.4 redux 工作流程

<img src="D:\project_file\Document\redux流程图.png" alt="redux流程图" style="zoom: 67%;" />

### 8.2 redux的三个核心概念

#### 8.2.1 action

- 动作的对象
- 包含2个属性
  - type：标识属性，值为字符串，唯一，必要属性
  - data：数据属性，值类型任意，可选属性
- 例子：{type:'ADD_STUDENT',data:{name:'tom',age:18}}

#### 8.2.2 reducer

- 用于初始化状态、加工状态
- 加工时，根据旧的state和action，产生新的state的纯函数

#### 8.2.3 store

- 将state、action、reducer联系在一起的对象

- 如何得到此对象?

  - import {createStore} from 'redux'
  - import reducer from './reducers'

  - const store = createStore(reducer)

- 此对象的功能?

  - getState(): 得到state

  - dispatch(action): 分发action, 触发reducer调用, 产生新的state

  - subscribe(listener): 注册监听, 当产生了新的state时, 自动调用

### 8.3 redux的核心API

#### 8.3.1 createstore()

作用：创建包含指定的render的store对象

#### 8.3.1 store对象

- 作用：redux库最核心的管理对象

- 内部维护着：
  - state
  - reducer
- 核心方法：
  - getState()
  - dispatch(action)
  - sucscribe(listener)
- 具体编码：
  - `store.getState()`
  - `store.dispatch({type:'increment',number})`
  - `store.subscribe(render) `—— 一般不这么用

#### 8.3.3 applyMiddleware()

作用：应用上基于redux的中间件（插件库）

#### 8.3.4 combineReducers()

作用：合并多个reducer函数

### 8.4 redux编写求和案例

- 去除Count组件自身的状态
- src下建立：
  - redux
    - store.js
    - count_reducer.js
- store.js:
  - 引入redux中的createStore函数，创建一个store
  - createStore调用时要传入一个为其服务的reducer
  - 记得暴露store对象
- count_reducer.js:
  - reducer本质上就是一个函数，接受：preState，action，返回加工后的状态
  - reducer有两个作用：初始化状态，加工状态
  - reducer被第一次调用时，是store自动触发的，传递的preState是undefined
- 再index.js中检测store中状态的改变，一旦发生改变重新渲染<App/>
  - 备注：redux只负责管理状态，至于状态的改变驱动着页面的展示，需要靠我们自己来写
- 完整版新增文件
  - count_action.js
    - 专门用于创建action对象
  - constant.js 
    - 放置容易写错的type值
- 异步action版
  - 明确：延迟的动作不想交给组件自身，想交给action
  - 何时需要异步action：想要对状态进行操作，但是具体的数据靠异步任务返回。
  - 具体编码：
    - `yarn add redux-thunk`，并配置store中
    - 创建action的函数不在返回一般对象，而是一个函数，该函数中写异步任务。
    - 异步任务有结果后，分发一个同步的action去真正操作数据
  - 备注：异步action不是必须要写的，完全可以自己等待异步任务的结果了再去分发同步action

### 8.5 react-redux模型图

- 所有的UI组件都应该包裹一个容器组件，他们是父子关系
- 容器组件是真正和redux打交道的，里面可以随意的使用redux的api
- UI组件中不能使用任何redux的api
- 容器组件会传给UI组件：
  - redux中保存的状态
  - 用于操作状态的方法
- 备注：
  - 容器给UI传递：状态、操作状态的方法，均通过props传递

<img src="D:\project_file\Document\react-redux模型图.png" alt="react-redux模型图" style="zoom:75%;" />



### 8.6 react-redux应用求和案例

#### 8.6.1 基本操作

- 明确两个概念
  - UI组件：不能使用任何redux的api，之负责页面的呈现、交互等
  - 容器组件：负责和redux通信，将结果交给UI组件
- 如何创建一个容器组件——靠react-redux的connect函数
  - `connect(mapStateToProps,mapDispatchToProps)`(UI组件)
    - `mapStateToProps`：映射状态，返回值是一个对象
    - `mapDispatchToProps`：映射操作状态的方法，返回值是一个对象
- 备注：
  - 容器组件中的store是靠props传进去的，而**不是在容器组件中直接引入**
  - `mapDispatchToProps`也可以是一个对象

#### 8.6.2 总 结

- 容器组件和UI组件整合成一个文件

- 无需自己给容器组件传递store，给<App/>包裹一个<Provider store={store}>即可

- 使用了react-redux后也不用再自己监测redux中状态的改变了，容器组件中可以自动完成这个工作。

- mapDispatchToProps也可以简单的写成一个对象

- 一个组件要和redux“打交道”，要经过哪几步？

  - 定义好UI组件——不暴露

  - 引入Connect生成一个容器组件，并暴露，写法如下：

    ```react
    connnect(
        state=>({key:value}),//映射状态
        {key:xxxAction}//映射操作状态的方法
    )(UI组件)
    ```

  - 在UI组件中通过`this.props.xxx`读取和操作状态

#### 8.6.3 react-redux数据共享案例

- 定义一个Person组件，和Count组件通过redux共享数据
- 为Person组件编写：reducer、action，配置constant常量
- 重点：Person的reducer和Count的reducer要使用combinereducers进行合并，合并后的总状态是一个对象
- 交给store的总是reducer，最后注意在组件中去除状态的时候，记得“取到位”

#### 8.6.4 react-redux开发者工具的使用

- `yarn add redux-devtools-extension`
- store中进行配置
  - `import {composeWithDevTools} from 'redux-devtools-extension'`
  - `count store = createStore(allReducer,composeWithDevTools(applyMiddlware(thunk)))`

### 9 纯函数和高阶函数

#### 9.1 纯函数

- 一类特别的函数: 只要是同样的输入(实参)，必定得到同样的输出(返回)

- 必须遵守以下一些约束：
  - 不得改写参数数据

  - 不会产生任何副作用，例如网络请求，输入和输出设备
  - 不能调用Date.now()或者Math.random()等不纯的方法 

- redux的reducer函数必须是一个纯函数

