**我们经常会遇到这样一种情景，就是在我们开发项目的时候经常会在一个类中调用其他的类中的方法，来完成我们期望的任务，大部分的情况下往往会采用在当前需要的这个类里面new一个实例出来，然后调用他的方法，那么这样的话会有个问题，就是有一天我想改变下这个类，改为其他的名称，那么这时候必须要做的是同时去调用方的类文件中改变这个改变的类的名称。这样的情况是因为代码的耦合带来了后期维护成本的增加，那么**[**spring**](http://lib.csdn.net/base/javaee)**的出现就可以很好的起到解耦的作用，而他的核心机制就是依赖注入。**

  


  


# **依赖注入与控制反转**

**  
**

**依赖注入：对于spring而言，将自己置身于spring的立场上去看，当调用方需要某一个类的时候我就为你提供这个类的实例，就是说spring负责将被依赖的这个对象赋值给调用方，那么就相当于我为调用方注入了这样的一个实例。从这方面来看是依赖注入。**

**  
**

**控制反转：对于调用方来说，通常情况下是我主动的去创建的，也就是对于这个对象而言我是控制方，我有他产生与否的权力，但是，现在变了，现在变为spring来创建对象的实例，而我被动的接受，从这一点上看，是控制反转。**

**  
**

**这两者的意思是一致的，就看你从谁的角度去看这个问题。不同的角度那么看到的问题可能是不一样的。**

**  
**

**  
**

# **依赖注入两种方式**

**  
**

## **1.设值注入**

**  
**

**设值注入:通过set的方式注入值.Ioc容器通过成员变量的setter方法来注入被依赖的对象，这种注入方式简单，直观，因而在spring中大量的使用。**

**下面我们采用实际的例子来体会一下：**

**假设这样的一个场景，我想打印消息，这样一件事情**

**首先定义一个MessageService的接口。**

```
package com.sx.spring20170328;

/**
 * Created by sx on 17/3/28.
 */
public interface MessageService {
    //消息打印
    void printMessage();
}

```

然后实现这个接口，并实现这个方法。

```
package com.sx.spring20170328;

/**
 * Created by sx on 17/3/28.
 */
public class MessagePrinter implements MessageService{
    @Override
    public void printMessage() {
        System.out.println("输出消息!");
    }
}
```

那么对于我而言，我也定义一个person的接口

```
package com.sx.spring20170328;

/**
 * Created by sx on 17/3/28.
 */
public interface Person {
    void sendMessage();
}

```

我来实现人这个接口

```
package com.sx.spring20170328;

/**
 * Created by sx on 17/3/28.
 */
public class WangYang implements Person {
    private MessageService service;

    public void setService(MessageService service){
        this.service = service;
    }

    @Override
    public void sendMessage() {
        this.service.printMessage();
    }
}
```

Spring的配置文件：





**\[java\]**

[view plain](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[copy](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[![](https://code.csdn.net/assets/CODE_ico.png "在CODE上查看代码片")](https://code.csdn.net/snippets/1591181)

[![](https://code.csdn.net/assets/ico_fork.svg "派生到我的代码片")](https://code.csdn.net/snippets/1591181/fork)

1. &lt;
   ?xml version=
   "1.0"
    encoding=
   "UTF-8"
   ?
   &gt;
2. &lt;
   beans xmlns=
   "http://www.springframework.org/schema/beans"
3.        xmlns:xsi=
   "http://www.w3.org/2001/XMLSchema-instance"
4.        xsi:schemaLocation="  
5. http:
   //www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
   &gt;
6. 
7. &lt;
   !-- bean definitions here --
   &gt;
8. &lt;
   bean id = 
   "messageService"
   class
    = 
   "com.siti.spring20160227.MessagePrinter"
   &gt;
   &lt;
   /bean
   &gt;
9. &lt;
   bean id = 
   "wy"
   class
    = 
   "com.siti.spring20160227.WangYang"
   &gt;
10. &lt;
    property name=
    "service"
     ref=
    "messageService"
    &gt;
    &lt;
    /property
    &gt;
11. &lt;
    /bean
    &gt;
12. &lt;
    /beans
    &gt;

  


测试类如下:





**\[java\]**

[view plain](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[copy](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[![](https://code.csdn.net/assets/CODE_ico.png "在CODE上查看代码片")](https://code.csdn.net/snippets/1591181)

[![](https://code.csdn.net/assets/ico_fork.svg "派生到我的代码片")](https://code.csdn.net/snippets/1591181/fork)

1. package
    com.siti.spring20160227;  
2. 
3. import
    org.springframework.context.ApplicationContext;  
4. import
    org.springframework.context.support.ClassPathXmlApplicationContext;  
5. 
6. public
   class
    MainTest {  
7. 
8. public
   static
   void
    main\(String\[\] args\) {  
9.         ApplicationContext context = 
   new
    ClassPathXmlApplicationContext\(
   "applicationContext.xml"
   \);  
10.         Person person = context.getBean\(
    "wy"
    , Person.
    class
    \);  
11.         person.sendMessage\(\);  
12.     }  
13. }  



**  
**

## **2.构造注入**

**  
**

**通过构造函数的方式注入。spring以反射的方式执行带指定参数的构造器，当执行带参数的构造器时就可以通过构造器的参数赋值给成员变量，完成构造注入。**

**  
**

**那么现在需求变了，我需要改一些东西，下面可以注意下我主要改动了哪里：**

**在WangYang这个类中添加有参数和无参数的构造函数：**



**\[java\]**

[view plain](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[copy](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[![](https://code.csdn.net/assets/CODE_ico.png "在CODE上查看代码片")](https://code.csdn.net/snippets/1591181)

[![](https://code.csdn.net/assets/ico_fork.svg "派生到我的代码片")](https://code.csdn.net/snippets/1591181/fork)

1. package
    com.siti.spring20160227;  
2. 
3. public
   class
    WangYang 
   implements
    Person{  
4. 
5. private
    MessageService service;  
6. 
7. &lt;
   span style=
   "color:\#33ff33;"
   &gt;
   public
    WangYang\(\) {  
8. super
   \(\);  
9.     }  
10. 
11. public
     WangYang\(MessageService service\) {  
12. this
    .service = service;  
13.     }  
14. 
15. &lt;
    /span
    &gt;
    public
    void
     setService\(MessageService service\) {  
16. this
    .service = service;  
17.     }  
18. 
19. @Override
20. public
    void
     sendMessage\(\) {  
21. this
    .service.printMessage\(\);  
22.     }  
23. 
24. }  

  


在Spring配置文件中，稍微改动，即将原来的设值注入换为构造注入即可。





**\[java\]**

[view plain](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[copy](http://blog.csdn.net/wangyang1354/article/details/50757098#)

[![](https://code.csdn.net/assets/CODE_ico.png "在CODE上查看代码片")](https://code.csdn.net/snippets/1591181)

[![](https://code.csdn.net/assets/ico_fork.svg "派生到我的代码片")](https://code.csdn.net/snippets/1591181/fork)

1. &lt;
   ?xml version=
   "1.0"
    encoding=
   "UTF-8"
   ?
   &gt;
2. &lt;
   beans xmlns=
   "http://www.springframework.org/schema/beans"
3.        xmlns:xsi=
   "http://www.w3.org/2001/XMLSchema-instance"
4.        xsi:schemaLocation="  
5. http:
   //www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
   &gt;
6. 
7. &lt;
   !-- bean definitions here --
   &gt;
8. &lt;
   bean id = 
   "messageService"
   class
    = 
   "com.siti.spring20160227.MessagePrinter"
   &gt;
   &lt;
   /bean
   &gt;
9. &lt;
   bean id = 
   "wy"
   class
    = 
   "com.siti.spring20160227.WangYang"
   &gt;
10. &lt;
    !-- 
    &lt;
    property name=
    "service"
     ref=
    "messageService"
    &gt;
    &lt;
    /property
    &gt;
     --
    &gt;
11. &lt;
    span style=
    "color:\#33ff33;"
    &gt;
    &lt;
    constructor-arg ref=
    "messageService"
    &gt;
    &lt;
    /constructor-arg
    &gt;
    &lt;
    /span
    &gt;
12. &lt;
    /bean
    &gt;
13. &lt;
    /beans
    &gt;



**  
**

这样再次运行MainTest类，程序正常运行。所以从这里也可以体会到，spring这种解耦的方便性和重要性。

**  
**

**  
**

# **设值注入和构造注入的对比**

**  
**

**这两种方式，效果是一样的，注入的时机不同，设值注入是先调用无参的构造函数，创建出实例后然后调用set方法注入属性值。而构造输入是通过在调用构造函数初始化实例的同时完成了注入。  
  
**

**  
**

## **设值注入的优点**

**  
**

**1. 通过set的方式设定依赖关系显得更加直观，自然，和javabean写法类似。**

**2. 复杂的依赖关系，采用构造注入会造成构造器过于臃肿，spring 实例化的时候同时实例化其依赖的全部实例，导致性能下降，set方式可以避免这些问题。**

**3. 在成员变量可选的情况下，构造注入不够灵活。**

**  
**

## **构造注入的优点**

**  
**

**某些特定的情况下，构造注入比设值注入好一些。**

**1. 构造注入可以在构造器中决定依赖关系的注入顺序，优先依赖的优先注入，构造注入可以清楚的分清注入的顺序。**

**2. 组件的调用者无需知道组件内部的依赖关系，符合高内聚原则。**

