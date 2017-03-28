spring[http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/官方文档：](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/官方文档：)

# 一、Spring框架概述 {#一spring框架概述}

Spring框架是一个轻量级的解决方案，可以一站式地构建企业级应用。Spring是模块化的，所以可以只使用其中需要的部分。可以在任何web框架上使用控制反转（IoC），也可以只使用Hibernate集成代码JDBC抽象层或MVC框架AOP。它支持声明式事务管理、通过RMI或web服务实现远程访问，并可以使用多种方式持久化数据。它提供了功能全面的，可以透明地集成到软件中。

Spring被设计为非侵入式的，这意味着你的域逻辑代码通常不会依赖于框架本身。在集成层（比如数据访问层），会存在一些依赖同时依赖于数据访问技术和Spring，但是这些依赖可以很容易地从代码库中分离出来。

本文档是Spring框架的参考指南，如果你有任何请求、评论或问题，请给我们发邮件[https://spring.io.questions，关于框架本身的问题将在StackOverflow上讨论（见）。](https://spring.io.questions，关于框架本身的问题将在StackOverflow上讨论（见）。)

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

![](/assets/1.png)

下面列出了每项功能对应的模块及其主题，它们都有人性的名字（artifact name），这些名字与依赖管理工具中的**artifact id**是相互对应的。

#### 2.2.1 核心容器（Core Container） {#221-核心容器core-container}

核心容器包括**spring-core**，**spring-beans**，**spring-context**，**spring-context-support**和**spring-expression**（SpEL，Spring表达式语言，Spring Expression Language）等模块。

**spring-core**和**spring-beans**模块是Spring框架的基础，包括控制反转和依赖注入等功能。BeanFactory是工厂模式的微妙实现，它移除了编码式单例的需要，并且可以把配置和依赖从实际编码逻辑中解耦。

ContextCore和Bean（**spring-context**）模块是在模块的基础上建立起来的，它以一种类似于JNDI注册的方式访问对象。Context模块继承自Bean模块，并且添加了国际化（比如，使用资源束）、事件传播、资源加载和透明地创建上下文（比如，通过Servelet容器）等功能。Context模块也支持Java EE的功能，比如EJB、JMX和远程调用等。**ApplicationContext**接口是Context模块的焦点。**spring-context-support**提供了对第三方库集成到Spring上下文的支持，比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、模板引擎（FreeMarker, JasperReports, Velocity）等。

**spring-expression**模块提供了强大的表达式语言用于在运行时查询和操作对象图。它是JSP2.1规范中定义的统一表达式语言的扩展，支持set和get属性值、属性赋值、方法调用、访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、选择以及聚合等。

#### 2.2.2 AOP和检测（Instrumentation） {#222-aop和检测instrumentation}

**spring-aop**模块提供了面向切面编程（AOP）的实现，可以定义诸如方法拦截器和切入点等，从而使实现功能的代码彻底的解耦出来。使用源码级的元数据，可以用类似于.Net属性的方式合并行为信息到代码中。

**spring-aspects**模块提供了对AspectJ的集成。

**spring-instrument**模块提供了对检测类的支持和用于特定的应用服务器的类加载器的实现。**spring-instrument-tomcat**模块包含了用于tomcat的Spring检测代理。

#### 2.2.3 消息处理（messaging） {#223-消息处理messaging}

Spring 4 包含的**spring-messaging**模块是从Spring集成项目的关键抽象中提取出来的，这些项目包括**Message**、**MessageChannel**、**MessageHandler**和其它服务于消息处理的项目。这个模块也包含一系列的注解用于映射消息到方法，这类似于Spring MVC基于编码模型的注解。

#### 2.2.4 数据访问与集成 {#224-数据访问与集成}

数据访问与集成层包含JDBC、ORM、OXM、JMS和事务模块。  
（译者注：JDBC=Java Data Base Connectivity，ORM=Object Relational Mapping，OXM=Object XML Mapping，JMS=Java Message Service）

**spring-jdbc**模块提供了JDBC数据库抽象层，它消除了冗长的JDBC编码和对供应商特定错误代码的解析。

**spring-tx**模块支持编程式事务和声明式事务，可用于实现了特定接口的类和所有的POJO对象。  
（译者注：编程式事务需要自己写beginTransaction\(\)、commit\(\)、rollback\(\)等事务管理方法，声明式事务是通过注解或配置由spring自动处理，编程式事务粒度更细）

**spring-orm**模块提供了对流行的对象关系映射JPAAPI的集成，包括JDOHibernate、和等。通过此模块可以让这些ORM框架和spring的其它功能整合，比如前面提及的事务管理。

**spring-oxm**模块提供了对OXM实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等。

**spring-jms**模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了**spring-messaging**模块。

#### 2.2.5 Web {#225-web}

Web层包括**spring-web**、**spring-webmvc**、**spring-websocket**、**spring-webmvc-portlet**等模块。

**spring-web**模块提供面向web的基本功能和面向web的应用上下文，比如多部分（multipart）文件上传功能、使用Servlet监听器初始化IoC容器等。它还包括HTTP客户端以及Spring远程调用中与web相关的部分。

**spring-webmvc**模块（即Web-Servlet模块）为web应用提供了模型视图控制（MVC）和REST Web服务的实现。Spring的MVC框架可以使领域模型代码和web表单完全地分离，且可以与Spring框架的其它所有功能进行集成。

**spring-webmvc-portlet**模块（即Web-Portlet模块）提供了用于Portlet环境的MVC实现，并反映了**spring-webmvc**模块的功能。

#### 2.2.6 Test {#226-test}

**spring-test**模块通过JUnit和TestNG组件支持单元测试集成测试和加载缓存。它提供了一致性地模拟对象和Spring上下文，也提供了用于单独测试代码的（mock object）。

### 2.3 使用场景 {#23-使用场景}

前面提及的构建模块使得Spring在很多场景成为一种合理的选择，不管是资源受限的嵌入式应用还是使用了事务管理和web集成框架的成熟的企业级应用。

**图2.2. 典型的成熟的Spring web应用程序**

![](/assets/2.png)

Spring的声明式事务管理hibernate可以使web应用完成事务化，就像使用EJB容器管理的事务。所有客制的业务逻辑都可以使用简单的POJO实现，并用Spring的IoC容器进行管理。另外，还包括发邮件和验证功能，其中验证功能是从web层分离的，由你决定何处执行验证。Spring的ORM可以集成JPA、和JDO等，比如，使用Hibernate时，可以继续使用已存在的映射文件和标准的Hibernate的SessionFactory配置。表单控制器无缝地把web层和领域模型集成在一起，移除了ActionForms和其它把HTTP参数转换成领域模型的类。

**图2.3. 使用第三方web框架的Spring中间件**

![](/assets/3.png)

一些场景可能不允许你完全切换到另一个框架。然而，Spring框架不强制你使用它所有的东西，它不是非此即彼（all-or-nothing）的解决方案。前端使用Struts、Tapestry、JSF或别的UI框架可以和Spring中间件集成，从而使用Spring的事务管理功能。仅仅只需要使用**ApplicationContext**连接业务逻辑，并使用**WebApplicationContext**集成web层即可。

**图2.4. 远程调用使用场景**

![](/assets/4.png)

当需要通过web服务访问现有代码时，可以使用Spring的**Hessian-**，**Burlap-**，**Rmi-**或者**JaxRpcProxyFactory**类，远程访问现有的应用并非难事。

**图2.5. EJB-包装现有的POJO**

![](/assets/5.png)

Spring框架也为EJB提供了访问抽象层，可以重新使用现有的POJO并把它们包装到无状态的会话bean中，以使其用于可扩展的安全的web应用中。

#### 2.3.1 依赖管理和命名约定 {#231-依赖管理和命名约定}

依赖管理和依赖注入是两码事。为了让应用程序拥有这些Spring的非常棒的功能（如依赖注入），需要导入所需的全部jar包，并在运行时放在classpath下，有可能的话编译期也应该放在classpath下。这些依赖并不是被注入的虚拟组件，而是文件系统上典型的物理资源。依赖管理的处理过程涉及到定位这些资源、存储并添加它们到classpath下。依赖可能是直接的（比如运行时依赖于Spring），也可能是间接的（比如依赖于**commons-dbcp**，**commons-dbcp**又依赖于**commons-pool**）。间接的依赖又被称作“传递”，它们是最难识别和管理的。

如果准备使用Spring，则需要拷贝一份所需模块的Spring的jar包。为了便于使用，Spring被打包成一系列的模块以尽可能地减少依赖，比如，如果不是在写一个web应用，那就没必要引入spring-web模块。这篇文档中涉及到的Spring模块，我们使用**spring-\***或**spring-\*.jar**的命名约定，其中，**\***代表模块的短名字（比如，**spring-core**、**spring-webmvc**、**spring-jms**等等）。实际使用的jar包正常情况下都是带有版本号的（比如，**spring-core-4.3.0.RELEASE.jar**）。

每个版本的Spring都会在以下地方发布artifact：

* Maven中央仓库，默认的Maven查询仓库，并且不需要特殊的配置就可以使用。许多Spring依赖的公共库也可以从Maven中央仓库获得，并且大部分的Spring社区也使用Maven作为依赖管理工具，所以很方便。Maven中的jar包命名格式为
  **spring-\*-&lt;version&gt;.jar**，其groupId是org.springframework。
* 特别为托管Spring的公共的Maven仓库。除了最终的GA版本，这个仓库也托管了开发的快照版本和里程碑版本。jar包和Maven中央仓库中的命名一致，所以这也是一个获取Spring的开发版本的有用地方，可以和Maven中央仓库中部署的其它库一起使用。这个仓库也包含了捆绑了所有Spring jar包的发行版的zip文件，以便于下载。

因此，首先要做的事就是决定如何管理依赖关系，我们一般推荐使用自动管理的系统，比如Maven、Gradle或Ivy，当然你也可以手动下载所有的jar包。

下面列出了Spring的artifact，每个模块更完整的描述，参考2.2 模块章节。

**表2.1. Spring框架的artifact**

| groupId | artifactId | 描述 |
| :--- | :--- | :--- |
| org.springframework | spring-aop | 基于代理的AOP |
| org.springframework | spring-aspects | 基于切面的AspectJ |
| org.springframework | spring-beans | bean支持，包括Groovy |
| org.springframework | spring-context | 运行时上下文，包括调度和远程调用抽象 |
| org.springframework | spring-context-support | 包含用于集成第三方库到Spring上下文的类 |
| org.springframework | spring-core | 核心库，被许多其它模块使用 |
| org.springframework | spring-expression | Spring表达式语言 |
| org.springframework | spring-instrument | JVM引导的检测代理 |
| org.springframework | spring-instrument-tomcat | tomcat的检测代理 |
| org.springframework | spring-jdbc | JDBC支持包，包括对数据源设置和JDBC访问支持 |
| org.springframework | spring-jms | JMS支持包，包括发送和接收JMS消息的帮助类 |
| org.springframework | spring-messaging | 消息处理的架构和协议 |
| org.springframework | spring-orm | 对象关系映射，包括对JPA和Hibernate支持 |
| org.springframework | spring-oxm | 对象XML映射 |
| org.springframework | spring-test | 单元测试和集成测试组件 |
| org.springframework | spring-tx | 事务基础，包括对DAO的支持及JCA的集成 |
| org.springframework | spring-web | web支持包，包括客户端及web远程调用 |
| org.springframework | spring-webmvc | REST web服务及web应用的MVC实现 |
| org.springframework | spring-webmvc-portlet | 用于Portlet环境的MVC实现 |
| org.springframework | spring-websocket | WebSocket和SockJS实现，包括对STOMP的支持 |

##### Spring的依赖和被依赖 {#spring的依赖和被依赖}

Spring对大部分企业和其它外部工具提供了集成和支持，把强制性的外部依赖降到了最低，这样就不需要为了简单地使用Spring而去寻找和下载大量的jar包了。基本的依赖注入只有一个强制性的外部依赖，那就是日志管理（参考下面关于日志管理选项的详细描述）。

下面列出依赖于Spring的应用的基本配置步骤，首先使用Maven，然后Gradle，最后Ivy。在所有案例中，如果有什么不清楚的地方，参考所用的依赖管理系统的文档或查看一些范例代码——Spring构建时本身使用Gradle管理依赖，所以我们的范例大部分使用Gradle或Maven。

##### Maven依赖关系管理 {#maven依赖关系管理}

如果使用Maven作为依赖管理工具，甚至不需要明确地提供日志管理的依赖。例如，创建应用上下文并使用依赖注入配置应用程序，Maven的依赖关系看起来像下面一样：

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.0.RELEASE</version>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

就这样，注意如果不需要编译Spring API，可以把scope声明为runtime，这是依赖注入使用的典型案例。

上面的示例使用Maven中央仓库，如果使用Spring的Maven仓库（例如，里程碑或开发快照），需要在Maven配置中指定仓库位置。

release版本：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.release</id>
        <url>http://repo.spring.io/release/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

里程碑版本：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.milestone</id>
        <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

快照版本：

```
<repositories>
    <repository>
        <id>io.spring.repo.maven.snapshot</id>
        <url>http://repo.spring.io/snapshot/</url>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
```

##### Maven的“物料清单式”依赖 {#maven的物料清单式依赖}

使用Maven时可能会不小心混合了Spring不同版本的jar包。例如，你可能会发现第三方库或其它的Spring项目存在旧版本的传递依赖。如果没有明确地声明直接依赖，各种各样不可预料的情况将会出现。

为了解决这个问题，Maven提出了“物料清单式”（BOM）依赖的概念。可以在**dependencyManagement**部分导入**spring-framework-bom**以保证所有的Spring依赖（不管直接还是传递依赖）使用相同的版本。

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>4.3.0.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

```
使用BOM的另外一个好处是不再需要指定<version>属性了：
```

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
    </dependency>
<dependencies>
```

##### Gradle依赖关系管理 {#gradle依赖关系管理}

为了在Gradle构建系统中使用Spring仓库，需要在**repositories**部分包含合适的URL：

```
repositories {
    mavenCentral()
    // and optionally...
    maven { url "http://repo.spring.io/release" }
}
```

可以酌情把**repositories**URL中的**/release**修改为**/milestone**或**/snapshot**。一旦仓库配置好了，就可以按Gradle的方式声明依赖关系了。

```
dependencies {
    compile("org.springframework:spring-context:4.3.0.RELEASE")
    testCompile("org.springframework:spring-test:4.3.0.RELEASE")
}
```

##### Ivy依赖关系管理 {#ivy依赖关系管理}

使用Ivy管理依赖关系有相似的配置选项。

在**ivysettings.xml**中添加resolver配置使Ivy指向Spring仓库：

```
<resolvers>
    <ibiblio name="io.spring.repo.maven.release"
            m2compatible="true"
            root="http://repo.spring.io/release/"/>
</resolvers>
```

可以酌情把**root**URL中的**/release**修改为**/milestone**或**/snapshot**。一旦配置好了，就可以按照惯例添加依赖了（在ivy.xml中）：

```
<dependency org="org.springframework"
    name="spring-core" rev="4.3.0.RELEASE" conf="compile->runtime"/>
```

##### 发行版的Zip文件 {#发行版的zip文件}

虽然使用支持依赖管理的构建系统是获取Spring框架的推荐方法，但是也支持通过下载Spring的发行版zip文件获取。

发行版zip文件发布在了Sprng的Maven仓库上（这只是为了方便，不需要额外的Maven或其它构建系统去下载它们）。

浏览器中打开[http://repo.spring.io/release/org/springframework/spring里程碑，并选择合适版本的子目录，就可以下载发行版的zip文件了。发行文件以\*\*-dist.zip\*\*结尾，例如，\*\*spring-framework-{spring-version}-RELEASE-dist.zip\*\*。发行文件也包含快照版本和版本。](http://repo.spring.io/release/org/springframework/spring里程碑，并选择合适版本的子目录，就可以下载发行版的zip文件了。发行文件以**-dist.zip**结尾，例如，**spring-framework-{spring-version}-RELEASE-dist.zip**。发行文件也包含快照版本和版本。)

#### 2.3.2 日志管理 {#232-日志管理}

对于Spring来说日志管理是非常重要的依赖关系，因为a）它是唯一的强制性外部依赖，b）每个人都喜欢从他们使用的工具看到一些输出，c）Spring集成了许多其它工具，它们都选择了日志管理的依赖。应用程序开发者的目标之一通常是在整个应用程序（包括所有的外部组件）的中心位置统一配置日志管理，这是非常困难的因为现在有很多日志管理的框架可供选择。

Spring中强制的日志管理依赖是Jakarta Commons Logging API（JCL）。我们编译了JCL，并使JCL的**Log**对象对继承了Spring框架的类可见。对用户来说所有版本的Spring使用相同的日志管理库很重要：迁移很简单因为Spring保存了向后兼容，即使对于扩展了Spring的应用也能向后兼容。我们是怎么做到的呢？我们让Spring的一个模块明确地依赖于**commons-logging**（JCL的典型实现），然后让所有其它模块都在编译期依赖于这个模块。例如，使用Maven，你想知道哪里依赖了**commons-logging**，其实是Spring确切地说是其核心模块**spring-core**依赖了。

**commons-logging**的优点是不需要其它任何东西就可以使应用程序运转起来。它拥有一个运行时发现算法用于在classpath中寻找其它日志管理框架并且适当地选择一个使用（或者告诉它使用哪个）。如果不需要其它的功能了，你就可以从JDK（java.util.logging或JUL）得到一份看起来很漂亮的日志了。你会发现大多数情况下你的Spring应用程序工作得很好且日志很好地输出到了控制台，这很重要。

##### 不使用Commons Logging {#不使用commons-logging}

不幸的是，**commons-logging**的运行时发现算法虽然对于终端用户很方便，但存在一定的问题。如果我们能让时光倒流，重新开始Spring项目，我们会使用不同的日志管理依赖。首要选择可能是Simple Logging Facade for Java（SLF4J），它也被用于了其它一些使用Spring的工具中。

有两种方式关掉**commons-logging**：

```
1.从spring-core模块中去除对commons-logging的依赖（因为这是唯一明确依赖于commons-logging的地方）
2.依赖于一个特定的commons-logging且把其jar包换成一个空jar包（具体做法参考SLF4J FAQ）
```

如下，在**dependencyManagement**中添加部分代码就可以排除掉**commons-logging**了：

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.3.0.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

现在这个应用可能是残缺的，因为在classpath上没有JCL API的实现，所以需要提供一个新的去修复它。下个章节我们将以SLF4J为例子为JCL提供一个替代实现。

##### 使用SLF4J {#使用slf4j}

SLF4J是一个更干净的依赖，且运行时比**commons-logging**更有效率，因为它使用编译期而非运行时绑定其它日志管理框架。这也意味着你不得不明确地指出运行时想做什么，并定义和配置它。SLF4J可以绑定许多公共的日志管理框架，所以通常你可以选择一个已经使用的，绑定它并配置和管理。

SLF4J可以绑定许多公共的日志管理框架，包括JCL，同时也是其它日志管理框架和它本身的桥梁。所以为了在Spring中使用SLF4J，需要用SLF4J-JCL桥梁代替**commons-logging**依赖。一旦这样做了然后日志记录从Spring内部调用转变成调用SLF4J API，因此，如果应用中的其它库使用了这个API，然后将有一个统一的地方用于配置和管理日志。

通常的选择是把Spring桥接到SLF4J，然后从SLF4J到Log4J提供明确的绑定。需要提供4个依赖关系（且排除掉**commons-logging**）：桥梁、SLF4J API、绑定到Log4J和Log4J的实现本身。在Maven中看起来像下面一样：

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.3.0.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

似乎这么多依赖仅仅用于获取日志。在类加载器问题上，它应该表现得比**commons-logging**更好，尤其是在像OSGi这样严格的容器中。而且，它也有性能优势因为绑定发生在编译期而非运行时。

对于SLF4J用户更普遍的选择是直接绑定Logback，这需要更少的步骤，生成更少的依赖。这样移除了额外的绑定因为Logback直接实现了SLF4J，所以仅仅需要两个库即可而不用四个库（**jcl-over-slf4j**和**logback**）。这样做的话还需要把slf4j-api依赖从其它外部依赖（不是Spring）中排除掉，因为在classpath下仅仅需要一个版本的API。

##### 使用Log4J {#使用log4j}

许多人使用Log4J作为日志管理框架。它是高效和完善的，实际上在构建和测试Spring的时候我们运行时就是使用它。Spring也提供了一些工具用于配置和初始化Log4J，所以某些模块在编译期可以选择依赖于Log4J。

为了使Log4J代替默认的JCL依赖（**commons-logging**），仅仅提供一个配置文件（**log4j.properties**或**log4j.xml**）放在classpath根目录下即可。Maven中的配置如下：

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.3.0.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

下面是log4j.properties的样例，用于打印日志到控制台：

```
log4j.rootCategory=INFO, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %t %c{2}:%L - %m%n

log4j.category.org.springframework.beans.factory=DEBUG
```

##### 带有本地JCL的运行时容器 {#带有本地jcl的运行时容器}

许多人在一个容器中运行Spring应用程序，而这个容器本身又提供了JCL的实现。IBM的Websphere Application Server（WAS）是一个原型。这经常引起一些问题，而且不幸的是没有很好的解决方案，简单地从应用中排除掉**commons-logging**在大部分情况下还不够。

更清楚地描述：这个问题通常并不与JCL本身有关，甚至是**commons-logging**，而是他们绑定了**commons-logging**到另一个框架（通常是Log4J）。这会失败是因为**commons-logging**改变了在旧版本（1.0）和新版本（1.1）中执行运行时发现算法的方式，其中，旧版本在一些容器中还在使用，新版本是现在大部分人使用的。Spring没有使用JCL API的其它部分，所以不会有什么问题，但是一旦Spring或你的应用试图记录日志就会发现Log4J不能工作了。（译者注：此处的意思是即使发生了上面的冲突，Spring也不会去检查，直接运行的时候需要打印日志的时候才会出错）

在WAS这个案例中，最简单的方法就是倒置类加载器的继承（IBM称作“parent last”，即把父类放后面），以便应用程序而不是容器控制JCL依赖。这种选择并不总是管用的，在公共领域有很多其它建议的替代方案，且你的里程可能会随着确切的版本和容器的特性而改变。（译者注：此处的意思是上面介绍的方法并不是唯一的，需要根据不同的版本和容器作出相应的方案）

---

# 二、Spring 4.x中的新特性 {#二spring-4x中的新特性}

## 3. Spring 4.0的新特性和增强功能 {#3-spring-40的新特性和增强功能}

Spring最初发行于2004年，从那以后有过几次重大的修改，Spring 2.0提供了XML命名空间和AspectJ，Spring 2.5包含了注解驱动的配置，Spring 3.0以Java 5+为框架的代码基础，并使用其新特性，诸如以**@Configuration**注解的模型等。

4.0版本是最近一次重大的修改，且首次全面支持Java 8的新特性。你仍然可以继续使用Java的旧版本，但是最低要求提升到了Java SE 6。我们也利用这次重大修改移除了很多过时的类和方法。

升级到Spring 4.0的指导手册Spring Framework GigHub Wiki参见。

### 3.1 改进了入门体验 {#31-改进了入门体验}

新的spring.io入门指南网址提供了完整的1. Spring入门帮你学习Spring。更多的指南请参考本文档的。新网址也提供了对发布在Spring下的许多项目的深入理解。

如果你是Maven用户，你可能会对现在发布在每个Spring版本中的物料清单POM文件感兴趣。

### 3.2 移除了过时的包和方法 {#32-移除了过时的包和方法}

4.0版本移除了所有过时的包以及许多过时的类和方法。如果从之前的版本升级过来，则需要保证修复所有对过时API的调用。

完整的改变请参考API Differences Report。

注意，可选的第三方依赖已经升级到2010/2011的版本（也就是说，Spring 4只支持发布在2010年之后的版本），尤其是，Hibernate 3.6+，EhCache 2.1+，Quartz 1.8+，Groovy 1.8+，Joda-Time 2.0+。有一个例外，Spring 4需要Hibernate Validator 4.3+和Jackson2.0+（Spring 3.2保留了对Jackson1.8/1.9的支持，但现在过时了）。

### 3.3 Java 8（以及6和7） {#33-java-8以及6和7}

Spring 4.0对Java 8的几个新特性提供了支持，允许使用lambda表达式，在Spring回调接口中使用方法引用。对**java.time**（JSR-310）有很好地支持，把几个已存在的注解改造为**@Repeatable**，还可以使用java 8的参数名称发现作为替代方案来编译启用了调试信息的代码（基于**-parameters**的编译器标志，译者注：参数名称发现是通过反射获取参数的名称，而不是类型）。

Spring保留了对旧版本Java和JDK的兼容，具体地说是Java SE 6和更高版本都全面支持（最低JDK6.18，发布于2010年1月）。尽管如此，我们依然建议基于Spring 4的新项目使用Java 7或者8。

### 3.4 Java EE 6和7 {#34-java-ee-6和7}

Java EE 6+及其相关的JPA 2.0和Servlet 3.0，被认为是Spring 4的基线。为了兼容Google App Engine和旧的应用服务器，可能要在Servlet 2.5环境中部署Spring 4。然而，Servlet 3.0+是我们强烈推荐的，并且它也是Spring测试的先决条件，也是模拟软件包测试开发环境设置的先决条件。

```
如果你是WebSphere 7用户，请一定要安装JPA 2.0包，如果是WebLogic 10.3.4或更高版本，还要安装JPA 2.0补丁，这样Spring 4才能兼容这两个服务器。
```

更有远见的主意，Spring 4.0现在支持Java EE 7适用的规范，尤其是JMS 2.0、JTA 1.2、JPA 2.1、Bean Validation 1.1和JSR-236 Concurrency Utilities。像往常一样，这种支持只针对个人的使用，比如在Tomcat或独立的环境中。尽管如此，当Spring应用部署在Java EE 7的服务器上依然运行良好。

注意，Hibernate 4.3是JPA 2.1的提供者，因此只在Spring 4.0中支持。同样地，Hibernate Validator 5.0是Bean Validation 1.1的提供者。因此，这两项并不被Spring 3.2官方支持。

### 3.5 Groovy Bean定义DSL {#35-groovy-bean定义dsl}

从Spring 4.0开始，可以使用Groovy DSL定义外部bean了。在概念上，这与使用XML配置bean类似，但是可以使用更简洁的语法。使用Groovy还可以很容易地把bean定义直接嵌入到引导代码中。例如：

```
def reader = new GroovyBeanDefinitionReader(myApplicationContext)
reader.beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}
```

更多信息请查阅**GroovyBeanDefinitionReader**的javadocs。

### 3.6 核心容器的改进 {#36-核心容器的改进}

核心容器有以下几点改进：

* Spring注入Bean时把泛型当作一种限定符。例如，使用Spring的Repository时，可以注入特定的实现： 
* @Autowired Repository&lt;Customer&gt; customerRepository。
* 使用Spring的元注解，可以开发暴露特定属性的自定义注解。
* Bean可以在被装配到list或数组中时排好序。通过@Order注解和Ordered接口支持。
* @Lazy注解可以用于注入点，也可用于@Bean定义上。
* 引入了@Description注解以便开发者使用基于Java的配置。
* 通过@Conditional注解可以定义有条件过滤的bean。这与@Profile类似但允许用户自定义开发策略。
* 基于CGLIB的代理类不再需要默认的构造方法。通过objenesis库进行支持，它被重新打包到Spring中并作为Spring框架的一部分发布。使用这种策略，生成代理实例时没有构造方法将被调用。
* 添加了管理时区的支持。例如LocaleContext。

### 3.7 Web的改进

保留了Servlet 2.5服务器的部署，但Spring 4.0现在主要关注Servlet 3.0+环境的部署。如果使用Spring MVC测试框架，需要保证在test classpath上包含Servlet 3.0的兼容JAR包。

除了下面要讲的WebSocket方面的支持，在Spring的Web模块还包含以下几点改进：

* 可以添加新的@RestController注解到Spring MVC应用上，而不用再添加@ResponseBody到每个@RequestMapping方法上。
* 添加了AsyncRestTemplate类，当开发REST客户端时允许非阻塞异步支持。
* 当开发Spring MVC应用时提供了全面的时区支持。

### 3.8 WebSocket、SockJS 和STOMP Messaging {#38-websocketsockjs-和stomp-messaging}

新的**spring-websocket**模块全面支持在web应用中客户端与服务端基于WebSocket双向通信。它兼容[JSR-356](http://jcp.org/en/jsr/detail?id=356)、Java WebSocket API，另外还提供了基于SockJS的后退选项（例如，WebSocket仿真）用于不支持WebSocket协议的浏览器（例如，IE &lt; 10）。

新的**spring-messaging**模块支持STOMP作为WebSocket的子协议与一个注解程序模型一起用于路由并处理来自WebSocket客户端的STOMP消息。因此，一个**@Controller**可以同时包含**@RequestMapping**和**@MessageMapping**方法用于处理HTTP请求和来自WebSocket客户端的消息。新的**spring-messaging**模块还包含从以前Spring集成项目提取出来的关键抽象作为基于消息处理的应用的基础，如**Message**、**MessageChannel**、**MesaageHandler**等。

### 3.9 测试的改进

除了移除了spring-test模块过时的代码，Spring 4.0还引入了几个新特性用于单元测试和集成测试：

* 几乎spring-test模块的所有注解（例如，@ContextConfiguration、@WebAppConfiguration、@ContextHierarchy、@ActiveProfiles等）都可以作为元注解用于创建自定义注解并减少测试套件中的重复配置。
* 有效的bean定义配置文件可以通过编程解析，只要简单地实现自定义的ActiveProfilesResolver并注册@ActiveProfiles的resolver属性即可。
* spring-core模块引入了新的SocketUtils类，用于扫描本地空闲的TCP和UDP服务端口。这项功能并不特定用于测试，但是当写需要socket的集成测试时非常有用，例如，启动内存中的SMTP服务器、FTP服务器、Servlet容器等的测试。
* 自Spring 4.0起，org.springframework.mock.web包中模拟集合以Servlet 3.0为基础。此外，一些Servlet API模拟（例如，MockHttpServletRequest，MockServletContext等）有少许增强并可通过配置改进。

## 4. Spring 4.1的新特性和增强功能 {#4-spring-41的新特性和增强功能}

### 4.1 JMS的改进 {#41-jms的改进}

Spring 4.1引入了一个更简单的方法来注册JMS监听器，那就是使用**@JmsListener**注解bean的方法。XML的命名空间也得到了增强以支持这项新特性（**jms:annotation-driven**），也可以通过Java配置来完全使用这项新特性（**@EnableJms**，**JmsListenerContainerFactory**），还可以使用**JmsListenerConfigurer**来编程式地注册监听器。

Spring 4.1还可以与4.0中引入的**spring-messaging**合作使用

* 消息监听器可以拥有更弹性的签名，并且可以受益于标准的消息处理注解，比如，@Payload, @Header, @Headers, @SendTo，等等，也可以使用标准的Message代替javax.jms.Message作为方法的参数。
* 新的JmsMessageOperation接口可以被使用，并且允许JmsTemplate像使用Message一样操作。

最后，Spring 4.1还提供了以下各种各样的改进：

* JmsTemplate支持同步的请求应答操作。
* 每个&lt;jms:listener&gt;元素可以指定监听器的优先级。
* 通过BackOff实现可以配置消息监听容器的恢复选项。
* JMS 2.0支持共享消费者。

### 4.2 缓存的改进 {#42-缓存的改进}

Spring 4.1支持JCache（JSR-107）注解，直接使用Spring已存在的缓存配置和基础架构即可，不需要其它的改变。

Spring 4.1也极大地改进了它的缓存策略：

* 可以在运行时使用CacheResolver解析缓存。因此，不再强制使用value参数来定义缓存的名称。
* 更多自定义的操作：缓存解析，缓存管理，键生成器。
* 新的@CacheConfig注解允许通用设置在类级别共享，而不需要启用任何缓存操作。
* 使用CacheErrorHandler更好地处理缓存的异常。

Spring 4.1还为了添加putIfAbsent方法对CacheInterface做了重大改变。

### 4.3 Web的改进 {#43-web的改进}

* 新的抽象ResourceResolver, ResourceTransformer和ResourceUrlProvider扩展了已存在的基于ResourceHttpRequestHandler的资源处理程序。一些内置的实现提供了对带版本的资源URL（为了有效的HTTP缓存）、定位gzip资源、生成HTML 5 AppCache清单等的支持。参考21.16.9 资源服务。
* JDK 1.8的java.util.Optional现在支持@RequestParam, @RequestHeader和@MatrixVariable控制器方法的参数。
* ListenableFuture作为返回值替代了DeferredResult，在这方面一项基础服务（或者说对AsyncRestTemplate的调用）已经返回了ListenableFuture。
* @ModelAttribute方法现在按照依赖间的顺序依次被调用。
* Jackson的@JsonView直接作用于@ResponseBody和ResponseEntity控制器方法，用于序列化同一个POJO的不同形式（比如，汇总和详情）。这可以通过为模型属性添加指定key的序列化视图类型来渲染视图。参考Jackson序列化视图支持。
* Jackson现在支持JSONP。参考Jackson JSONP支持。
* 新的生命周期选项可用于在控制器方法返回后且响应写出前拦截@ResponseBody和ResponseEntity方法，声明一个@ControllerAdvice bean实现ResponseBodyAdvice即可，内置的@JsonView和JSONP恰恰利用了这点。参考21.4.1 使用HandlerInterceptor拦截请求。
* 有三个HttpMessageConverter选项： 
* Gson——比Jackson更轻的足迹，已用于Spring Android中。
* Google协议缓冲——企业内部有效的服务间通信数据协议，但是也可以作为JSON和XML暴露于浏览器中。
* 通过jackson-dataformat-xml扩展支持基于XML的Jackson。当使用@EnableWebMvc或&lt;mvc:annotation-driven&gt;时，如果classpath下存在jackson-dataformat-xml则默认会替代JAXB2。
* 类似JSP的视图现在可以通过引用控制器映射的名称与控制器建立链接。默认的名称将被赋给每一个@RequestMapping。例如，FooController拥有方法handleFoo，它的名称为“FC\#handleFoo”。命名策略是可插拔的，也可以通过name属性为@RequestMapping明确地命名。在Spring JSP标签库中新的mvcUrl功能可以让使用JSP页面变得更方便。参考21.7.2 从视图为Controller及其方法创建URI。
* ResponseEntity提供了创建者风格的API用于引导控制器方法为服务端响应做准备。例如，ResponseEntity.ok\(\)。
* RequestEntity是一种新类型，它提供了创建者风格的API用于引导客户端REST代码为HTTP请求做准备。

* MVC Java配置与XML命名空间：

  * bean中的任何公共方法都能够通过@EventListener注解来消费事件。

  * @TransactionalEventListener提供了事务绑定的事件支持。

* Spring 4.2提供了一流的支持用于声明和查找注解属性的别名。新的@AliasFor注解可以用来在单个注解内声明一对别名属性，或者声明一个从自定义注解属性到元注解属性的别名。

  * 以下注解都通过@AliasFor翻新过了，以便为value属性提供更有意义的别名：@Cacheable, @CacheEvict, @CachePut, @ComponentScan, @ComponentScan.Filter, @ImportResource, @Scope, @ManagedResource, @Header, @Payload, @SendToUser, @ActiveProfiles, @ContextConfiguration, @Sql, @TestExecutionListeners, @TestPropertySource, @Transactional, @ControllerAdvice, @CookieValue, @CrossOrigin, @MatrixVariable, @RequestHeader, @RequestMapping, @RequestParam, @RequestPart, @ResponseStatus, @SessionAttributes, @ActionMapping, @RenderMapping, @EventListener, @TransactionalEventListener。

  * 例如，来自spring-test模块的@ContextConfiguration现在定义如下：

  * ```
    public @interface ContextConfiguration {

    @AliasFor("locations")
    String[] value() default {};

    @AliasFor("value")
    String[] locations() default {};

    // ...
    }
    ```
  * 类似地，重写了元注解属性的注解现在也可以使用@AliasFor细粒度地控制那些在注解层次结构中被重写的属性。实际上，现在可以为元注解的value属性声明一个别名。

  * 例如，现在可以像下面一样开发一种重写了自定义属性的组合注解。

  * ```
    @ContextConfiguration
    public @interface MyTestConfig {

    @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
    String[] xmlFiles();

    // ...
    }
    ```
  * 参考Spring注解编程模型。

* Spring在发现元注解的搜索算法上做了很多改进。例如，在注解继承体系中可以声明局部的组合注解。

* 重写了元注解属性的组合注解现在可以用在接口、抽象类、桥接和接口方法上，也可以用在类、标准方法、构造方法和字段上。

* 代表注解属性的Map（和AnnotationsAttributes实例）可以被合成（或者转换）到一个注解中。

* 基于字段的数据绑定（DirectFieldAccessor）可以与当前基于属性的数据绑定（BeanWrapper）一起使用。特别地，基于字段的绑定现在支持为集合、数据和Map导航。

* DefaultConversionService为Steam、Charset、Currency和TimeZone提供了可以直接使用的转换器。这些转换器也可以被添加到任意的ConversionService中。
* DefaultFormattingConversionService为JSR-354中的货币提供了支持（如果javax.money存在于classpath下），即MonetaryAmount和CurrencyUnit。这也包含对@NumberFormat的支持。
* @NumberFormat现在可以作为元注解使用。
* JavaMailSenderImpl有一个新的方法testConnection\(\)用于检查与服务器间的连接。
* ScheduledTaskRegistrar暴露计划的任务。
* Apache的commons-pool2现在支持AOP池CommonsPool2TargetSource。
* 为脚本化bean引入了StandardScriptFactory作为一个基于JSR-223的机制，暴露于XML中的lang:std元素。对JavaScript和JRuby的支持。（注意：JRubyScriptFactory和lang:jruby现在过时了，请使用JSR-223）

### 5.2 数据访问的改进 {#52-数据访问的改进}

* AspectJ现在支持javax.transactional.Transactional。
* SimpleJdbcCallOperations现在支持命名绑定。
* 全面支持Hibernate ORM 5.0，作为JPA提供者（自动适配），也支持其原生API（被新的org.springframework.orm.hibernate5包覆盖）。
* 嵌入的数据库现在可以被自动赋值不同的（unique）名字，且&lt;jdbc:embedded-database&gt;支持新的属性database-name。参考下面的“测试的改进”部分。

### 5.3 JMS的改进 {#53-jms的改进}

* autoStartup属性可以通过JmsListenerContainerFactory控制。
* 每个监听器容器都能配置应答Destination的类型。
* @SendTo注解的值现在可以使用SpEL表达式。
* 响应目标可以使用JmsResponse在运行时计算。
* @JmsListener是一个可重复性的注解，可以在同一个方法上声明多个JMS容器（如果你还没有使用Java 8，请使用新引入的@JmsListeners）。

### 5.4 Web的改进 {#54-web的改进}

* 支持HTTP流和服务器发送事件。参考HTTP流。
* 支持内置CORS的全局（MVC Java配置和XML命名空间）和局部（例如，@CrossOrign）配置。参考26 CORS支持。
* HTTP缓存更新： 
  * 新的创建者CacheControl，嵌入到ResponseEntity, WebContentGenerator, ResourceHttpRequestHandler中。
  * 在WebRequest中改进了ETag/Last-Modified的支持。
* 自定义映射注解，使用@RequestMapping作为元注解。
* AbstractHandlerMethodMapping中的公共方法用于在运行时注册和取消注册请求映射。
* AbstractDispatcherServletInitializer中的保护方法createDispatcherServlet进一步自定义DispatcherServlet的实例。
* HandlerMethod作为@ExceptionHandler方法的参数，特别在@ControllerAdvice组件中非常便利。
* java.util.concurrent.CompletableFuture作为@Controller方法的返回类型。
* HttpHeaders支持字节范围的请求，并提供静态资源。
* @ResponseStatus检测嵌套异常。
* RestTemplate中的UriTemplateHandler扩展点。 
  * DefaultUriTemplateHandler暴露了baseUrl属性和路径段编码选项。
  * 此扩展点可嵌入到URI模板库中。
* OkHTTP与RestTemplate集成。
* 自定义的baseUrl可以替代MvcUriComponentsBuilder中的方法。
* 序列化/反序列化的异常信息在WARN级别被记录。
* 默认的JSON前缀从“{}&&”改成了更安全的”\)\]}’,”中的一个（译者注：此处可能官方文档有误）。
* 新的扩展点RequestBodyAdvice和内置实现支持@RequestBody方法参数上的Jackson的@JsonView。
* 使用GSON或Jackson 2.6+时，处理器方法的返回类型被用于改进参数化类型的序列化，比如List&lt;Foo&gt;。
* 引入了ScriptTemplateView作为JSR-223用于处理脚本web视图的机制，主要关注于Nashorn（JDK 8）上的JavaScript视图模板。

### 5.5 WebSocket消息处理的改进 {#55-websocket消息处理的改进}

* 暴露关于已连接用户和订阅存在的信息。 
  * 新的SimpUserRegistry暴露为叫作“userRegistry”的bean。
  * 在服务器集群间共享已存在的信息（参考代理中继配置选项）。
* 解决用户在服务器集群中的目的地（参考代理中继配置选项）。
* StompSubProtocolErrorHandler扩展点用来定制和控制STOMP错误帧到客户端。
* 通过@ControllerAdvice组件声明的全局方法@MessageExceptionHandler。
* SpEL表达式“selector”头用于SimpleBrokerMessageHandler的订阅。
* 通过TCP和WebSocket使用STOMP客户端。参考25.4.13 STOMP客户端。
* @SendTo和@SendToUser可以包含多个占位符。
* Jackson的@JsonView支持在@MessageMapping和@SubscribeMapping方法上返回值。
* ListenableFuture和CompletableFuture可以作为@MessageMapping和@SubscribeMapping方法的返回值类型。
* MarshallingMessageConverter用于XML负载。

### 5.6 测试的改进 {#56-测试的改进}

* 基于JUnit的集成测试现在可以使用JUnit规则执行而不是SpringJUnit4ClassRunner。这使得基于Spring的集成测试可以使用替代runner运行，比如JUnit的Parameterized或第三方的runner如MockitoJUnitRunner。参考Spring JUnit规则。
* Spring MVC测试框架现在对HtmlUnit提供了一流的支持，包括集成Selenium的WebDriver，允许基于页面的web应用测试不再需要部署到一个Servlet容器上。参考14.6.2, HtmlUnit的集成。
* AopTestUtils是一个新的测试工具类，它允许开发者可以获取到底层的隐藏在一个或多个Spring代理类下的目标对象。参考13.2.1 通用测试工具类。
* ReflectionTestUtils现在支持为static字段设值和取值，包括常量。
* 通过@ActiveProfiles声明的bean定义配置文件的原始顺序现在保留了，这是为了使用一些案例，比如Spring Boot的ConfigFileApplicationListener，它通过有效的名称来加载配置文件。
* @DirtiesContext现在支持新的模式BEFORE\_METHOD, BEFORE\_CLASS和BEFORE\_EACH\_TEST\_METHOD用于在测试之前关闭ApplicationContext——例如，在大型测试套件中的一些劣质的测试毁坏了对ApplicationContext的原始配置。
* @Commit这个新注解可以直接替代@Rollback\(false\)。
* @Rollback现在可以用来配置类级别默认的回滚语义。 
  * 因此，@TransactionConfiguration现在过时了，并且会在后续版本中移除。
* 通过statements这个新的属性@Sql现在支持内联SQL语句的执行。
* 用于在测试期间缓存应用上下文的ContextCache现在是公共的API，它有默认的实现，可以替代自定义的缓存需求。
* DefaultTestContext, DefaultBootstrapContext和DefaultCacheAwareContextLoaderDelegate现在是support子包下的公共类，允许自定义扩展。
* TestContextBootstrappers现在负责创建TestContext。
* 在Spring MVC测试框架中，MvcResult的详细日志现在可以在DEBUG级别被打印，或者写出到自定义的OutputStream或Writer中。参考MockMvcResultHanlder中的新方法log\(\), print\(OutputStream\)和print\(Writer\)。
* JDBC XML的命名空间支持一个新的属性database-name，位于&lt;jdbc:embedded-database&gt;中，允许开发者为嵌入的数据库设置不同的名字——例如，通过SpEl表达式或者被当前 有效bean定义 配置文件 影响的属性文件占位符。
* 嵌入的数据库现在可以被自动赋予不同的名字，允许在同一测试套件不同的应用上下文中重复使用通用的测试数据库配置。参考18.8.6 为嵌入的数据库生成不同的名字。
* MockHttpServletRequest和MockHttpServletResponse现在通过getDateHeader和setDateHeader方法提供了更好的支持用于格式化日期头。

## 6. Spring 4.3的新特性和增强功能 {#6-spring-43的新特性和增强功能}

### 6.1 核心容器的改进 {#61-核心容器的改进}

* 核心容器提供了更丰富的元数据用于编程式评估。
* Java8的默认方法可以作为bean属性的getter/setter方法被检测。
* 如果目标bean仅仅定义了一个构造方法，就不必指定@Autowired注解了。
* @Configuration类支持构造方法注入。
* 任何用于指定@EventLIstener条件的SpEL表达式现在可以引用bean了（例如，@beanName.method\(\)）。
* 组合注解现在可以重写元注解的数组属性。例如，@RequestMapping的String\[\] path可以使用组合注解的String path重写。
* @Scheduled和@Schedules可以作为元注解，用来创造组合注解并可重写其属性。
* @Scheduled支持任何作用域的bean。

### 6.2 数据访问的改进 {#62-数据访问的改进}

jdbc:initialize-database和jdbc:embedded-database支持一个可配置的分隔符应用于任何脚本。

### 6.3 缓存的改进 {#63-缓存的改进}

spring 4.3 允许并发调用给定的key，从而使得值只被计算一次。这是一项可选功能，通过**@Cacheable**的新属性**sync**启用。这项功能也使**Cache**接口做了重大改变，增加了**get\(Object key, Callable&lt;T&gt; valueLoader\)**方法。

spring 4.3 也改进了以下缓存方面的内容：

* 缓存相关的注解中的SpEL表达式现在可以引用bean了（比如，@beanName.method\(\)）。
* ConcurrentMapCacheManager和ConcurrentMapCache现在可以通过新的属性storeByValue序列化缓存的entry。
* @Cacheable, @CacheEvict, @CachePut和@Caching现在可以作为元注解，用来创造组合注解并可重写其属性。

### 6.4 JMS的改进 {#64-jms的改进}

* @SendTo现在可应用于类级别上，以便共享共同的目标。
* @JmsListener和@JmsListeners现在可作为元注解，用来创造组合注解并可重写其属性。

### 6.5 Web的改进 {#65-web的改进}

* 内置了对Http头和Http选项的支持。
* 新的组合注解@GetMapping, @PostMapping, @PutMapping, @DeleteMapping和@PatchMapping，它们来源于@RequestMapping。 
* 参考@RequestMapping的变种。
* 新的组合注解@RequestScope, @SessionScope和@ApplicationScope用于web作用域。 
* 参考Request scope, Session scope和Application scope。
* 新的注解@RestControllerAdvice，它是@ControllerAdvice和@ResponseBody的组合体。
* @ResponseStatus现在可用于类级别并可以被所有方法继承。
* 新的@SessionAttribute注解用于访问session的属性。
* 新的@RequestAttribute注解用于访问request的属性。
* @ModelAttribute可以设置其属性binding=false阻止数据绑定。
* 错误和自定义的异常可一致地暴露给MVC的异常处理器。
* Http消息转换器中一致地处理字符集，默认地使用UTF-8处理多部分文本内容。
* 使用已配置的ContentNegotiationManager处理媒体类型等静态资源。
* RestTemplate和AsyncRestTemplate可通过DefaultUriTemplateHandler支持严格的URI编码。
* AsyncRestTemplate支持请求拦截。



### 6.6 WebSocket消息处理的改进 {#66-websocket消息处理的改进}

* **@SendTo**和**@SendToUser**现在可应用于类级别上，以便共享共同的目标。

### 6.7 测试的改进 {#67-测试的改进}

* spring测试上下文中的JUnit现在需要 4.12 及其更高版本。
* SpringJUnit4ClassRunner的新别名SpringRunner。
* 测试相关的注解现在可用于接口上，从而可以使用Java 8 中接口的默认方法。
* 空声明的@ContextConfiguration现在可以完全省略了，如果默认的XML文件、Groovy脚本或@Configuration类被检测到。
* @Transactional测试方法不再必需是public了（例如，在TestNG和JUnit 5 中）。
* @BeforeTransaction和AfterTransaction方法不再必需是public了，并且现在也可能用在Java 8 接口的默认方法上。
* spring测试上下文中的ApplicationContext缓存现在是有界的，默认最大值为32，并按最近最少原则回收。其最大值可以通过JVM的系统属性或spring的属性spring.test.context.cache.maxSize进行设置。
* 用于自定义测试ApplicationContext的新API ContextCustomizer在bean定义之后且上下文刷新之前被加载到上下文中。Customizer可以通过第三方注册，但需要实现自定义的ContextLoader。
* @Sql和@SqlGroup现在可作为元注解，用来创造组合注解并可重写其属性。
* ReflectionTestUtils现在会自动解除代理当set或get一个字段时。
* 服务器端的springmvc测试支持响应头带有多个值。
* 服务器端的springmvc测试解析表单数据请求内容并填充请求参数。
* 服务器端的springmvc测试支持对已调用的处理器方法模拟断言。
* 客户端的REST测试允许指明希望发送多少次请求并决定是否请求的顺序可被忽略。
* 客户端的REST测试支持在请求体中添加表单数据。

### 6.8 支持新库和服务器 {#68-支持新库和服务器}

* Hibernate ORM 5.2（仍然能很好地支持4.2/4.3和5.0/5.1，但是3.6已经过时了）

* Jackson 2.8（至少需要2.6以上版本）
* OkHttp 3.x（同时仍然支持OkHttp 2.x）
* Netty 4.1
* Undertow 1.4
* Tomcat 8.5.2 及 9.0 M6

另外，spring 4.3的spring-core.jar中集成了更新的ASM 5.1和Objenesis 2.4。



