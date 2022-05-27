# React 简介

React 只关注视图，也就是V

很多人把React跟Vue比较，但React并不是一个框架，它也不做框架的事情

![Screen Shot 2022-01-26 at 10.06.41 AM](/Users/lyle/Desktop/Screen Shot 2022-01-26 at 10.06.41 AM.png)

## 为什么需要 React

因为如果不用 CSS, 只用 JS 想去改一些东西的会比较繁琐

-  JS 操作 DOM 繁琐且效率低
- 使用 JS 直接操作 DOM ，浏览器会进行大量的重绘重排
- 原生 JS 没有组件化编码方案，代码复用率低



## React 的特点

1. 采用组件化模式、声明式编码，提高开发效率及组件复用率，我们以前更熟悉是命令式编程
2. 在 React Native 中可以使用 React语法进行移动端开发
3. 使用虚拟 DOM + 优秀的 Diffing 算法，尽量减少与真实DOM的交互

![image-20220126103313812](/Users/lyle/Library/Application Support/typora-user-images/image-20220126103313812.png)

就是说我现在想再增加一个人比如：肖鹤云，那已有的两个也得重绘，并不能复用，所以效率很低，也就是

![image-20220126103543513](/Users/lyle/Library/Application Support/typora-user-images/image-20220126103543513.png)

虚拟DOM来了！

![image-20220126103609277](/Users/lyle/Library/Application Support/typora-user-images/image-20220126103609277.png)

当数据变化的时候，React 会进行虚拟DOM的比较，之前已经有的，就可以直接用，所以更高效

React

# Hello React

先看一下环境需要哪些文件

Babel.min.js.   ES6->ES5，JSX->JS

先引入react.development,再引入 rect-dom.development



```js
<!--准备好一个容器-->
    <div id="test">
        <h1>Hello, React</h1>
    </div>

<!--引入React核心库-->
<script type="text/javascript" src="../js/react.development.js"></script>
<!--引入react_dom用于支持操作dom-->
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<!--引入babel,用于将jsx转为js-->
<!--这种方式不会在真实生产环境中使用，因为会现翻译，比较慢-->
<script type="text/babel" src="../js/babel.min.js">
    <!--React有虚拟DOM才能工作-->
    <!--1. 创建虚拟DOM-->
    <!--这就是JSX，能和标签混写-->
    const VDOM = <h1>Hello, React</h1>
    <!--2. 渲染虚拟DOM到页面-->
    // 不会有人在这想用jQuery吧，NOOOOO
    ReactDOM.render(VDOM,document.getElementById('test'))

</script>

```

## 创建虚拟DOM的两种创建方式

1. JSX的方式

JSX就是JS创建虚拟DOM的语法糖

1. JS的方式（一般不用），因为太繁琐

为什么虚拟DOM要用 const 声明？



## 虚拟DOM和真实DOM

虚拟DOM：

1. 本质是Object类型的对象
2. 虚拟DOM属性比较少，真实DOM属性多，因为虚拟DOM是React内部在用，不需要那么多属性
3. 虚拟DOM最终会被转换为真实DOM，呈现在页面上



## JSX

JSX全称 JavaScript XML 

是React定义的一种类似于XML的JS扩展语法：JS+XML，用来简化创建虚拟DOM



JSX语法规则：

1. 定义虚拟DOM时，不要引号
2. 标签中混入JS表达式要用{}
3. CSS样式的类名指定不要用class,要用className
4. 内联样式要用{{key:value}}的形式去写
5. 虚拟DOM只有一个根标签
6. 标签必须闭合



JS表达式是什么？

表达式是会产生一个值的，可以放在任何一个需要值的地方，比如

- a
- a+b
- demo(1)
- arr.map()
- function test() {}



JSX小练习

```js
<!--准备好一个容器-->
<div id="test">

</div>

<!--引入React核心库-->
<script type="text/javascript" src="../js/react.development.js"></script>
<!--引入react_dom用于支持操作dom-->
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<!--引入babel,用于将jsx转为js-->
<script type="text/javascript" src="../js/babel.min.js"></script>
<!--这种方式不会在真实生产环境中使用，因为会现翻译，比较慢-->
<script type="text/babel">

    //模拟一些数据
    const data = ['Angular','React','Vue']
  const VDOM = (
      <div>
          <h1>前端JS框架</h1>
          <ul>
              <!--就这里到底能写什么代码，for循环,if都不行-->
              <!--这里是只能写JS表达式:-->
              {
                  data.map((item,index) => {
                      <!-- 每个li都要有个唯一的key在虚拟DOM中-->
                      return <li key={index}>{item}</li>
                  })
              }
          </ul>
      </div>
  )

  ReactDOM.render(VDOM,document.getElementById('test'))
</script>

```



JSX怎么防止注入攻击？

React会对JSX的内容进行转义







## 模块与组件

模块就是向外提供特定功能的JS程序，一般就是一个JS文件

组件是更高一级的存在，包含代码和资源的集合，React的开发者工具可以看到网站由多少个组件构成







# React 面向组件编程

函数式组件和类式组件

```js
 //1.创建函数式组件
  function Demo() {
    return <h1>我是函数式组件</h1>
  }

  //2.渲染组件到页面
  ReactDOM.render(<Demo/>,document.getElementById('test'))
```

Reac解析组件标签，找到Demo组件，然后发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，呈现在页面中



## 组件实例三大核心属性

### state

函数式组件这种简单组件没有 state, 类式组件这种复杂组件才有 state

人  状态 影响 行为

组件 状态 驱动 页面



自定义函数里面的this指向window，如果在严格模式下，就是 undefined

可以利用 bind 关键字解决

`bind()`方法创建一个新的函数，在`bind()`被调用时，这个新函数的this被bind的第一个参数指定，其余的参数将作为新函数的参数供调用时使用

```js
function demo() {
  console.log(this);
}
demo()
const x = demo.bind({a:1,b:2})
x()
```



注意点：

- 组件中 render 方法中的this为组件实例对象
- 组件自定义的方法中this为undefined，如何解决
  - 强制绑定this：通过函数对象的bind()
  - 箭头函数
- 状态数据不能直接修改或更新





props可以接受标签输入的属性

批量传props，有代码

限制props，有代码，React15.5以前可以不用引入库

props是只读的，不能改

类组件的构造器是否接收 props，以及是否传递给 super ，取决于是否希望在构造器中通过 this 访问 props



### 函数式组件使用 props

```js
function Person(props) {
  const {name,age,sex} = props
  return (
    <ul>
    	<li>姓名：{name}</li>
    	<li>性别: {sex}</li>
			<li>年龄：{age}</li>
    </ul>
  )
}
//也一样可以对props进行限制

```



总结：





### refs

就像 标签的id 属性, 只要加了这个ref，React就能收集到refs对象中

字符串类型的（已经不推荐了）因为效率问题，但是简单

```js
class Demo extends React.Component {
  showData = () => {
    const {input1} = this.refs
    alert(input1.value)
  }
  
  shouwData2 = () => {
    const {input2} = this.refs
    alert(input.value)
  }
  render(){
    return (
      <div>
      	<input ref="input1" type="text" placeholder="点击按钮提示数据">&nbsp;
      	<button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
				<input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
      </div>
    )
  }

  ReactDOM.render(<Demo/>,document.getElementById('test'))
}
```



### 回调函数形式的ref

```js
<script type="text/babel">

    class Demo extends React.Component {
        //展示左侧输入框的内容
        showData = () => {
            const {input1} = this
            alert(input1.value)
        }

        //展示右侧输入框的内容
        showData2 = () => {
            const {input2} = this
            alert(input2.value)
        }

        render() {
            return(
                <div>
                    {/*ref接收一个回调函数，只需要写在这，React会去调用这个回调函数*/}
                    <input ref={currentNode => this.input1 = currentNode} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                    <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
                    <input onBlur={this.showData2} ref={currentNode => this.input2 = currentNode} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                </div>
            )
        }
    }

    ReactDOM.render(<Demo a="1" b="2"/>,document.getElementById('test'))
</script>
```

如果回调函数是内联形式的，那么会调用两次，如果是类的自定义函数的形式就不会，但一般无关紧要

ref的最新使用方式

```js
<script type="text/babel">

    class Demo extends React.Component {
      
      myRef = React.createRef()
      myRef2 = React.createRef()
        //展示左侧输入框的内容
        showData = () => {
            alert(this.myRef.current.value)
        }

        //展示右侧输入框的内容
        showData2 = () => {
            alert(this.myRef2.current.value)
        }

        render() {
            return(
                <div>
                    <input ref={this.myRef} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                    <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
                    <input ref="input2" onBlur={this.showData2} ref={currentNode => this.input2 = currentNode} type="text" placeholder="点击按钮提示数据"/>&nbsp;
                </div>
            )
        }
    }
    ReactDOM.render(<Demo a="1" b="2"/>,document.getElementById('test'))
</script>
```





## 事件处理

1. 通过OnXxx属性指定事件处理函数
   1. React使用的是自定义（合成）事件，而不是使用的原生DOM事件 -- 为了更好的兼容性
   2. React中的事件是通过事件委托方式处理的 -- 为了高效
2. 通过 event.target得到发生事件的DOM元素对象



## 受控组件和非受控组件

表单中所有输入框的值都是现用现取就是非受控组件

表单中所有输入框的值随着输入会维护到状态中，这在Vue中就是双向数据绑定





## 高阶函数柯里化

如果一个函数符合下面2个规范中的任意一个，那该函数就是高阶函数

1. 若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数
2. 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数

常见的高阶函数有：promise, setTimeout, arr.map()

函数柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式



## 组件的生命周期

组件从创建到死亡会经历一些特定的阶段

React组件中包含一系列钩子函数（生命周期回调函数），会在特定的时刻调用

我们在定义组件时会在特定的生命周期回调函数中做特定的工作

Render()的调用次数，组件初始化会调用，之后每次修改状态都会调用，是 1+N

生命周期回调函数 = 生命周期钩子函数 = 生命周期函数 = 生命周期钩子



生命周期流程图

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220203124417436.png" alt="image-20220203124417436" style="zoom:50%;" />



我们说当状态更新时，会调用render，实际上在调用render之前会先调用 shouldComponentUpdate

初始化阶段：由ReactDOM.render()触发  -- 初次渲染

1. Constructor()
2. ComponentWillMount()
3. Render()
4. ComponentDidMount()

更新阶段：由组件内部this.setState()或父组件render触发

1. ShouldComponentUpdate()
2. ComponentWillUpdate()
3. Render()
4. ComponentDidUpdate()

卸载阶段：由 ReactDOM.unmountComponentAtNode()

1. ComponentWillUnmount()





## 新生命周期

新版本也是可以用旧版本的钩子的，但是不推荐

新和旧的区别：

1. 废弃了三个钩子：
2. 提出两个新的钩子，剩下的都是一样



getDerivedStateFromProps很少用，只有在state的值完全取决于props的时候才用

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220203190934166.png" alt="image-20220203190934166" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220203191131020.png" alt="image-20220203191131020" style="zoom:50%;" />





# 脚手架

App.js 是父组件，你可以写其他子组件包含在这个里面

在 App.js中引入 js和jsx文件都可以不写后缀

index.js



# ES6模块化

https://www.1024sou.com/article/502155.html

https://blog.51cto.com/jackiehao/3780702

文件名大写代表是个组件

也就是说这个不是像Java那种包管理器是语言本身就有的.



CSS可能会产生冲突，可以用样式的模块化解决，但一般不会，因为一般用less



# 功能界面组件化编码流程

1. 拆分组件：拆分界面，抽取组件
2. 实现静态组件：使用组件实现静态页面效果
3. 实现动态组件
   1. 动态显示初始化数据
      1. 数据类型
      2. 数据名称
      3. 保存在哪个组件中

   2. 交互（从绑定事件监听开始）




# TODOLIST 案例

按照上面的组件化编码流程，在静态页面已有的情况下，就得拆分到组件里面。

## 问题

然后有一个问题是父子组件可以通过 props 传值，那兄弟组件之间如何传值？

还有子组件怎么给父组件传值？



## 相关知识点

1. 拆分组件、实现静态组件，注意：className、style的写法
2. 动态初始化列表，如何确定将数据放在哪个组件的state中？
   1. 某个组件使用：放在自身的state中
   2. 某些组件使用：放在它们共同的父组件state中（官方称为：状态提升）
3. 关于父子之间通信：
   1. 父组件给子组件传递数据：通过props传递
   2. 子组件给父组件传递数据：通过props传递，要求父提前给子传递一个函数
4. 注意defaultChecked 和 checked 的区别，类似的还有 defaultValue 和 value
5. 状态在哪里，操作状态的方法就在哪里





# React路由

对于多页面应用来说，浏览器中的路径对应着一个页面；而对于单页面应用来说，浏览器中的路径对应着一个组件



什么是路由？

路由就是一个映射关系(key:value)

key为路径，value可能是function或component



后端路由：

后端路由应该就是Spring MVC里面的请求映射吧

value是function，用来处理客户端提交的请求

工作过程：当服务器接收到一个请求时，根据请求路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据



前端路由

value是component,用于展示页面内容

工作过程：当浏览器的path变为/test时，当前路由组件就会变成Test组件

前端路由的基石就是 BOM的 history



## react-router的理解

react的一个插件库，专门用来实现一个SPA应用























# Webpack

https://segmentfault.com/a/1190000006178770







# 经典面试题

React/Vue中的key有什么作用？（key的内部原理是什么？）

为什么遍历列表时，key最好不要用index?

![image-20220203193839608](/Users/lyle/Library/Application Support/typora-user-images/image-20220203193839608.png)







————————————————————————————————————————————————————————————



# React元素，渲染，工程化

 

npx create-react-app 项目名

npx是npm5.2+的包运行工具

create-react-app内部的工程化：babel/webpack



# Vite

Vite是什么？

vite 帮助我们处理JSX

# JSX

1. 是一种标签语法，JS进行的语法扩展
2. 不是字符串、不是HTML标签
3. 描述UI呈现与交互的直观的形式
4. 生成React元素



createElement 与 JSX 对比

```js
const rEl = React.createElement('h1',{
  className: 'title'
}, 'This is my first JSX experience');

const rEl = <h1 className="title">This is my first experience.</h1>
ReactDOM.render(
rEl,
document.getElementById('app')
)
```



为什么React不把视图标签和逻辑分开？

1. 渲染和UI标记是有逻辑耦合的，更加直观
2. 即使是这样的耦合，也能实现关注点分离



JSX 插值表达式：就是写在 { expression } 这种括号中的表达式

JSX 被编译后会转化为 React元素，这个React元素和那个 React API 提供的 React.createElement()创建出来的是一样的，这个对象中最重要的属性就是 props，可以通过组件传值嘛

```jsx
遍历对象数组
let arr = []
function setList () {
  return (
  <ul>
      {
        arr.map((item) => {
          return (
            <li key={ item.id }>
            	<span>{ item.id }</span>
              <p> { item.name }</p>
            </li>
          );
        })
      }
    </ul>
  )
}
```

JSX在渲染之前会被转成字符串,然后进行分析

```jsx

const rEl = <h1 className="title">this is a title.</h1>;
console.log(rEl);

@param ReactElement - react元素
@param rootNode - 根节点
ReactDOM.render(
rEl,
document.getElementById('app')
)
```

基本的更新逻辑

1. React元素是不可变对象 immutable Object
   1. 不能添加属性
   2. 不能修改属性
   3. 不能删除属性
   4. 不能修改属性的枚举、配置、可写 enumerable/configurable/writable



## 条件渲染







## 列表渲染

列表的每个子元素都应该有一个 unique key prop

因为 key 是 React 查看元素是否改变的一个唯一标识

key必须在兄弟节点中唯一



不建议使用index作为key值（禁止）

因为如果列表项增删或者顺序改变了，index的对应项就会改变

key对应的项还是之前列表情况的对应元素的值

导致状态（arr）混乱，查找元素性能就会变差



好的做法：

如果列表是静态不可操作的，可以选择index作为key，但也不推荐，因为这个列表在以后可能会变成可操作的列表

可以用数据的ID，但是ID也可能会变化，后端如果操作变更了数据

最好的选择是使用动态生成一个静态ID  [nanoid](http://localhost:3000/users) https://github.com/ai/nanoid/blob/main/README.zh-CN.md



key 赋值的正确姿势





key 是不会作为属性传递给子组件的，必须显示传递key值，这是为了防止开发者在逻辑中对key值进行操作





