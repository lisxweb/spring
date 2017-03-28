[spring](http://lib.csdn.net/base/javaee)官方文档：[http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/)

# 一、Spring框架概述 {#一spring框架概述}

Spring框架是一个轻量级的解决方案，可以一站式地构建企业级应用。Spring是模块化的，所以可以只使用其中需要的部分。可以在任何web框架上使用控制反转（IoC），也可以只使用Hibernate集成代码JDBC抽象层或MVC框架AOP。它支持声明式事务管理、通过RMI或web服务实现远程访问，并可以使用多种方式持久化数据。它提供了功能全面的，可以透明地集成到软件中。

Spring被设计为非侵入式的，这意味着你的域逻辑代码通常不会依赖于框架本身。在集成层（比如数据访问层），会存在一些依赖同时依赖于数据访问技术和Spring，但是这些依赖可以很容易地从代码库中分离出来。

本文档是Spring框架的参考指南，如果你有任何请求、评论或问题，请给我们发邮件https://spring.io.questions，关于框架本身的问题将在StackOverflow上讨论（见）。

## 1. Spring入门 {#1-spring入门}

这篇参考指南提供了Spring框架的详细信息，包括了对所有功能的全面理解，同时也包括一些重要概念的背景（比如，依赖注入）。

如果你才开始使用Spring，可以通过创建一个基于Spring Boot的应用开始使用Spring框架。Spring Boot提供了一种快速创建Spring应用的方式，它基于Spring框架，支持约定优于配置，使你可以尽快启动并运行。

可以使用start.spring.io入门指南或遵循构建RESTful web应用入门（比如，）生成一个基本的项目。除了易于理解，这些指南聚集于一个个任务，它们大部分都是基于Spring Boot的，同时也包含了Spring包下的其它项目，以便你可以考虑何时使用它们解决特定的问题。

## 2. Spring框架简介 {#2-spring框架简介}

Spring框架是基于Java平台的，它为开发Java应用提供了全方位的基础设施支持，并且它很好地处理了这些基础设施，所以你只需要关注你的应用本身即可。

Spring可以使用POJO（普通的Java对象，plain oldJavaJava SEobjects）创建应用，并且可以将企业服务非侵入式地应用到POJO。这项功能适用于Java EE编程模型以及全部或部分的。

那么，做为开发者可以从Spring获得哪些好处呢？

* 不用关心事务API就可以执行数据库事务；
* 不用关心远程API就可以使用远程操作；
* 不用关心JMX API就可以进行管理操作；
* 不用关心JMS API就可以进行消息处理。

译者注：①JMX，Java Management eXtension，Java管理扩展，是一个为应用程序、设备、系统等植入管理功能的框架。JMX可以跨越一系列异构操作系统平台、系统体系结构和网络传输协议，灵活的开发无缝集成的系统、网络和服务管理应用。②JMS，Java Message Service，Java消息服务，是Java平台上有关面向消息中间件\(MOM\)的技术规范，它便于消息系统中的Java应用程序进行消息交换,并且通过提供标准的产生、发送、接收消息的接口简化企业应用的开发。

### 2.1 依赖注入（DI）和控制反转（IoC） {#21-依赖注入di和控制反转ioc}

一个Java应用程序，从受限制的嵌入式应用到n层的服务端应用，典型地是由相互合作的对象组成的，因此，一个应用程序中的对象是相互依赖的。

Java平台虽然提供了丰富的应用开发功能，但是它并没有把这些基础构建模块组织成连续的整体，而是把这项任务留给了架构师和开发者。你可以使用设计模式，比如工厂模式、抽象工厂模式、创建者模式、装饰者模式以及服务定位器模式等，来构建各种各样的类和对象实例，从而组成整个应用程序。这些设计模式是很简单的，关键在于它们根据最佳实践起了很好的名字，它们的名字可以很好地描述它们是干什么的、用于什么地方、解决什么问题，等等。这些设计模式都是最佳实践的结晶，所以你应该在你的应用程序中使用它们。

Spring的控制反转解决了上述问题，它提供了一种正式的解决方案，你可以把不相干组件组合在一起，从而组成一个完整的可以使用的应用。Spring根据设计模式编码出了非常优秀的代码，所以可以直接集成到自己的应用中。因此，大量的组织机构都使用Spring来保证应用程序的健壮性和可维护性。

背景

2004年Martin Fowler在他的网站上提出了关于控制反转（IoC，Inversion of Control）的问题，“The question is, what aspect of control are \[they\] inverting?”，后来，他又建议重新命名这项原则，使其可以自我解释，从而提出了依赖注入（DI，Dependency Injection）的概念。

### 2.2 模块 {#22-模块}

Spring大约包含了20个模块，这些模块组成了核心容器（CoreContainer测试）、数据访问/集成（Data Access/Integration）、Web、AOP（面向切面编程，Aspect Oriented Programming）、Instrumentation、消息处理（Messaging）和（Test），如下图：

**图 2.1. Spring框架概述**  
![](http://img.blog.csdn.net/20160331161910594?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center "spring框架概述")

下面列出了每项功能对应的模块及其主题，它们都有人性的名字（artifact name），这些名字与依赖管理工具中的**artifact id**是相互对应的。

#### 2.2.1 核心容器（Core Container） {#221-核心容器core-container}

核心容器包括**spring-core**，**spring-beans**，**spring-context**，**spring-context-support**和**spring-expression**（SpEL，Spring表达式语言，Spring Expression Language）等模块。

**spring-core**和**spring-beans**模块是Spring框架的基础，包括控制反转和依赖注入等功能。BeanFactory是工厂模式的微妙实现，它移除了编码式单例的需要，并且可以把配置和依赖从实际编码逻辑中解耦。

ContextCore和Bean（**spring-context**）模块是在模块的基础上建立起来的，它以一种类似于JNDI注册的方式访问对象。Context模块继承自Bean模块，并且添加了国际化（比如，使用资源束）、事件传播、资源加载和透明地创建上下文（比如，通过Servelet容器）等功能。Context模块也支持Java EE的功能，比如EJB、JMX和远程调用等。**ApplicationContext**接口是Context模块的焦点。**spring-context-support**提供了对第三方库集成到Spring上下文的支持，比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、模板引擎（FreeMarker, JasperReports, Velocity）等。

**spring-expression**模块提供了强大的表达式语言用于在运行时查询和操作对象图。它是JSP2.1规范中定义的统一表达式语言的扩展，支持set和get属性值、属性赋值、方法调用、访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、选择以及聚合等。

