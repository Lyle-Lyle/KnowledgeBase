

# 知识点



视图函数里面，render 方法的context参数







# 简介

项目的文件目录介绍

![image-20220305130814989](/Users/lyle/Library/Application Support/typora-user-images/image-20220305130814989.png)

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305211840078.png" alt="image-20220305211840078" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305214125424.png" alt="image-20220305214125424" style="zoom: 33%;" />

Django是一个重框架，已经内置了很多功能了。这个settings.py就是当前项目的配置

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305225005057.png" alt="image-20220305225005057" style="zoom: 33%;" />





项目APP的创建

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305131112214.png" alt="image-20220305131112214" style="zoom:50%;" />

如果你的项目比较大，你可以创建多个app来划分功能模块



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305131517004.png" alt="image-20220305131517004" style="zoom:50%;" />





- APP创建了还需要注册，在settings.py的installed_APPS中注册
- 编写URL和视图函数的对应关系在 urls.py中
- 编写视图函数 views.py

![image-20220305160144980](/Users/lyle/Library/Application Support/typora-user-images/image-20220305160144980.png)

- 启动Django项目

  - pycharm
  - python manage.py runserver

  

  SQLite是一个嵌入式的轻量级数据库

  

  

  

# URL和视图函数

Django是怎么处理URL请求的

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306105434403.png" alt="image-20220306105434403" style="zoom:33%;" />

视图函数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306110122232.png" alt="image-20220306110122232" style="zoom: 33%;" />



## 路由配置

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306120258236.png" alt="image-20220306120258236" style="zoom: 33%;" />



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306121134981.png" alt="image-20220306121134981" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306121341321.png" alt="image-20220306121341321" style="zoom:33%;" />

视图转换器的作用例子

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306122155758.png" alt="image-20220306122155758" style="zoom: 33%;" />

这样能匹配所有int的url

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306122642146.png" alt="image-20220306122642146" style="zoom: 33%;" />

这是URL，再看下视图函数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306124720294.png" alt="image-20220306124720294" style="zoom:33%;" />

re_path用来做更精确的匹配

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306124607141.png" alt="image-20220306124607141" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306125234987.png" alt="image-20220306125234987" style="zoom: 33%;" />



路由的拆分

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306160647676.png" alt="image-20220306160647676" style="zoom: 33%;" />





# Model



通过models的定义来实现数据库表的定义

makemigrations 创建model

migrate 在数据库中创建对应的表



更改Django的数据库，在settings.py中DATABASES配置

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306172648762.png" alt="image-20220306172648762" style="zoom:50%;" />





# Template

- templates文件夹可以建立在项目根目录下，也可以放在app的目录里面

  

  这个里面就是放的HTML文件，还需要一个static文件夹来存放静态文件

  <img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220305173233336.png" alt="image-20220305173233336" style="zoom: 50%;" />

  这种 load static 引入方式比绝对路径要好，因为比较好替换



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306181224361.png" alt="image-20220306181224361" style="zoom:50%;" />

render实际上也会返回 HttpResponse



模板的语法

![image-20220306222445182](/Users/lyle/Library/Application Support/typora-user-images/image-20220306222445182.png)

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306185730184.png" alt="image-20220306185730184" style="zoom:50%;" />

对应的模板

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220306185839769.png" alt="image-20220306185839769" style="zoom:50%;" />

![image-20220306225045781](/Users/lyle/Library/Application Support/typora-user-images/image-20220306225045781.png)



模板渲染流程

![image-20220306225846824](/Users/lyle/Library/Application Support/typora-user-images/image-20220306225846824.png)





















模板的继承



















