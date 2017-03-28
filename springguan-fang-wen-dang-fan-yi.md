spring官方文档：http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/

一、Spring框架概述

Spring框架是一个轻量级的解决方案，可以一站式地构建企业级应用。Spring是模块化的，所以可以只使用其中需要的部分。可以在任何web框架上使用控制反转（IoC），也可以只使用Hibernate集成代码或JDBC抽象层。它支持声明式事务管理、通过RMI或web服务实现远程访问，并可以使用多种方式持久化数据。它提供了功能全面的MVC框架，可以透明地集成AOP到软件中。

Spring被设计为非侵入式的，这意味着你的域逻辑代码通常不会依赖于框架本身。在集成层（比如数据访问层），会存在一些依赖同时依赖于数据访问技术和Spring，但是这些依赖可以很容易地从代码库中分离出来。

本文档是Spring框架的参考指南，如果你有任何请求、评论或问题，请给我们发邮件，关于框架本身的问题将在StackOverflow上讨论（见https://spring.io.questions）。

1. Spring入门

这篇参考指南提供了Spring框架的详细信息，包括了对所有功能的全面理解，同时也包括一些重要概念的背景（比如，依赖注入）。

如果你才开始使用Spring，可以通过创建一个基于Spring Boot的应用开始使用Spring框架。Spring Boot提供了一种快速创建Spring应用的方式，它基于Spring框架，支持约定优于配置，使你可以尽快启动并运行。

可以使用start.spring.io或遵循入门指南（比如，构建RESTful web应用入门）生成一个基本的项目。除了易于理解，这些指南聚集于一个个任务，它们大部分都是基于Spring Boot的，同时也包含了Spring包下的其它项目，以便你可以考虑何时使用它们解决特定的问题。

2. Spring框架简介

Spring框架是基于Java平台的，它为开发Java应用提供了全方位的基础设施支持，并且它很好地处理了这些基础设施，所以你只需要关注你的应用本身即可。

Spring可以使用POJO（普通的Java对象，plain old Java objects）创建应用，并且可以将企业服务非侵入式地应用到POJO。这项功能适用于Java SE编程模型以及全部或部分的Java EE。

那么，做为开发者可以从Spring获得哪些好处呢？

不用关心事务API就可以执行数据库事务；
不用关心远程API就可以使用远程操作；
不用关心JMX API就可以进行管理操作；
不用关心JMS API就可以进行消息处理。
译者注：①JMX，Java Management eXtension，Java管理扩展，是一个为应用程序、设备、系统等植入管理功能的框架。JMX可以跨越一系列异构操作系统平台、系统体系结构和网络传输协议，灵活的开发无缝集成的系统、网络和服务管理应用。②JMS，Java Message Service，Java消息服务，是Java平台上有关面向消息中间件(MOM)的技术规范，它便于消息系统中的Java应用程序进行消息交换,并且通过提供标准的产生、发送、接收消息的接口简化企业应用的开发。

2.1 依赖注入（DI）和控制反转（IoC）

一个Java应用程序，从受限制的嵌入式应用到n层的服务端应用，典型地是由相互合作的对象组成的，因此，一个应用程序中的对象是相互依赖的。

Java平台虽然提供了丰富的应用开发功能，但是它并没有把这些基础构建模块组织成连续的整体，而是把这项任务留给了架构师和开发者。你可以使用设计模式，比如工厂模式、抽象工厂模式、创建者模式、装饰者模式以及服务定位器模式等，来构建各种各样的类和对象实例，从而组成整个应用程序。这些设计模式是很简单的，关键在于它们根据最佳实践起了很好的名字，它们的名字可以很好地描述它们是干什么的、用于什么地方、解决什么问题，等等。这些设计模式都是最佳实践的结晶，所以你应该在你的应用程序中使用它们。

Spring的控制反转解决了上述问题，它提供了一种正式的解决方案，你可以把不相干组件组合在一起，从而组成一个完整的可以使用的应用。Spring根据设计模式编码出了非常优秀的代码，所以可以直接集成到自己的应用中。因此，大量的组织机构都使用Spring来保证应用程序的健壮性和可维护性。

背景

2004年Martin Fowler在他的网站上提出了关于控制反转（IoC，Inversion of Control）的问题，“The question is, what aspect of control are [they] inverting?”，后来，他又建议重新命名这项原则，使其可以自我解释，从而提出了依赖注入（DI，Dependency Injection）的概念。

2.2 模块

Spring大约包含了20个模块，这些模块组成了核心容器（Core Container）、数据访问/集成（Data Access/Integration）、Web、AOP（面向切面编程，Aspect Oriented Programming）、Instrumentation、消息处理（Messaging）和测试（Test），如下图：

图 2.1. Spring框架概述 