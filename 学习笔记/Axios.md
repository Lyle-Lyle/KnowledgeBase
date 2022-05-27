# 异步

JS是单线程的，这是为了防止DOM冲突

解决方式就是异步，否则单线程会阻塞页面

而异步的解决方案就是事件轮询，事件轮询的核心是回调函数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220206115519579.png" alt="image-20220206115519579" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220206115151941.png" alt="image-20220206115151941" style="zoom: 33%;" />

Call Stack 是主线程（宏任务）的调用栈

当时间完成时，就把cb1放到回调队列中

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220206115649100.png" alt="image-20220206115649100" style="zoom: 33%;" />

而只要主线程中没有任务，就会一直查看 Callback queue，如果里面有任务就执行



同步回调函数？异步回调函数





# 迭代器，生成器，promise, async, await

ES6的三大核心：类相关，promise, 模块化

![image-20220206121705740](/Users/lyle/Library/Application Support/typora-user-images/image-20220206121705740.png)

如果我们想用一种统一的遍历方式去遍历图中的三种结构，我们发现对象类型是会报错的。这是因为：

for of 之所以能遍历，是因为数组和字符串的原型上面都有一个 Symbol.iterator,这个东西决定了它们是可以用 for of 方式遍历的

![image-20220206122656955](/Users/lyle/Library/Application Support/typora-user-images/image-20220206122656955.png)

# axios简介



