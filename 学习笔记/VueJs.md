# 概述

Vue 是一个渐进式框架，意味着你可以把Vue作为你的应用的一部分。

Vue的安装方式

1. 直接CDN引入，分开发版本还是生产环境版本
2. 下载和引入
3. NPM 安装



同样的，跟React一样，Vue也是声明式，好处是数据和界面分离。



# 展示列表

v-for

```js
<div id="app">
  <ul>
  遍历列表
  	<li v-for="items in movies">{{item}}</li>
  
  </ul>
 
</div>

const app = new Vue({
  el:'#app',
  data: {
    movies: ['星际穿越', '大话西游', '少年派', '盗梦空间']
  }
})
```

并且这种方式是响应式的，就是如果这个movies数组里面又新增了1个



# 计数器案例

mustache语法

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220217173534523.png" alt="image-20220217173534523" style="zoom: 50%;" />

```html
<div id="app">
  <h2>
    当前计数: {{counter}}
  </h2>
  监听事件
  <button v-on:click="counter++"> + </button>
   <button> - </button>
</div>
<script>
	let app = new Vue({
    el: '#app',
    data: {
      counter: 1
    }
   
  })
</script>
```



# Vue中的MVVM

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220217174328505.png" alt="image-20220217174328505" style="zoom:33%;" />



# Vue中的options



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220217175547223.png" alt="image-20220217175547223" style="zoom: 50%;" />





# Vue的生命周期













