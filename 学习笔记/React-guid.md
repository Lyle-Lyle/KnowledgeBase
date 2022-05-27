# Components

组件就是把HTML，CSS，JS 代码集成到一个组件里面，并可重用

React 使用声明式的方法来构建组件

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220212184009687.png" alt="image-20220212184009687" style="zoom: 33%;" />

A component is basically just a custom HTML element

现在来对比一下React使用声明式语法的JSX和我们命令式（imperative）的原生JS的区别：

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220213123539194.png" alt="image-20220213123539194" style="zoom: 50%;" />

当界面变得很复杂的时候，这种声明式的写法就会非常麻烦

![image-20220213124248477](/Users/lyle/Library/Application Support/typora-user-images/image-20220213124248477.png)

一个React应用实际上是一棵组件树



React 的 component其实就是JS函数，只不过返回值比较特殊，是HTML code，并且这个JSX 代码片段只能有一个根标签

外部文件需要使用组件的话，需要 export 当前组件

格式化日期

```js
const day = props.date.toLocalString('en-US', { day: '2-digit'});
```


## 容器型组件

props.children allows you to create wrapper components

https://wangjintian.com/2020/11/17/props.children%20%E5%92%8C%E5%AE%B9%E5%99%A8%E7%B1%BB%E7%BB%84%E4%BB%B6/



# React State & Working with Events

![image-20220214123223360](/Users/lyle/Library/Application Support/typora-user-images/image-20220214123223360.png)



这里是可以用 const 来定义变量的，因为后面的 setTitle 并不是直接 title =  ""   这样赋值的。

虽然 setTitle 确实改变了 title 的值

更重要的是 State 更新的时机





## 组件接收用户输入

```js
const ExpenseForm = () => {
  
  const [enteredTitle,setEnteredTitle] = useState('')
  
  //如果有多个state
  const [userInput, setUserInput] = useState({
    enteredTitle: '',
    enteredAmount: '',
    enteredDate: ''
  })
  const titleChangeHandler = (event) => {
    setEnteredTitle(enteredTitle)
    //如果有多个state,因为state是会被全部替换，所以需要复制整个数组
    setUserInput({
      ...userInput,
      enteredTitle: event.target.value
    })
  }
}

<input type='text' onChange={titleChangeHandler} />
```

但是这种做法可能会出问题，因为你依赖了以前的state来更新当前的state，所以修改为

原因是 React可能并不会马上更新state，而是有一个schdule,

而下面这种方式的prevState是保证是最新的state

```js
setUserInput((prevState) => {
  return { ...prevState, enteredTitle: event.target.value};
})
```



处理表单提交

为什么没有加在button上面，默认表单事件



add two-way binding









通过回调函数让子组件向父组件传值以及兄弟组件间传值（状态提升）

```js
const NewExpense = () => {

    const saveExpenseDataHandler = (enteredExpenseData) => {
        const expenseData = {
            ...enteredExpenseData,
            id: Math.random().toString()
        };
        console.log(expenseData)
    };

  return (
    <div className='new-expense'>
      <ExpenseForm onSaveExpenseData={ saveExpenseDataHandler }/>
    </div>
  );
};
export default NewExpense;

```



## 受控与非受控组件





# Rendering List & Conditional Content

渲染动态列表



unique keys







# Styling Components







# Dive deeper: working with fragments, portals & Refs



























# IMDB Project

## Features

1. videos trailers
2. users rating 
3. Watchlist
4. your website must contain is that the users can order movies which might be missing in IMDB. 
5. Carousel
6. login page