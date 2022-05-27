# JavaScript基础语法

JavaScript很重要在前端领域，学习阶段重心应该在JS而不是前端框架。

五大主流浏览器 内核
IE  trident
chrome  webkit blink
safari webkit
firefox gecko
opera presto

浏览器的历史
1990，Tim 用超文本分享资讯
world wide web 移植到C libwww/nexus
允许别人浏览他人编写的网站

1993，NCSA开发了**MOSIAC**浏览器，这是第一个图形化浏览器

1994，马克安德森和吉姆克拉克，MOSIAC被伊利诺大学卖给了spy glass公司 -> Netscape 网景公司 -> netscape navigator -> 直到2003还流行

1996，微软收购 spy glass 在MOSIAC基础上开发出 IE浏览器

1996，网景公司Brendan eich开发出了 livescript，这就是JS的前身。

1996，Java火起来了，livescript改名为JavaScript

2001，IE6 XP诞生，单独剥离出来JS引擎

2003，mozilla公司的firefox在 netscape navigator的基础上被开发出来了

2008，google基于 WEBKIT BLINK GEARS 开发出了 chrome -> V8引擎 -> JS引擎

1. 直接翻译机器码
2. 独立于浏览器运行  -> Node.js




Progressive web app 渐进式WEB APP 是现在正在搞的概念

2009，Oracle收购了SUN公司，JS的所有权给Oracle



ECMA European Computer Manufactures Association

 ECMA -262 脚本语言的规范  ECMAScript
 命名规范：
 不能以数字开头，能以字母_$开头，不能是关键字/保留字，尽量语义化，结构化
 小驼峰，第一个单词的首字母小写



## JS的值

 原始值 -> 基本类型 5种
 Number String Boolean undefined null

```JavaScript
var a = 1;
var a = 3.14;
var str = 'I love you';

JS跟Java,C++的区别在于，JS的数据类型在声明的时候左边并没有定数据类型，而是根据右边的值定的。
JS是弱类型语言。
动态语言 -> 脚本语言 -> 解释性语言 -> 弱类型语言 
静态语言 -> 编译型语言 -> 强类型语言

var a = undefined;
document.write(a)

```

 引用值


 object array function date RegExp


 Object引用类型 包括 object,array,null(一个bug),

 ```JavaScript
 var person = {
     name: 'Lyle',
     age: 18,
     height: 180,
     weight: 140,
     job: 'Software Developer'
 }

 console.log(typeof([]));  ->object
 console.log(typeof(null)); -> object
 console.log(typeof(undefined)); ->undefined
 console.log(typeof(function(){}));  ->function
 console.log(typeof(1 - "1"));  ->number
 console.log(typeof("1" - "1"));  ->number
 console.log(typeof(a));   ->undefined
 console.log(typeof(typeof(undefined)));  ->string , 并不是undefined
 console.log(typeof(typeof(a)));  ->string, 两次typeof都是string,因为把类型名当字符串了
 每条语句结尾加上分号，如果没加，也会自动加上

 任何数据类型的值 + 字符串都是字符串

 

 c = "str" + NaN
 c = 0 / 0  -> NaN
 NaN not a number  
 c = "a" / "c" -> NaN
 c = 1 / NaN -> NaN
 c = 1 / 0  -> Infinity数字类型

 ==是不看数据类型的，===需要看数据类型是否相等
 NaN与包括自己在内的所有东西都不相等

 ```

## 逻辑运算

与&& 或|| 非!

undefined, null, NaN, "", 0, false 是假，其它都是真

```JavaScript
var a = 1 && 2;
console.log(a);   ->1
var b = 1 || 2;
console.log(b);   ->2
var c = 1 && 2 && undefined && 10;  ->undefined
var d = 0 || null || 1 || 0;  ->1
短路原则
```

## 类型转换

显式和隐式类型转换

```JavaScript

var a = '3.14';
console.log(typeof(Number(a)));  ->Number

var b = true,false,null,NaN
typeof(parseInt(b)); //都会是NaN
console.log(parseInt('abc123'));  //->NaN
console.log(parseInt('123abc'));  //->123

var num = parseFloat('3.1415926');
console.log(num.toFixed(2));  //->3.15
console.log(typeof(String(123))); //->string
console.log(123+'');  //同样的效果，转换成字符串

var str = undefined;
console.log(str.toString()); //undefined和null不行，没有toString方法

隐式类型转换

var a = '123';
a++;
console.log(a);  //124

var b = '1' > 2;
console.log(a);  //false

var c = 'a' > 'b'; //比较ASCII码
console.log(c);   //false

var d = 2 > 1 > 3;
var d2 = 2 > 1 == 1;
console.log(d, d2);  //false, true

var e = undefined > 0; //false
var e = undefined < 0; //false

var f = null > 0; //false
var f2 = null == 0; //false

var g = null == undefined;  //true

isNaN(NaN);  //true
isNaN(null);  //false, 会转成0
isNaN(undefined);  //true, undefined转换成Number就是NaN
isNaN('a'); //true

```

面试题常考类型转换这部分

## 函数基础

函数是一种解耦合的方式。模块的单一责任制。

函数声明的方法：

```JavaScript
function test() {
    for (var i = 0; i < 10; i++) {
        console.log(i); 
    }
}

// 这里也可以省略test1这个函数名，即匿名函数
var test = function test1() {
    var a = b = 1;
    // 这样是可以调用到的，递归
    test1();
}
console.log(b);   //b是全局变量，因为没有在函数体内声明，所以它在window上


// 去掉名字就是匿名函数了
var test = function() {

}
```

函数传参数的问题

形参和实参数量不相等

```JavaScript

function test(a, b, c) {
    console.log(a, b, c);  //->1 2 undefined
}

test(1,2);

function test(a, b,) {
    console.log(a, b);  //->1 2  不会报错
}

test(1, 2, 3);

```

函数内部如何得到所有实参

```JavaScript

function test(a, b) {
    console.log(arguments);
    // 同样的形参也可以知道 
    console.log(test.length)
}

test(1, 2, 3);
```

arguments是一个数组表示所有的实参

```JavaScript
function test(a, b) {
    b = 3;
    console.log(arguments[1]);  // undefined,因为b对应的实参并没有传进来，所以通过arguments是获取不到的
}
test(1);


// a = 3 和 arguments[0]并不是一个东西
//因为a是存在栈内存中，而arguments是在堆内存中
function test(a, b) {
    a = 3;
    console.log(arguments[0]);   //注意这里结果是 undefined
    //因为arguments[0]并没有对应外面传进来的实参的值
}
test(1, 2);

```

函数返回值

```JavaScript
function test() {
    console.log("End");
}
 JS引擎会自动在最后面添加上return
```

## 参数默认值

```JavaScript

//如果没有传实参，那么初始值是undefined
function test(a, b) {
    console.log(a);   //->1
    console.log(b);   //->undefined
}
test(1)

//怎么给b赋值
//通过undefined
//a = 1 这种写法是ES6的
function test(a = 1, b) {
    console.log(a);   
    console.log(b); 
}
test()

//ES5怎么完成给形参赋默认值
//1.通过arguments
function test(a, b) {
    var a = arguments[0] || 1;
    var b = arguments[1] || 2;
    console.log(a + b);
}

test();

//2.通过typeof的方法
function test(a, b) {
    var a, b;
    if (typeof(arguments[0]) !== 'undefined') {
        a = arguments[0];
        
    } else {
        a = 1;
    }

    // 简便写法
    var a = typeof(arguments[0]) !== 'undefined' ? arguments[0] : 1;
    var b = typeof(arguments[1]) !== 'undefined' ? arguments[1] : 2;
    if (typeof(arguments[1]) !== 'undefined') {
        
        b = arguments[1];
    } else {
        b = 2;
    }
    console.log(a + b);
}

test(3, 4)

```

## 预编译

JS代码运行过程

1. 检查通篇的语法错误
1.5 预编译过程
2. 解释一行，执行一行

预编译过程：函数声明整体提升，变量只有声明提升，赋值是不提升的。

```JavaSCript
console.log(a);   //->打印a函数

function a(a) {
    var a = 10;
    var a = function() {

    }
    var a = 1;
}

```

暗示全局变量 imply global variable

```JavaScript

//声明了这里也是全局变量
var a = 1;
// 没有声明直接赋值，为全局变量，所有权归window
b = 2;
console.log(window.b);

window = {
    a: 1,
    b: 2
}

// b直接存到window里面了
function test() {
    var a = b = 1;
}
```

预编译

AO: activation object 活跃对象即函数上下文 

```JavaScript

 function test(a) {
     console.log(a);
     var a = 1;
     console.log(a);
     function a(){}
     console.log(a);
     var b = function(){}
     console.log(b);
     function d(){}
 }
 test(2);

 上面这个函数的AO
 第一步：把声明了的变量赋值为undefined
 第二步：把实参赋值给形参
 第三步：寻找函数声明，赋值函数体
 上面是预编译，然后是执行
 第四步：执行函数
 AO = {
     a: undefined,   ->2  -> function a(){}  -> 1
     b: undefined,
     d: function d(){}
 }

 根据console.log的位置来看当时不同变量的值就行了

 function test(a, b) {
     console.log(a);
     c = 0;
     var c;
     a = 5;
     a = 6;
     console.log(b);
     function b(){}
     function d(){}
     console.log(b);
 }
test(1);   //-> 1 6 6 
 AO = {
     a: undefined, ->1,
    //  这里是先函数声明提升，再赋值的
     b: undefined, ->function b(){} -> 6
     c: undefined,
     d: function d(){}
 }


 var a = 1;
 function a() {
     console.log(2);
 }
 console.log(a);

 GO global object 全局上下文

 第一步找变量
 第二步找函数声明
 第三步执行

 GO = {
     a: undefined -> function a(){} -> 1;
 }

 GO实际上就等于window

 console.log(a, b);  // 
 function a(){}
 var b = function(){}
 GO = {
     b: undefined,
     a: function a(){}
 }

 function test() {
     var a = b = 1;
     console.log(b);
 }

GO 看到test函数，产生AO,AO中没有b，到GO中找b
 GO = {
     b: 1
 }

 AO = {
     a: undefined  -> 1
 }


 var b = 3;
 console.log(a);   //function a(a){}
 function a(a) {
     console.log(a);  //function a(){}
     var a = 2;
     console.log(a);  // 2
     function a() {
         var b = 5;
         console.log(b);  //5
     }
 }

 a(1);


a = 1;
function test() {
    console.log(a);  // undefined
    a = 2;
    console.log(a);  // 2
    var a = 3;
    console.log(a);  // 3
}
test();
var a;
为什么会第一个会打印 undefined 而不是 1
因为AO里面是有a的，所以不会去GO里面找a，并且变量声明提升，赋值不提升，所以undefined


function test() {
    console.log(b);  //undefined
    if (a) {
        var b = 2;
    }
    c = 3;
    console.log(c);   // 3
}

var a;
test();
a = 1;
console.log(a);   // 1

GO = {
    a: undefined
    test: function test(){}
}

AO = {
    // b是有的，因为预编译根本不看if，只要有变量就行
    b: undefined
}


```


## 作用域和作用域链

函数也是一种对象类型（引用类型），对象有些属性是我们无法访问的，是JS引擎固有的隐式属性

[[scope]]隐式属性

1. 函数创建时，生成的一个JS内部的隐式属性
2. 函数存储作用域链的容器，而作用域链中存放的是AO/GO
   AO:函数的执行期上下文
   GO:全局的执行期上下文

函数执行完成之后，AO是要销毁的
看个例子

```JavaScript
function a() {
    function b() {
        var b = 2;
    }
    var a = 1;
    b();
}
var c = 3;
a();
```

上面这段代码的作用域链

作用域链就是像一个数组保存了AO和GO。



## 闭包

当内部函数被返回到外部并保存时，一定会产生闭包。闭包会产生原来的作用域链不是放，过度的闭包可能会导致内存泄漏，或加载过慢。



从AO和GO角度分析以下例子：









闭包返回两个函数

```javascript
function test() {
  var n = 100;
  function add() {
    n++;
    console.log(n);
  }
  
  function reduce() {
    n--;
    console.log(n);
  }
  return [add,reduce];
}

var arr = test();
arr[0]();  //101
arr[1]();  //100
```

虽然 test函数已经销毁掉了，但是由于通过arr变量保存了test()的返回值，test()的AO依然被test里面的函数抓着的，依然能够操作test的AO里面的变量





## 立即执行函数

IIFE - immediately-invoked function expression 自动执行，执行完成以后立即释放。

两种写法：

```javascript
(function() {
  
})();

(function() {
  
}());  //w3c建议方式
```

例子：

```javascript
(function(a, b) {
  console.log(a + b);   // 3
}(1, 2));
```

()包起来的，不管里面是变量还是函数还是什么，都会变成表达式。



Wrong example:

```javascript
// 像这样写立即执行函数是不行的
function test() {
  
}();  

// this one works though!
var test = function() {
  console.log(1);
}();


var test1 = function() {
  console.log(2);    // 2
}();
console.log(test1);    // undefined,因为没有return值出来
```

总结：一定是表达式才能被执行符号执行。

还有另一种方法，把函数声明变成表达式，就是在函数声明前面加运算符

```javascript
+ function test() {
  console.log(1);
}(); // 像这样的就可以被立即执行

1 && function test() {
  console.log(1);
}();
```



面试题：

```javascript
function test(a) {
  
}(6);   // 这样是不会报错的，因为传值了，所以JS引擎还是优先认为(6)是一个表达式，如果不传值，就认为是立即执行会报错


function test() {
  var arr = [];
  
  for (var i = 0; i < 10; i++) {
    arr[i] = function() {
      document.write(i + ' ');
    }
  }
  
  return arr;   // return了9个匿名函数
}

var myArr = test();

console.log(myArr);  // 打印10个f

for (var j = 0; j < 10; j++) {
  myArr[j]();   //页面上输出10个10
}


第三种方法：
function test() {
  var arr = [];
  
  for (var i = 0; i < 10; i++) {
    (function(j) {
      arr[j] = function() {
        document.write(j + ' ');
      }
    })(i);
  }
  return arr;
}
var myArr = test();
for (var j = 0; j < 10; j++) {
  myArr[j]();
}
```

再来看个面试题：

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
<script type="text/javascript">
var oLi = document.querySelectorAll('li');
  
  for (var i = 0; i < oLi.length; i++) {
    oLi[i].onclick = function() {
      console.log(i);   // 不管点哪个都返回5
    }
  }
</script>
因为for循环执行结束i==5, 然后是把一个匿名函数作为点击事件的回调函数，并且在for循环的作用域内有个函数，这个函数在for循环结束后并没有被销毁，形成了闭包，所以这个函数每次点击打印的都是5
```

面试题：

```javascript
var num = (1, 2);  // 这种返回的是后面那个
console.log(num);  // 2

var fn = (
	function test1() {
    return 1;
  },
  
  function test2() {
    return '2';
  }
)();   // 逗号运算返回的是逗号后面这个，所以立即执行的是后面这个函数

console.log(typeof(fn));  //string
```



```javascript
var a = 10;
if (function b(){}) {
  a += typeof(b)   
}
console.log(a);  // 10undefined
分析：(function b(){}) 这个函数声明被括号包裹，所以是一个表达式，如果是表达式，那么里面的函数名会被忽略，所以后面的b是undefined
```



作业：

累加器

```javascript
function test() {
  var num = 0;
  
  function add() {
    console.log(++num)
  }
  return add;
}
var add = test();
add();
add();
add();
```

一个班级，学生名字保存在一个数组里，两个方法写在函数中的一个对象中，第一个方法加入班级，第二个方法离开班级，每次加入或离开，都需要打印新的学生名单

```javascript
function myClass() {
  students: [];
  
  var operations = {
    join: function(name) {
      students.push(name);
      console.log(students);
    },
    leave: function(name) {
      for (var i = 0; i < students.length; i++) {
        var item = students[i];
        
        if(item === name) {
          students.splice(i, 1);
        }
      }
      
      //或者也可以用indexOf的方法
//      var idx = students.indexOf(name);
//      if(idx !== -1) {
//        students.splice(idx, 1);
//      }
//      console.log(idx);
      
      console.log(students);
    }
  }
  
  return operations;
  
}

var obj = myClass();
obj.join('Tom');
obj.join('Lyle');
obj.join('Betty');
```



## 构造函数

```javascript
function Car(color, brand) {
  this.color = color;
  this.brand = brand;
  this.drive = function() {
    console.log('I am running');
  }
}

var car = new Car('red', 'Mazda');
console.log(car.color);
car.drive();

问题是，如果不实例化构造函数，那么this存在吗？
function Car(color) {
  this.color = color;
}
Car();
this是存在于这个函数的AO中的，并指向window,上面等同于 window.color = color
如果实例化了，那么this就指向实例化的这个对象
```

对于构造函数来说，实例化的时候就相当于普通函数被调用的时候，会产生函数的AO。

AO = {

​	this: {

​	color: color,

​	brand: brand

}

}

并且AO中会默认添加一个this对象，this对象并不是空的，并且构造函数会默认 return this 

所以 new 关键字实际上做的事情就是在函数中加上了 this，并且改变了this的指向，从指向window到指向实例化的这个对象。构造函数如果显式return一个引用值，那么是会返回这个引用值，如果return一个原始值，那么是不管的，默认 return this



## 包装类

```javascript
var a = 1;
var c = 3;
var b = new Number(a);
b.len = 1;
b.add = function(){
  console.log(1);
}
var d = b + 1; 
console.log(d);   // 2
```

包装类和原始值作运算，得到的结果是原始值。原始值没有自己的方法和属性，但包装类可以有



包装类：Number, String, Boolean

```javascript
var a = 'abc'; // abc

var aa = new String('abc'); // String

var bb = aa + 'bcd';  // abcbcd
```



另一个问题，对比一下：

```javascript
var a = 123;
a.len = 3;
console.log(a.len); // undefined

var str = 'abc';
console.log(str.length);  // 3
```

为啥都是原始值，但第二个有length属性，这涉及到包装类的


















# 面试题

```JavaScript
if (typeof(a) && (-true) + (+undefined) + '') {
    console.log('通过了');  //true
} else {
    console.log('没通过')
}

console.log(typeof(a)); // 这里如果直接打印a，会报not defined错误，但是加上typeof(a)是undefined,并且是字符串

-true隐式转换是-1，undefined隐式转换是NaN，他们相加是NaN


if (1 + 5 * '3' === 16) // true


console.log(!!' ' + !!'' - !!false || '未通过');  // 1

//-------------------------------
function test() {
    return a;
    a = 1;
    function a(){}
    var a = 2;
}
console.log(test());  // function a(){}

如果改变return的位置
console.log(test());
function test() {
    a = 1;
    function a(){}
    var a = 2;
    return a;
}


//--------------------------------
a = 1;
function test(e) {
    function e(){}
    arguments[0] = 2;
    console.log(e);  // 2
    if (a) {
        var b = 3;
    }
    var c;
    a = 4;
    var a;
    console.log(b);  // undefined
    f = 5;
    console.log(c);  // undefined
    console.log(a);  //4
}
var a;
test(1);
console.log(a);  // 1
console.log(f);  // 5

```
