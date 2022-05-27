

狂神 博客：https://mp.weixin.qq.com/mp/homepage?__biz=Mzg2NTAzMTExNg==&hid=3&sn=456dc4d66f0726730757e319ffdaa23e&scene=18#wechat_redirect

Java3y Spring: https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247483942&idx=1&sn=f71e1adeeaea3430dd989ef47cf9a0b3&chksm=ebd74327dca0ca3141c8636e95d41629843d2623d82be799cf72701fb02a665763140b480aec&scene=21###wechat_redirect



配合视频的文档使用

# IOC

框架就是其他人写好的一个软件，所以学习框架，我们需要：

1. 学习怎么使用框架，知道框架能干什么
2. 学习框架实现的原理



IOC（Inversion of Control）：控制反转是一个概念，思想。即我们要把对象的创建、复制、管理工作都交给代码之外的容器来做，也就是其他外部资源来做。



Java中创建对象有哪些方式：

1. 构造方法  new
2. 反射
3. 序列化
4. 克隆
5. IOC （不仅是创建对象哈，还有管理对象之间的关系什么的）
6. 动态代理



IOC的体现：

servlet：我们在 web.xml 中注册 servlet，使用<servlet-name> myservlet </servlet-name>

​																		<servlet-class>com.bjpwernode.controller.MyServlet</servlet-class>

我们并没有主动创建servlet对象，servlet是Tomcat这个容器来为我们创建的。

而且 Tomcat容器中不仅有 Servlet对象，还有 Listener，Filter对象



IOC的技术实现：

DI 是 IOC的技术实现

DI（Dependency Injection）：依赖注入，只需要在程序中提供要使用的对象名称就可以了，至于对象如何在容器中创建、赋值，查找都由容器内部实现

Spring是使用的DI实现了IOC的功能，Spring底层创建对象，使用的是反射。

DI的实现语法有两种：基于XML文件和基于注解



Spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

   <!--bean就是java对象 , 由Spring创建和管理-->
  <!-- 
	id：对象的自定义名称，唯一值，Spring通过这个名称找到对象
	class:类的全限定名称（不能是接口，因为Spring是反射机制创建对象，必须使用类）
-->
   <bean id="hello" class="com.kuang.pojo.Hello">
       <property name="name" value="Spring"/>
   </bean>

</beans>
```

通过以上配置文件，Spring就能完成 SomeService someService = new SomeServiceImpl()

Spring是把创建好的对象放入到map中的，Spring框架有一个map存放对象的。

例如 springMap.put("someService", new SomeServiceImpl())

一个 Bean标签声明一个对象

```java
@Test
public void test02() {
  //1. 指定Spring配置文件的名称
    String config = "beans.xml";
  //2. 创建表示Spring容器的对象，ApplicationContext(这是接口)
ApplicationContext ac  new ClassPathXmlApplicationContext(config);
  
  //从容器中拿到对象
 //getBean的参数是配置文件中的bean的id值
SomeService service = (SomeService) ac.getBean("someService");
  
}
```



Spring创建对象的时机

Spring通过配置文件找到bean id 对应的类的全类名，并通过反射机制调用类的构造方法来创建对象，并把创建好的对象放到IOC容器中，默认调用无参数构造方法来创建对象

Spring默认创建对象的时机是在读取配置文件，创建Spring容器时，会创建配置文件中所有的对象



获取Spring容器中Java对象的信息

```java
@Test
public void test02() {
  //1. 指定Spring配置文件的名称
    String config = "beans.xml";
  //2. 创建表示Spring容器的对象，ApplicationContext(这是接口)
ApplicationContext ac  new ClassPathXmlApplicationContext(config);
  
  //从容器中拿到对象
 //getBean的参数是配置文件中的bean的id值
SomeService service = (SomeService) ac.getBean("someService");
  
  //获取容器中定义的对象的数量
  int nums = ac.getBeanDefinitionCount();
  System.out.println("容器中定义的对象数量:" + nums);
  //容器中每个定义的对象的名称
  for (String name : names) {
    System.out.println(name)
  }
  
  
}
```



Spring创建非自定义类的对象

```xml
创建一个已经存在的某个类的对象
<bean id="mydate" class="java.util.Date"/>
```





DI的语法分类

1. set注入（）：Spring调用类的set方法，在set方法可以实现属性的赋值，80%左右都是用set注入

注入就是赋值的意思

简单类型：Spring规定的Java的基本类型和String都是简单类型

```xml
<bean id="xx" class="yyy">
  一个property只能给一个属性赋值
	<property name="属性名字" value="此属性的值"/>
         
</bean>
```

那要是没有set方法怎么办？

会出异常

set注入找的是name对应的setName的方法，就算没有name这个属性，也是可以的，并且就算这个类不是自定义的类，只要有对应的setXXX方法就可以。

引用类型的set注入

```xml
<bean id="xxx" class="yyy">
	<property name="属性名称" ref="bean的id(就是一个对象)" />
</bean>
```





2. 构造注入，Spring调用类的有参数构造方法，创建对象，在构造方法中完成赋值

   构造注入使用 <constructor-arg>标签

   标签属性：

   name: 表示构造方法的形参名

   index: 表示构造方法的参数的位置，参数从左往右位置是0,1,2 的顺序

   value: 构造方法的形参类型是简单类型的，使用value

   ref: 构造方法的形参类型是引用类型的，使用ref

```xml
<bean id="myStudent" class="com.bjpowernode.ba03.Student">
	<constructor-arg name="myname" value="张三"/>
  <constructor-arg name="myage" value="20"/>
  <constructor-arg name="mySchool" value="School"/>
</bean>

<bean id="School" class"com.bjpowernode.ba03.School">
	<property name="name" value="北京大学"/>
  <property name="address" value="北京的海淀区"/>
</bean>
```

不用关心顺序，因为Spring会先创建出所有的对象

构造注入文件对象

```xml
<bean id="myfile" class="java.io.File">
	<constructor-arg name="parent" value="文件路径"/>
  <constructor-arg name="child" value="readme.txt"/>
</bean>
```





可以看到上面的创建一个对象的话，每一个属性都得在XML配置文件中被赋值

引用类型的自动注入，常用 byName和byType，只有引用类型可以，普通原始类型不行



byName: Java类引用类型的属性名和Spring容器中Bean的ID一样，且数据类型是一样的，才能注入

Spring会自动去找引用类型的属性，然后把属性名和XML配置文件中的bean id 比较看有没有一样的

```java
<bean id="myStudent" class="com.bjpowernode.ba03.Student" autowire="byName">
	<constructor-arg name="myname" value="张三"/>
  <constructor-arg name="myage" value="20"/>
  <constructor-arg name="mySchool" value="School"/>
</bean>
```



byType: Java类中引用类型的数据类型和<bean>中的class属性是同源关系，这样的bean就能赋值给引用类型

同源就是同一类的意思：

1. Java类中引用类型的数据类型和bean的class的值是一样的。
2. Java类中引用类型的数据类型和bean的class值是父子关系或接口实现关系



多配置文件

当你项目类很多的时候，如果你把所有类的声明都写在一个XML配置文件中，文件就变得很大，不好维护

最好是一个模块一个配置文件

https://www.bilibili.com/video/BV1nz4y1d7uy?p=27





## 基于注解的DI

使用注解的步骤：

1. 加入依赖：spring-aop
2. 在类中加入Spring的注解
3. 在spring的配置文件中，加入一个组件扫描器的标签，说明注解在你项目中的位置



学习的注解：

1. @Component
2. @Repository
3. @Service
4. @Controller
5. @Value
6. @Autowired
7. @Resource



@Component用来创建对象等同于<bean>的功能,value相当于bean的id是唯一的，等同于

```xml
<bean id="myStudent" class="com.bjpowernode.ba01.Student" />
```



```java
@Component(value="myStudent")
public class Student {
  
}
```

声明组件扫描器

组件就是Java对象

base-package:指定注解在你的项目中的包名

Spring会扫描 base-package 指定的包和子包中的所有类，找到类中的注解，按照注解的功能创建对象，或给属性赋值

```xml
<context:component-scan base-package=""/>
```



注解更灵活的用法

```java
//省略value
@Component("myStudent")
public class Student {
  
}

//不指定对象名称，由Spring默认提供
//默认名称是类名首字母小写
@Component
public class Student {
  
}
```



还有的创建对象的注解：

@Repository: 放在dao的实现类上表示创建dao对象

@Service: 放在Service的实现类上

@Controller：放在控制器类上，控制器对象就是servlet的功能

以上3个注解的语法和@Component一样，但有额外功能

这3个注解是给项目分层的，不知道是哪一层的就用@Component，知道就用特定层的





扫描多个包

1. 使用多个组件扫描器

```xml
<context:component-scan base-package=""/>
<context:component-scan base-package=""/>
<context:component-scan base-package=""/>
```

2. 使用分隔符分割多个包名

```xml
<context:component-scan base-package="com.lyle.Student;com.lyle.Books"/>
```

3. 指定父包

```xml
<context:component-scan base-package="com.lyle"/>
```





### 简单属性赋值@Value

属性：Value是String类型的

位置：1. 在属性定义的上面，无需set方法，推荐使用

2. 在set方法上面

```java
@Value(value = "Lyle")
private String name;
@Value(value = "29")
private Integer age;

@Value("30")
public void setAge(Integer age) {
  
}
```



## 引用类型属性赋值

@Autowired: Spring框架提供的注解，实现引用类型的赋值

spring中通过注解给引用类型赋值，使用的是自动注入的原理，支持byType, byName，默认是byType

位置：1. 在属性定义的上面，无需set方法，推荐使用

2. 在set方法上面

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220220110134409.png" alt="image-20220220110134409" style="zoom:50%;" />

如果要使用byName的方式

1. 在属性上面加入@Autowired
2. 在属性上面加入@Qualifier(value="bean的id")：表示使用指定名称的bean完成赋值



Autowired的required属性是一个 boolean类型，默认true，如果引用类型赋值失败，程序报错，执行终止

如果required为false, 引用类型如果赋值失败，程序继续执行，引用类型是null。

推荐使用 true



@Resource是JDK中的注解，Spring提供了对这个注解的支持，可以使用这个注解对引用类型赋值，也是自动注入，支持byName 和 byType 默认是 byName，先使用byName,如果失败，再使用 byType





# AOP



## 动态代理

![image-20220220113506172](/Users/lyle/Library/Application Support/typora-user-images/image-20220220113506172.png)

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220220113906665.png" alt="image-20220220113906665" style="zoom:50%;" />



在原有的代码不改变的前提下，给目标类增加功能。









AOP底层就是采用动态代理模式实现的，可以使用JDK和cglib两种方式

AOP就是动态代理的规范化，把动态代理的实现步骤和方式都定义好了，让开发人员用一种统一的方式使用动态代理

术语和AOP实现框架

Aspect：切面，表示增强的功能，就是一堆代码，完成一个功能。非业务功能。常见的切面功能有日志、事务、统计信息、参数检查、权限验证

JointPoint: 连接点，连接业务方法和切面的位置

Pointcut：切入点，指多个连接点方法的集合

目标对象：给哪个类的方法增加功能，这个类就是目标对象

Advice：通知表示切面功能执行的时间



aop的技术实现框架：

1. Spring在内部实现了aop规范，能做aop的工作，我们在工作中很少用Spring的aop，因为比较笨重
2. aspectj是一个开源的aop框架，Spring中集成了aspectj

aspectj实现aop有2种方式:

1. 使用xml配置文件：配置全局事务
2. 使用注解，一般都使用注解，aspectj有5个注解



学习aspectj框架的使用

1. 切面的执行时间，这个执行时间在规范中叫做Advice（通知，增强）

   使用以下注解表示，也可以用xml文件

   @Before

   @AfterReturning

   @Around

   @AfterThrowing

   @After

2. 表示



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221103440928.png" alt="image-20220221103440928" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221103619257.png" alt="image-20220221103619257" style="zoom:50%;" />





<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221104658962.png" alt="image-20220221104658962" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221104727964.png" alt="image-20220221104727964" style="zoom:50%;" />



使用aspectj的步骤

加入Spring和aspectj的依赖

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221105238661.png" alt="image-20220221105238661" style="zoom:50%;" />



```java
@Aspect
public class myAspect {
  
  // 定义方法，方法是实现切面功能的
 	//方法的定义要求：
  //1. 公共方法public
  //2. 方法没有返回值
  //3. 方法名称自定义
  //4. 方法可以有参数，也可以没有参数
  	//如果有参数，参数不是自定义的，有几个参数类型可以使用
  
  //@Before: 前置通知注解
  //属性：value，是切入点表达式，表示切面的功能执行的位置
  //位置：在方法上面
  @Before(value="execution(public void com.lyle.ServiceImpldoSome(name, age))")
  public void myBefore() {
    //切面要执行的功能代码
  }
}
```

创建Spring的配置文件

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221111907175.png" alt="image-20220221111907175" style="zoom:50%;" />

这个自动代理生成器会根据切入点表达式找到目标对象，然后创建它的代理对象。并且自动代理生成器会把Spring容器中的所有目标对象都一次生成代理对象

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221112333175.png" alt="image-20220221112333175" style="zoom:50%;" />

切入点表达式的花式写法

TODO

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221114502487.png" alt="image-20220221114502487" style="zoom:50%;" />





后置通知

```java
@Aspect
public class MyAspect {
  // 后置通知定义方法，方法是实现切面功能的
  // 方法的定义要求
  //1. 公共方法public
  //2. 方法没有返回值
  //3. 方法名称自定义
  //4. 方法有参数的，推荐是Object，参数名自定义
  
  //@AfterReturning:后置通知
  //属性：1. value：切入点表达式
  //			2. returning 自定义的变量，表示目标方法的返回值,自定义的变量名必须和通知方法的形参名一样
  //位置：在方法定义上面
  // 特点：
  // 1.在目标方法之后执行的
  // 2.能够获取到目标方法的返回值，可以根据这个返回值做不同的处理
  // 3.可以修改这个返回值
  
  @AfterReturning(value="execution(* *..SomeServiceImpl.doOther(..))", returning = "res")
  public void myAfterReturning(Object res) {
    	// Object res 是目标方法执行后的返回值，根据返回值做你的切面功能处理
    System.out.println("后置通知：在目标方法之后执行的，获取的返回值是：" + res)
  }
}
```

如果在后置通知中修改res这个返回值是不会影响原方法的值的，为什么？



环绕通知

```java
@Aspect
public class MyAspect {
  // 环绕通知方法的定义格式
  // 1. public 
  //2. 必须有一个返回值，推荐使用Object
  //3. 方法名称自定义
  //4. 方法有参数，固定的参数 ProceedingJoinPoint
  
  //@Around 环绕通知
  // 属性：value 切入点表达式
  // 位置：在方法的定义上面
  //特点：
  //1. 它是功能最强的通知
  //2. 在目标方法的前和后都能增强功能
  //3. 控制目标方法是否被调用执行
  //4. 修改原来的目标方法的执行结果。影响最后的调用结果
  
  //参数：ProceedingJoinPoint 就等同于 method  作用：执行目标方法
  // 返回值：就是目标方法的执行结果，可以被修改
  
  
  @Around(value = "execution(* *..SomeServiceImpl.doFirst(..))")
  public Object myAround(ProceedingJoinPoint pjp) {
    //实现环绕通知
    Object result = null;
    System.out.println("环绕通知：在目标方法之前，输入时间：" + new Date());
    //1. 目标方法调用
    result = pjp.proceed();  //method.invoke(); Object result = doFirst();
    System.out.println("环绕通知：在目标方法之后，提交事务");
    //2. 在目标方法的前或后加入功能
    
}
}
```



AOP这一部分先跳过一下，需要看一下动态代理视频：





# Spring事务

事务本来是数据库中的概念，

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220221230637639.png" alt="image-20220221230637639" style="zoom:50%;" />





Spring提供一种处理事务的统一模型，能使用统一步骤，完成多种不同数据库访问技术的事务处理

![image-20220221232016924](/Users/lyle/Library/Application Support/typora-user-images/image-20220221232016924.png)



![image-20220222153135130](/Users/lyle/Library/Application Support/typora-user-images/image-20220222153135130.png)



隔离级别主要是在高并发情况下，对事务安全性的一种控制







# SpringMVC

https://zhuanlan.zhihu.com/p/22420952

servlet的本质是什么，它是如何工作的？ - bravo1988的回答 - 知乎 https://www.zhihu.com/question/21416727/answer/690289895

是Servlet的一个升级，Spring MVC在Serlvet基础上增加了一些功能，使得做Web开发更加方便

![image-20220222161014854](/Users/lyle/Library/Application Support/typora-user-images/image-20220222161014854.png)



跟 Java Web阶段的web有什么区别：

![image-20220222161210735](/Users/lyle/Library/Application Support/typora-user-images/image-20220222161210735.png)



SprinbMVC使用步骤：

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220222235115259.png" alt="image-20220222235115259" style="zoom:50%;" />

注册中央调度器

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220223000624894.png" alt="image-20220223000624894" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220223021028544.png" alt="image-20220223021028544" style="zoom:50%;" />

![image-20220224004151610](/Users/lyle/Library/Application Support/typora-user-images/image-20220224004151610.png)

创建控制类

注意体会和servlet的不同

```java
//@Controller:创建处理器对象，对象放在Springmvc容器中
//位置：在类的上面
//和Spring中讲的@Service, @Component
@Controller
public class MyController {
  
  //处理用户提交的请求，springmvc中是使用方法来处理的
  //方法是自定义的，可以有多种返回值，多种参数，方法名称自定义
  
  
  //准备使用doSome方法处理some.do请求
  //@RequestMapping:请求映射，作用是把一个请求地址和方法绑定在一起，一个请求指定一个方法处理
  //value是一个String表示url地址
  //value的值必须是唯一的，不能重复，在使用时，推荐以 "/"
  // 位置：1. 在方法的上面，常用的
  // 2. 在类的上面
  //说明：使用@RequestMapping修饰的方法叫做控制器方法，这个方法可以处理请求
  //返回值：ModelAndView
  //Model:数据，请求处理完成后，要现实给用户的数据
  //View: 视图，比如JSP等等
  
  @RequestMapping(value="/some.do")
  public ModelAndView doSome() {
    
    //添加数据，框架在请求的最后把数据放到 request作用域
    //request.SetAttribute("msg","HelloWorld")
    ModelAndView mv = new ModelAndView();
    mv.addObject("msg","HelloWorld");
    mv.addObject("fun","执行的是doSome方法");
    
    //指定视图,指定视图的完整路径
    //框架对视图执行的forward操作，request.getRequestDispacher("/show.jsp").forward()
    mv.setViewName("/show.jsp");
    return mv
  }
  
}
```



还要创建对象，自动扫描配置组件扫描器

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224014640312.png" alt="image-20220224014640312" style="zoom:50%;" />

然后整个JSP页面就可以渲染数据了

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224004020926.png" alt="image-20220224004020926" style="zoom:50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224012823412.png" alt="image-20220224012823412" style="zoom:50%;" />



<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224013706192.png" alt="image-20220224013706192" style="zoom: 33%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224014553649.png" alt="image-20220224014553649" style="zoom:50%;" />





配置视图解析器

对资源访问进行控制，就是说我们不希望哪些文件能被用户直接在浏览器输URL就能访问

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224132125013.png" alt="image-20220224132125013" style="zoom: 33%;" />

那么视图解析器有什么用？

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224154709518.png" alt="image-20220224154709518" style="zoom: 33%;" />

可以字符串拼接路径

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224154755271.png" alt="image-20220224154755271" style="zoom: 33%;" />

把多个请求交给同一个方法处理

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224232504513.png" alt="image-20220224232504513" style="zoom:50%;" />

@RequestMapping放在类的上面的时候表示所有请求的公共部分，叫做模块名称。这样就可以很方便地更改掉一个模块的所有公共请求路径了





指定请求方式

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224235811684.png" alt="image-20220224235811684" style="zoom: 50%;" />

如果没有指定请求方式，就没有限制，任何请求方式都可以

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220224235614358.png" alt="image-20220224235614358" style="zoom: 33%;" />



处理器方法的参数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220225001051875.png" alt="image-20220225001051875" style="zoom:50%;" />

逐个接收参数

要求：控制器方法的形参名和请求中参数名必须一致，同名的请求参数赋值给同名形参

框架接收参数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220226215807001.png" alt="image-20220226215807001" style="zoom:50%;" />



请求参数名和处理器方法形参名不一样

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220226224431005.png" alt="image-20220226224431005" style="zoom: 50%;" />

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220226232115377.png" alt="image-20220226232115377" style="zoom:50%;" />

对象接收参数

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220226234635776.png" alt="image-20220226234635776" style="zoom:50%;" />

看一下视图页面





总结：所以接收参数就是逐个接收，或者是对象接收。但是逐个接收中的注解@ReqeustParam在对象接收中无法用

逐个接收适合参数少的情况。

所以其实我们讲的其实就是这个Controller的方法。

![image-20220226235853102](/Users/lyle/Library/Application Support/typora-user-images/image-20220226235853102.png)





静态资源的处理问题

https://blog.csdn.net/ITWANGBOIT/article/details/103562221

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220227001627221.png" alt="image-20220227001627221" style="zoom:50%;" />

由图可知，静态资源都是由Tomcat处理的。

Tomcat是怎么处理静态资源的？

Tomcat自己是有默认的Servlet的

<img src="/Users/lyle/Library/Application Support/typora-user-images/image-20220227001608645.png" alt="image-20220227001608645" style="zoom:50%;" />



总结：这部分网上文章很多，看视频有点慢









## SpringMVC核心技术

