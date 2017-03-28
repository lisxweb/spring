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

**2.构造注入**

**        
**

**通过构造函数的方式注入。spring以反射的方式执行带指定参数的构造器，当执行带参数的构造器时就可以通过构造器的参数赋值给成员变量，完成构造注入。**

**        
**

**那么现在需求变了，我需要改一些东西，下面可以注意下我主要改动了哪里：**

**复制WangYang这个类改成LiSi添加有参数和无参数的构造函数：**

```
package com.sx.spring20170328;

/**
 * Created by lisx on 17/3/28.
 */
public class LiSi implements Person {
    private MessageService service;

    public LiSi(MessageService service) {
        this.service = service;
    }

    @Override
    public void sendMessage() {
        this.service.printMessage();
    }
}
```

Spring的配置文件：

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="messageService" class="com.sx.spring20170328.MessagePrinter"></bean>
    <bean id="wy" class="com.sx.spring20170328.WangYang">
        <property name="service" ref="messageService"></property><!--set注入-->
    </bean>
    <bean id="ls" class="com.sx.spring20170328.LiSi">
        <constructor-arg ref="messageService"/><!--构造注入-->
    </bean>
</beans>
```

测试类如下:

```
package com.sx.spring20170328;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * Created by lisx on 17/3/28.
 */
public class MainTest {
    public static void main(String[] args){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Person person = context.getBean("wy",Person.class);
        person.sendMessage();
        person = context.getBean("ls",Person.class);
        person.sendMessage();
    }
}
```

程序正常运行。所以从这里也可以体会到，spring这种解耦的方便性和重要性。



Spring 注入集合

下面例子向您展示[spring](http://lib.csdn.net/base/javaee)如何注入值到集合类型\(List, Set, Map, and Properties\)。 支持4个主要的集合类型：

```
List – <list/>
Set – <set/>
Map – <map/>
Properties – <props/>
```

> 使用EL表达式注入集合：[http://www.yiibai.com/spring/spring-el-lists-maps-example.html](http://www.yiibai.com/spring/spring-el-lists-maps-example.html)

```
package com.sx.spring20170328;

/**
 * Created by lisx on 17/3/28.
 */
import java.util.List;
import java.util.Map;
import java.util.Properties;
import java.util.Set;

public class MyCollection {

    private List<Object> lists;
    private Set<Object> sets;
    private Map<Object, Object> maps;
    private Properties pros;

    public void setLists(List<Object> lists) {
        this.lists = lists;
    }

    public void setSets(Set<Object> sets) {
        this.sets = sets;
    }

    public void setMaps(Map<Object, Object> maps) {
        this.maps = maps;
    }

    public void setPros(Properties pros) {
        this.pros = pros;
    }

    @Override
    public String toString() {
        return "MyCollection [lists=" + lists + ", sets=" + sets + ", maps=" + maps + ", pros=" + pros + "]";
    }
}   
```

```
package com.sx.spring20170328;

/**
 * Created by lisx on 17/3/28.
 */
public class Person {

    private String name;
    private String address;
    private int age;

    public void setName(String name) {
        this.name = name;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", address=" + address + ", age=" + age + "]";
    }

    public void sendMessage() {
    }
}
```

bean 配置文件

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="MyCollectionBean" class="com.sx.spring20170328.MyCollection">
        <!--java.util.List-->
        <property name="lists" >
            <list>
                <value>1</value><!-- 第一个list数据 -->
                <ref bean="PersonBean"/><!-- 第二个list数据 -->
                <bean class="com.sx.spring20170328.Person"><!-- 第三个list数据 -->
                    <property name="name" value="list哈罗" />
                    <property name="address" value="list罗马" />
                    <property name="age" value="29" />
                </bean>
            </list>
        </property>

        <!-- java.util.Set -->
        <property name="sets">
            <set>
                <value>1</value>
                <ref bean="PersonBean" />
                <bean class="com.sx.spring20170328.Person">
                    <property name="name" value="set哈罗" />
                    <property name="address" value="set罗马" />
                    <property name="age" value="29" />
                </bean>
            </set>
        </property>

        <!-- java.util.Map -->
        <property name="maps">
            <map>
                <entry key="Key 1" value="1" />
                <entry key="Key 2" value-ref="PersonBean" />
                <entry key="Key 3">
                    <bean class="com.sx.spring20170328.Person">
                        <property name="name" value="map简单" />
                        <property name="address" value="map越南" />
                        <property name="age" value="30" />
                    </bean>
                </entry>
            </map>
        </property>

        <!-- java.util.Properties -->
        <property name="pros">
            <props>
                <prop key="admin">admin@peng.com</prop>
                <prop key="support">support@peng.com</prop>
            </props>
        </property>

    </bean>
    <bean id="PersonBean" class="com.sx.spring20170328.Person">
        <property name="name" value="哈罗" />
        <property name="address" value="罗马" />
        <property name="age" value="28" />
    </bean>
</beans>
```

```
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.peng.collection.MyCollection;

public class TestMyCollection {
      public static void main( String[] args )
        {
            ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
            MyCollection mycollection = (MyCollection)context.getBean("MyCollectionBean");
            System.out.println(mycollection);

        }
}
```

输出结果：

```
MyCollection [lists=[1, Person [name=哈罗, address=罗马, age=28], Person [name=list哈罗, address=list罗马, age=29]], sets=[1, Person [name=哈罗, address=罗马, age=28], Person [name=set哈罗, address=set罗马, age=29]], maps={Key 1=1, Key 2=Person [name=哈罗, address=罗马, age=28], Key 3=Person [name=map简单, address=map越南, age=30]}, pros={admin=admin@peng.com, support=support@peng.com}]
```

# **设值注入和构造注入的对比**

**        
**

\*\*这两种方式，效果是一样的，注入的时机不同，设值注入是先调用无参的构造函数，创建出实例后然后调用set方法注入属性值。而构造输入是通过在调用构造函数初始化实例的同时完成了注入。

\*\*

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

