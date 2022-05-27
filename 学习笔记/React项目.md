# 项目配置

路径问题

```json
"compilerOptions": {
    "baseUrl": "./src",
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
```



使用 Prettier对代码进行统一格式化，实现每次提交前对代码进行自动格式化

手动格式化：yarn prettier --write .

但我们希望能自动格式化，借助 Pre-commit hook

prettier和eslint一起工作的时候会有一些冲突







# CSS模块

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207180356262.png" alt="image-20220207180356262" style="zoom:50%;" />

引入 CSS对象而不是CSS文件



CSS in JS

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207181942744.png" alt="image-20220207181942744" style="zoom:50%;" />



还有一件事：既然 typescript是为了给JS加类型的，那么现在变成对象的CSS是不是也能加上类型呢？

## 加载媒体和字体文件

因为字体是全局样式，在 index.css中添加



# State 和 Props

React是单向数据流动的，

State可以认为是组件的私有属性，必须用setState来修改属性

如果直接修改State，组件不会触发 render函数，页面不会渲染

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207203848079.png" alt="image-20220207203848079" style="zoom:50%;" />

值得注意的是：State的更新是异步的

调用setState后，state不会立即改变，是异步的操作，React可能会把多次state修改的操作合并到一次来做，所以不要依赖当前的state去计算下一个state.



Props就是从组件外部传入组件的数据。

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207204211698.png" alt="image-20220207204211698" style="zoom:50%;" />

所有的 Props 都是不可变的，就像函数的自变量 x 不会因为函数的操作就被改变了值

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207204353251.png" alt="image-20220207204353251" style="zoom:50%;" />





# 事件

自定义函数使用箭头函数的原因是 this 的指向问题，直接声明的函数this是undefined或指向window的，而我们希望this能够指向类组件实例，而箭头函数的this是指向外层的。

不用箭头函数的解决办法是：

![image-20220207210733847](/Users/lyle/Library/Application Support/typora-user-images/image-20220207210733847.png)

但还是箭头函数简洁一点。

这个Even事件有两个值

e.target 这个是比如你点了图标触发了事件，这个就表示那个图标

e.currentTarget   这个是表示事件绑定的元素，就是按钮



# setState 异步处理

setState函数是异步更新，同步执行的







# React Hooks

Hooks的目的就是为了给函数式组件加上状态

生命周期函数会同时处理多项任务：发起AJAX，跟踪数据状态，绑定事件监听

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207232114950.png" alt="image-20220207232114950" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207232400442.png" alt="image-20220207232400442" style="zoom:50%;" />

![image-20220207232523242](/Users/lyle/Library/Application Support/typora-user-images/image-20220207232523242.png)



## side effect

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207234750055.png" alt="image-20220207234750055" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220207234143266.png" alt="image-20220207234143266" style="zoom: 33%;" />

useEffect的两个情况，第一个是第二个参数为空，就相当于是初始化组件的时候调用一下，如果第二个参数没有，那么就相当于每次渲染都会调用，可能造成严重后果





## 组件化 context provider

```typescript
interface AppStateValue {
  username: string;
  shoppingCart: { items: {id: number, name: string}[] }
}

const defaultContextValue : AppStateValue = {
  username: "Lyle",
  shoppingCart: {items: [] }
}

export const appContext = React.createContext(defaultContextValue);

export const AppStateProvider: React.FC = (props) => {
  const [state, setState] = useState(defaultContextValue);
  
  return (
  	<appContext.Provider value={state}>
    	{props.children}
    </appContext.Provider>
  )
}
```





## 高阶组件HOC

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220208110344402.png" alt="image-20220208110344402" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220208110541077.png" alt="image-20220208110541077" style="zoom: 33%;" />

## 自定义Hook







# 网站开发实战



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220208132631606.png" alt="image-20220208132631606" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220208133833619.png" alt="image-20220208133833619" style="zoom:50%;" />

页面规划就是根据每一个模块，规划需要哪些页面

## 项目配置

安装CSS模块化

```type
npm install typescript-plugin-css-modules --save-dev
```

tsconfig.json  .vscode.  custome.d.ts

修改 App.tsx 文件，以对象化的形式导入CSS



安装 Ant Design 依赖

```
npm install antd @ant-design/icons

import 'antd/dist/antd.css';
```





组件化 Header 和 Footer





## 路由

npm install react-router-rom

npm install @types/react-router-dom --save-dev

想在 {} 中写JSX需要用模版字符串？

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220210210601832.png" alt="image-20220210210601832" style="zoom: 33%;" />



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211101333514.png" alt="image-20220211101333514" style="zoom: 50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211105608696.png" alt="image-20220211105608696" style="zoom: 33%;" />



react-router中有两种在页面之间跳转的方式：

1. 就是直接使用 navigate的方式
2. 还有就是组件化的思想使用link组件



<Link> 得放在 顶层 <Router>里面，可以改用 <NavLink>

这个组件可以右键新打开标签页





## Redux

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211125649287.png" alt="image-20220211125649287" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211130650778.png" alt="image-20220211130650778" style="zoom:50%;" />

React是单向数据流动，但我们可以通过回调函数往父组件传值，但会导致项目代码很难维护

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211130804504.png" alt="image-20220211130804504" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211131056461.png" alt="image-20220211131056461" style="zoom: 25%;" />

redux 统一保存数据，在隔离了数据与UI的同时，负责处理数据的绑定

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211131426888.png" alt="image-20220211131426888" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211131944117.png" alt="image-20220211131944117" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220211132341789.png" alt="image-20220211132341789" style="zoom:50%;" />

因为 Redux 中数据是单向流动的，所以你是没有办法直接去修改你看到的别人的朋友圈（store）的内容的，所以你只能 dispatch actions to inform someone 

### 创建数据仓库 Store





### I18N国际化工具





### Action Creator 工厂模式

重构 action的代码，因为action很容易出错，由于是事件驱动的，很难找到源头，所以使用工厂模式集中创建action





