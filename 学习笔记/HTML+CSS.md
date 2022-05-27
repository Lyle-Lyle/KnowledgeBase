# HTML

网页的title:

​	主页：网站名称+主要的关键字/关键词的描述

​	详情页：详情名称+网站名称+简介

​	列表页：分类名称+关键字+网站名称

​	文章页：标题+分类+网站名称



keywords   100个字符

网站名称+分类信息+网站名称



网页的description 描述信息  80-120

综合 title + keywords 的简单描述



搜索引擎认知的优先级：

​	title > description > keywords

```html
<html>
  <head>
    <title></title>
    <meta name="keywords" content=""/>
    <meta name="description" content=""/>
  </head>
  <body>
    
  </body>
</html>
```

搜索引擎每隔一段时间就会启动爬虫程序去对一个IP范围的网站的数据进行抓取并保存到自己的数据库中。



# 语义化

在网页设计中有两种标签，一种是物理性的标签，一种是语义化的标签









# CSS

浏览器的组成：shell和内核

内核：渲染引擎/JS引擎

Google Chrome     webkit/blink

Safari		webkit

Firefox		gecko

IE		trident

Opera		presto



浏览器解析页面：

当输入网址的时候，浏览器会去下载HTML和CSS文件，它们分别形成DOM树和CSS规则树，然后这两个树又会构建出渲染树，



## 选择器



属性选择器出现比较少，多用于 input 输入框，用于区分不同 type 的输入框



## 样式优先级

https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Selectors

直接在样式后面写 !important，在项目中如果用到这个就得想想样式是否合理了。

优先级

!important > id > class = 属性 > 标签 > * 

浏览器对父子选择器的匹配规则

是从左往右匹配的，这样效率高



## 盒子模型

如何让一个盒子在另一个盒子中居中?

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子模型</title>
    <style>
        /*如何让一个盒子在另一个盒子中居中，就是给外面大盒子设置padding,外面大盒子会被撑开*/
        .box {
            width: 100px;
            height: 100px;
            padding: 30px;
            border: 1px solid #000;
        }

        .box .box1 {
            width: 100px;
            /*写100%表示继承父元素的值，这种用的更多*/
            /*width: 100%;*/
            /*height: 100%;*/
            height: 100px;
            background-color: orange;
        }
    </style>
</head>
<body>
    <div class="box">
        <div class="box1"></div>
    </div>
</body>
</html>
```

```html
如何让一个盒子在另一个盒子中居中，并且外边盒子不被撑开
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子模型</title>
    <style>
        div {
            /*表示把边框和内边距收到盒子内部绘制,这样能准确绘制外层盒子的宽高*/
            box-sizing: border-box;
            /*兼容firefox*/
            -moz-box-sizing: border-box;
            /*兼容chrome*/
            -webkit-box-sizing: border-box;
        }
        /*如何让一个盒子在另一个盒子中居中，并且外边盒子不被撑开*/
        .box {
            width: 200px;
            height: 200px;
            padding: 30px;
            border: 1px solid #000;
            /*表示把边框和内边距收到盒子内部绘制*/
            box-sizing: border-box;
            /*兼容firefox*/
            -moz-box-sizing: border-box;
            /*兼容chrome*/
            -webkit-box-sizing: border-box;

        }

        .box .box1 {
            /*width: 100px;*/
            /*写100%表示继承父元素的值，这种用的更多*/
            width: 100%;
            height: 100%;
            /*height: 100px;*/
            background-color: orange;
        }
    </style>
</head>
<body>
    <div class="box">
        <div class="box1"></div>
    </div>
</body>
</html>
```



盒子在网页中居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子模型</title>
    <style>
        /*父盒子左右居中*/
        .box {
            width: 200px;
            height: 200px;
            background-color: orange;
            margin: 0 auto;
        }

        /*子盒子在父盒子中左右居中*/
        .box1 {
            width: 50px;
            height: 50px;
            background-color: green;
            margin: 0 auto;
        }

    </style>
</head>
<body>
    <div class="box">
        <div class="box1"></div>
    </div>
</body>
</html>
```

margin 塌陷的问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子模型</title>
    <style>
        /*父盒子左右居中*/
        .box {
            width: 200px;
            height: 200px;
            background-color: orange;
            margin: 0 auto;
        }

        /*子盒子在父盒子中左右居中*/
        .box1 {
            width: 50px;
            height: 50px;
            background-color: green;
          父盒子下来了，自盒子还是没动
            margin: 100px auto;
        }

    </style>
</head>
<body>
    <div class="box">
        <div class="box1"></div>
    </div>
</body>
</html>
```

浏览器的默认body的边距

```html
    <style>
        /*可以看到这个div跟浏览器边框是有几个像素的空隙的，这是浏览器的默认的body的边距，*/
        /*这个每个浏览器的标准不一样。*/
        .header {
            width: 100%;
            height: 60px;
            background-color: #000;
        }
    </style>

```



## 定位

绝对定位

如果一个元素有了绝对定位那么就会新建一个层，就像PS里面新建图层一样。绝对定位找离自己最近有定位的父元素，没有就是HTML文档

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box1 {
            position: absolute;
            left: 30px;
            top: 50px;
            width: 100px;
            height: 100px;
            background-color: green;
        }

        .box2 {
            width: 200px;
            height: 200px;
            background-color: orange;
        }

    </style>
</head>
<body>
<!--绝对定位 absolute-->
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



相对定位：

可以明显看出，相对定位的元素即使脱离了文档流，但是原来所在层的位置还是不能被其他元素占据的，也就是说这个相对定位的元素是不会跟其他元素重合在一起的，像绝对定位那样

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box1 {
            position: relative;
            left: 20px;
            top: 10px;
            width: 100px;
            height: 100px;
            background-color: green;
        }

        .box2 {
            width: 200px;
            height: 200px;
            background-color: orange;
        }

    </style>
</head>
<body>
<!--绝对定位 absolute-->
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



把绝对定位和相对定位结合起来

一般是子绝父相

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box1 {
            width: 400px;
            height: 400px;
            margin: 100px 0 0 100px;
            border: 1px solid #000;
        }

        .box1 .box2 {
            position: relative;
            width: 200px;
            height: 200px;
            background-color: green;
        }

        .box1 .box2 .box3 {
            position: absolute;
            top: 0px;
            left: 0;
            width: 50px;
            height: 50px;
            background-color: orange;
        }


    </style>
</head>
<body>

    <div class="box1">
        <div class="box2">
            <div class="box3">

            </div>
        </div>
    </div>

</body>
</html>
```

z-index

两个绝对定位的元素，后面的会放在上面，如果想把前面的放在上面，可以加上z-index

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box1 {
            position: absolute;
            z-index: 999;
            width: 100px;
            height: 100px;
            background-color: #000;
        }
       .box2 {
           position: absolute;
           width: 100px;
           height: 100px;
           background-color: orange;
       }
    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



### 绝对定位中的两栏设计

这个效果是右边不变，左边随浏览器变化而变化，如果想反过来，也很简单

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        html,body {
            height: 100%;
            margin: 0;
          没有滚动条
            overflow-y: hidden;
        }

        .left {
            height: 100%;
            margin-right: 300px;
            background-color: green;
        }

        .right {
            position: absolute;
            right: 0;
            top: 0;
            width: 300px;
            height: 100%;
            background-color: orange;
        }

    </style>
</head>
<body>

    <div class="left"></div>
    <div class="right"></div>

</body>
</html>
```





## 浮动

https://juejin.cn/post/6930795725143932936

float出来最初的目的是解决，图片嵌入文字的问题。因为块元素会自动换行，所以图片没办法和文字在一行，加了浮动就可以了。

块级元素加了浮动之后就变成内联块元素了

重要结论：

内联，内联块，浮动，溢出隐藏，纯文本都可以识别浮动元素的位置，只有块级元素不行。也就是说一个加了浮动的元素，碰到另一个块元素会重合在一起，因为浮动最初引入的目的是为了解决图片嵌入文本并自适应对齐，所以浮动无法识别块元素的位置，而内联，内联块和文本相关的都可以

常常会导致这种结果：父盒子如果没有宽度，那么里面的两个浮动子盒子是没有办法撑开父盒子的，因为父盒子是块级元素，无法识别浮动元素

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220214103006361.png" alt="image-20220214103006361" style="zoom:50%;" />

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box {
            width: 200px;
            border: 10px solid #000;
        }

        .box .inner-box {
            float: left;
            width: 100px;
            height: 100px;
        }

        .box .inner-box.box1 {
            background-color: green;
        }

        .box .inner-box.box2 {
            background-color: orange;
        }

        .text-box {
            width: 100px;
            border: 1px solid #000;
        }

    </style>
</head>
<body>
    <div class="box">
        <div class="inner-box box1"></div>
        <div class="inner-box box2"></div>
    </div>
    <div class="text-box"></div>
</body>
</html>
```



那么如何解决这个问题呢？

就是清除浮动

第一种解决办法就是加一个块级元素并添加清除浮动

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box {
            width: 200px;
            border: 10px solid #000;
        }

        .box .inner-box {
            float: left;
            width: 100px;
            height: 100px;
        }

        .box .inner-box.box1 {
            background-color: green;
        }

        .box .inner-box.box2 {
            background-color: orange;
        }

        .text-box {
            width: 100px;
            border: 1px solid #000;
        }

        .clearfix {
            clear: both;
        }

    </style>
</head>
<body>

    <div class="box">
        <div class="inner-box box1"></div>
        <div class="inner-box box2"></div>
        <p class="clearfix"></p>
    </div>
    <div class="text-box"></div>

</body>
</html>
```



第二种是使用伪元素：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        /*清除浮动的最佳方法*/
        /*这个就相当于之前最后面的<P>的位置*/
        ul::after,
        div::after {
            /*content是必须要的*/
            content: "";
            display: block;
            clear: both;
        }
        .box {
            width: 200px;
            border: 10px solid #000;
        }
        
        .box1 {
            float: left;
            width: 100px;
            height: 100px;
            background-color: green;
        }

        .box2 {
            float: left;
            width: 100px;
            height: 100px;
            background-color: orange;
        }


    </style>
</head>
<body>
<div class="box">
    <div class="box1"></div>
    <div class="box2"></div>
</div>
</body>
</html>
```



在父级盒子上 overflow: hidden 也可以，但是会出问题，比如没有滚动条



 <img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220214104755946.png" alt="image-20220214104755946" style="zoom: 33%;" />

怎么让黄色块移到上面一行，因为绿色盒子是块元素，黄色是加了浮动的块元素，所以会换行

解决办法：给绿色盒子也加浮动，这样两个盒子就都是内联块元素了，可以在一行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        .header {
            width: 100%;
            height: 60px;
            background-color: #000;
        }

        .header .left {
            float: left;
            width: 200px;
            height: 100%;
            background-color: green;
        }

        .header .right {
            float: right;
            width: 200px;
            height: 100%;
            background-color: orange;
        }

    </style>
</head>
<body>
<div class="header">
    <div class="left"></div>
    <div class="right"></div>
</div>
</body>
</html>
```





## 伪类

https://juejin.cn/post/7047473676979994654

https://juejin.cn/post/6976646049456717838

所有HTML元素都有 :before 和 :after 伪类

而 ::before 和 ::after 是伪元素



老师做了个京东轮播图的样式，就是下面有一排白色小点那个，可以看看

还有应用场景就是获取后端数据的时候

```html
P:before {
	content: attr(data-username);
}

<body>
  <p data-username="superatc">
    欢迎您
  </p>
</body>
```



## 盒子阴影

怎么遮住盒子上面的阴影

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
       body {
           margin: 0;
       }
       .header {
           position: relative;
           z-index: 1;
           width: 100%;
           height: 60px;
           background-color: yellow;
       }

       .box {
           width: 300px;
           height: 200px;
           background-color: orange;
           margin-left: 200px;
           box-shadow: 0 0 10px #666;
           -webkit-box-shadow: 0 0 30px #000;
           -moz-box-shadow: 0 0 30px #000;
       }
    </style>
</head>
<body>

    <div class="header"></div>
    <div class="box"></div>

</body>
</html>
```

 ## 圆角

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
      .box1 {
          width: 300px;
          height: 100px;
          background-color: orange;
          /*在做纯圆的时候才会用百分比*/
          border-radius: 20px;
      }

      .box2 {
          width: 200px;
          height: 200px;
          background-color: orange;
          border-radius: 50%;
      }
    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



## 背景图

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        body {
            margin: 0;
        }

        .banner {
            width: 100%;
            height: 600px;
            background-color: orange;
            background-image: url();
            background-size: 100% 100%;
            /*设置背景图不会变形，并一直在中间显示*/
            /*cover是要占满整个盒子，跟contain相反*/
            background-size: cover;
            /*保持完整显示整个图片*/
            /*background-size: contain;*/
            background-position: center center;
        }
    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>
</html>
```



怎么让背景图不滚动？

background-attachment: fixed;

企业级写法

这种写法即使网速不好的时候，也能有正常体验

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
       h1 {
           margin: 0;
       }

       .logo {
           width: 142px;
           height: 58px;
       }

       .logo h1 .logo-hd {
           display: block;
           width: 142px;
           height: 0;
           padding-top: 58px;
           background: url(img/logo.png) no-repeat 0 0/142px 58px;
           overflow: hidden;
       }
    </style>
</head>
<body>
    <div class="logo">
        <h1>
            <a href="" class="logo-hd">
                淘宝网
            </a>
        </h1>
    </div>
</body>
</html>
```





