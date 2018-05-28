[spring](http://lib.csdn.net/base/javaee)官方文档：<http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/>

# 一、Spring框架概述

Spring框架是一个轻量级的解决方案，可以一站式地构建企业级应用。Spring是模块化的，所以可以只使用其中需要的部分。可以在任何web框架上使用控制反转（IoC），也可以只使用[Hibernate集成代码](http://blog.csdn.net/tangtong1/article/details/51326887#hibernate)或[JDBC抽象层](http://blog.csdn.net/tangtong1/article/details/51326887#jdbc-introduction)。它支持声明式事务管理、通过RMI或web服务实现远程访问，并可以使用多种方式持久化数据。它提供了功能全面的[MVC框架](http://blog.csdn.net/tangtong1/article/details/51326887#mvc-introduction)，可以透明地集成[AOP](http://blog.csdn.net/tangtong1/article/details/51326887#aop-introduction)到软件中。

Spring被设计为非侵入式的，这意味着你的域逻辑代码通常不会依赖于框架本身。在集成层（比如数据访问层），会存在一些依赖同时依赖于数据访问技术和Spring，但是这些依赖可以很容易地从代码库中分离出来。

本文档是Spring框架的参考指南，如果你有任何请求、评论或问题，[请给我们发邮件](https://groups.google.com/forum/#!forum/spring-framework-contrib)，关于框架本身的问题将在StackOverflow上讨论（见[https://spring.io.questions](https://spring.io.questions/)）。

## 1. Spring入门

这篇参考指南提供了Spring框架的详细信息，包括了对所有功能的全面理解，同时也包括一些重要概念的背景（比如，依赖注入）。

如果你才开始使用Spring，可以通过创建一个基于[Spring Boot](http://projects.spring.io/spring-boot/)的应用开始使用Spring框架。Spring Boot提供了一种快速创建Spring应用的方式，它基于Spring框架，支持约定优于配置，使你可以尽快启动并运行。

可以使用[start.spring.io](http://start.spring.io/)或遵循[入门指南](https://spring.io/guides)（比如，[构建RESTful web应用入门](https://spring.io/guides/gs/rest-service/)）生成一个基本的项目。除了易于理解，这些指南聚集于一个个任务，它们大部分都是基于Spring Boot的，同时也包含了Spring包下的其它项目，以便你可以考虑何时使用它们解决特定的问题。

## 2. Spring框架简介

Spring框架是基于[Java](http://lib.csdn.net/base/javase)平台的，它为开发Java应用提供了全方位的基础设施支持，并且它很好地处理了这些基础设施，所以你只需要关注你的应用本身即可。

Spring可以使用POJO（普通的Java对象，plain old [Java ](http://lib.csdn.net/base/java)objects）创建应用，并且可以将企业服务非侵入式地应用到POJO。这项功能适用于[Java SE](http://lib.csdn.net/base/javase)编程模型以及全部或部分的[Java EE](http://lib.csdn.net/base/javaee)。

那么，做为开发者可以从Spring获得哪些好处呢？

- 不用关心事务API就可以执行数据库事务；
- 不用关心远程API就可以使用远程操作；
- 不用关心JMX API就可以进行管理操作；
- 不用关心JMS API就可以进行消息处理。

译者注：①JMX，Java Management eXtension，Java管理扩展，是一个为应用程序、设备、系统等植入管理功能的框架。JMX可以跨越一系列异构[操作系统](http://lib.csdn.net/base/operatingsystem)平台、系统体系结构和网络传输协议，灵活的开发无缝集成的系统、网络和服务管理应用。②JMS，Java Message Service，Java消息服务，是Java平台上有关面向消息中间件(MOM)的技术规范，它便于消息系统中的Java应用程序进行消息交换,并且通过提供标准的产生、发送、接收消息的接口简化企业应用的开发。

### 2.1 依赖注入（DI）和控制反转（IoC）



2.1.1接口及面向接口编程

2.1.2 什么是IOC

![1527428726848](C:\Users\ADMINI~1\AppData\Local\Temp\1527428726848.png)

2.1.3 Spring的Bean配置

2.1.4 Bean的初始化

![1527429265372](C:\Users\ADMINI~1\AppData\Local\Temp\1527429265372.png)

2.1.5 Spring的常用注入方式

![1527430369177](C:\Users\ADMINI~1\AppData\Local\Temp\1527430369177.png)

![1527430445394](C:\Users\ADMINI~1\AppData\Local\Temp\1527430445394.png)

![1527430609667](C:\Users\ADMINI~1\AppData\Local\Temp\1527430609667.png)

2.1.6 单元测试

![1527429830446](C:\Users\ADMINI~1\AppData\Local\Temp\1527429830446.png)

例如：

![1527429980260](C:\Users\ADMINI~1\AppData\Local\Temp\1527429980260.png)

2.1.7 bean的初始化

![1527430210732](C:\Users\ADMINI~1\AppData\Local\Temp\1527430210732.png)

![1527430310901](C:\Users\ADMINI~1\AppData\Local\Temp\1527430310901.png)



一个Java应用程序，从受限制的[嵌入式](http://lib.csdn.net/base/embeddeddevelopment)应用到n层的服务端应用，典型地是由相互合作的对象组成的，因此，一个应用程序中的对象是相互依赖的。

Java平台虽然提供了丰富的应用开发功能，但是它并没有把这些基础构建模块组织成连续的整体，而是把这项任务留给了[架构](http://lib.csdn.net/base/architecture)师和开发者。你可以使用设计模式，比如工厂模式、抽象工厂模式、创建者模式、装饰者模式以及服务定位器模式等，来构建各种各样的类和对象实例，从而组成整个应用程序。这些设计模式是很简单的，关键在于它们根据最佳实践起了很好的名字，它们的名字可以很好地描述它们是干什么的、用于什么地方、解决什么问题，等等。这些设计模式都是最佳实践的结晶，所以你应该在你的应用程序中使用它们。

Spring的控制反转解决了上述问题，它提供了一种正式的解决方案，你可以把不相干组件组合在一起，从而组成一个完整的可以使用的应用。Spring根据设计模式编码出了非常优秀的代码，所以可以直接集成到自己的应用中。因此，大量的组织机构都使用Spring来保证应用程序的健壮性和可维护性。

背景

2004年Martin Fowler在[他的网站](http://martinfowler.com/articles/injection.html)上提出了关于控制反转（IoC，Inversion of Control）的问题，“The question is, what aspect of control are [they] inverting?”，后来，他又建议重新命名这项原则，使其可以自我解释，从而提出了依赖注入（DI，Dependency Injection）的概念。

### 2.2 模块

Spring大约包含了20个模块，这些模块组成了核心容器（Core [Container](http://lib.csdn.net/base/docker)）、数据访问/集成（Data Access/Integration）、Web、AOP（面向切面编程，Aspect Oriented Programming）、Instrumentation、消息处理（Messaging）和[测试](http://lib.csdn.net/base/softwaretest)（Test），如下图：

**图 2.1. Spring框架概述** 
![spring框架概述](http://img.blog.csdn.net/20160331161910594?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

下面列出了每项功能对应的模块及其主题，它们都有人性的名字（artifact name），这些名字与[依赖管理工具](http://blog.csdn.net/tangtong1/article/details/51326887#dependency-management)中的 **artifact id** 是相互对应的。

#### 2.2.1 核心容器（Core Container）

核心容器包括**spring-core**，**spring-beans**，**spring-context**，**spring-context-support**和**spring-expression**（SpEL，Spring表达式语言，Spring Expression Language）等模块。

**spring-core**和**spring-beans**模块是[Spring框架的基础](http://blog.csdn.net/tangtong1/article/details/51326887#beans-introduction)，包括控制反转和依赖注入等功能。BeanFactory是工厂模式的微妙实现，它移除了编码式单例的需要，并且可以把配置和依赖从实际编码逻辑中解耦。

[Context](http://blog.csdn.net/tangtong1/article/details/51326887#context-introduction)（**spring-context**）模块是在[Core和Bean](http://blog.csdn.net/tangtong1/article/details/51326887#beans-introduction)模块的基础上建立起来的，它以一种类似于JNDI注册的方式访问对象。Context模块继承自Bean模块，并且添加了国际化（比如，使用资源束）、事件传播、资源加载和透明地创建上下文（比如，通过Servelet容器）等功能。Context模块也支持Java EE的功能，比如EJB、JMX和远程调用等。**ApplicationContext**接口是Context模块的焦点。**spring-context-support**提供了对第三方库集成到Spring上下文的支持，比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、模板引擎（FreeMarker, JasperReports, Velocity）等。

**spring-expression**模块提供了强大的[表达式语言](http://blog.csdn.net/tangtong1/article/details/51326887#expressions)用于在运行时查询和操作对象图。它是JSP2.1规范中定义的统一表达式语言的扩展，支持set和get属性值、属性赋值、方法调用、访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、选择以及聚合等。

#### 2.2.2 AOP和检测（Instrumentation）

**spring-aop**模块提供了[面向切面编程](http://blog.csdn.net/tangtong1/article/details/51326887#aop-introduction)（AOP）的实现，可以定义诸如方法拦截器和切入点等，从而使实现功能的代码彻底的解耦出来。使用源码级的元数据，可以用类似于.Net属性的方式合并行为信息到代码中。

**spring-aspects**模块提供了对AspectJ的集成。

**spring-instrument**模块提供了对检测类的支持和用于特定的应用服务器的类加载器的实现。**spring-instrument-tomcat**模块包含了用于tomcat的Spring检测代理。

#### 2.2.3 消息处理（messaging）

Spring 4 包含的**spring-messaging**模块是从Spring集成项目的关键抽象中提取出来的，这些项目包括**Message**、**MessageChannel**、**MessageHandler**和其它服务于消息处理的项目。这个模块也包含一系列的注解用于映射消息到方法，这类似于Spring MVC基于编码模型的注解。

#### 2.2.4 数据访问与集成

数据访问与集成层包含JDBC、ORM、OXM、JMS和事务模块。 
（译者注：JDBC=Java Data Base Connectivity，ORM=Object Relational Mapping，OXM=Object XML Mapping，JMS=Java Message Service）

**spring-jdbc**模块提供了[JDBC](http://blog.csdn.net/tangtong1/article/details/51326887#jdbc-introduction)抽象层，它消除了冗长的JDBC编码和对[数据库](http://lib.csdn.net/base/mysql)供应商特定错误代码的解析。

**spring-tx**模块支持[编程式事务和声明式事务](http://blog.csdn.net/tangtong1/article/details/51326887#transaction)，可用于实现了特定接口的类和所有的POJO对象。 
（译者注：编程式事务需要自己写beginTransaction()、commit()、rollback()等事务管理方法，声明式事务是通过注解或配置由spring自动处理，编程式事务粒度更细）

**spring-orm**模块提供了对流行的[对象关系映射](http://blog.csdn.net/tangtong1/article/details/51326887#orm-introduction)API的集成，包括[JPA](http://blog.csdn.net/tangtong1/article/details/51326887#orm-jpa)、[JDO](http://blog.csdn.net/tangtong1/article/details/51326887#orm-jdo)和[Hibernate](http://blog.csdn.net/tangtong1/article/details/51326887#orm-hibernate)等。通过此模块可以让这些ORM框架和spring的其它功能整合，比如前面提及的事务管理。

**spring-oxm**模块提供了对[OXM](http://blog.csdn.net/tangtong1/article/details/51326887#oxm)实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等。

**spring-jms**模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了**spring-messaging**模块。

#### 2.2.5 Web

Web层包括**spring-web**、**spring-webmvc**、**spring-websocket**、**spring-webmvc-portlet**等模块。

**spring-web**模块提供面向web的基本功能和面向web的应用上下文，比如多部分（multipart）文件上传功能、使用Servlet监听器初始化IoC容器等。它还包括HTTP客户端以及Spring远程调用中与web相关的部分。

**spring-webmvc**模块（即Web-Servlet模块）为web应用提供了模型视图控制（[MVC](http://blog.csdn.net/tangtong1/article/details/51326887#mvc-introduction)）和REST Web服务的实现。Spring的MVC框架可以使领域模型代码和web表单完全地分离，且可以与Spring框架的其它所有功能进行集成。

**spring-webmvc-portlet**模块（即Web-Portlet模块）提供了用于Portlet环境的MVC实现，并反映了**spring-webmvc**模块的功能。

#### 2.2.6 Test

**spring-test**模块通过JUnit和TestNG组件支持[单元测试](http://blog.csdn.net/tangtong1/article/details/51326887#unit-testing)和[集成测试](http://blog.csdn.net/tangtong1/article/details/51326887#integration-testing)。它提供了一致性地[加载](http://blog.csdn.net/tangtong1/article/details/51326887#testcontext-ctx-management)和[缓存](http://blog.csdn.net/tangtong1/article/details/51326887#testcontext-ctx-management-caching)Spring上下文，也提供了用于单独测试代码的[模拟对象](http://blog.csdn.net/tangtong1/article/details/51326887#mock-objects)（mock object）。

### 2.3 使用场景

前面提及的构建模块使得Spring在很多场景成为一种合理的选择，不管是资源受限的嵌入式应用还是使用了事务管理和web集成框架的成熟的企业级应用。

**图2.2. 典型的成熟的Spring web应用程序** 
![典型的成熟的Spring web应用程序](http://img.blog.csdn.net/20160405123611266?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

Spring的[声明式事务管理](http://blog.csdn.net/tangtong1/article/details/51326887#transaction-declarative)可以使web应用完成事务化，就像使用EJB容器管理的事务。所有客制的业务逻辑都可以使用简单的POJO实现，并用Spring的IoC容器进行管理。另外，还包括发邮件和验证功能，其中验证功能是从web层分离的，由你决定何处执行验证。Spring的ORM可以集成JPA、[hibernate](http://lib.csdn.net/base/javaee)和JDO等，比如，使用Hibernate时，可以继续使用已存在的映射文件和标准的Hibernate的SessionFactory配置。表单控制器无缝地把web层和领域模型集成在一起，移除了ActionForms和其它把HTTP参数转换成领域模型的类。

**图2.3. 使用第三方web框架的Spring中间件** 
![使用第三方web框架的Spring中间件](http://img.blog.csdn.net/20160405150119917?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

一些场景可能不允许你完全切换到另一个框架。然而，Spring框架不强制你使用它所有的东西，它不是非此即彼（all-or-nothing）的解决方案。前端使用Struts、Tapestry、JSF或别的UI框架可以和Spring中间件集成，从而使用Spring的事务管理功能。仅仅只需要使用**ApplicationContext**连接业务逻辑，并使用**WebApplicationContext**集成web层即可。

**图2.4. 远程调用使用场景** 
![远程调用使用场景](http://img.blog.csdn.net/20160405161505242?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

当需要通过web服务访问现有代码时，可以使用Spring的**Hessian-**，**Burlap-**，**Rmi-**或者**JaxRpcProxyFactory**类，远程访问现有的应用并非难事。

**图2.5. EJB-包装现有的POJO** 
![EJB-包装现有的POJO](http://img.blog.csdn.net/20160405163407827?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

Spring框架也为EJB提供了[访问抽象层](http://blog.csdn.net/tangtong1/article/details/51326887#ejb)，可以重新使用现有的POJO并把它们包装到无状态的会话bean中，以使其用于可扩展的安全的web应用中。

#### 2.3.1 依赖管理和命名约定

依赖管理和依赖注入是两码事。为了让应用程序拥有这些Spring的非常棒的功能（如依赖注入），需要导入所需的全部jar包，并在运行时放在classpath下，有可能的话编译期也应该放在classpath下。这些依赖并不是被注入的虚拟组件，而是文件系统上典型的物理资源。依赖管理的处理过程涉及到定位这些资源、存储并添加它们到classpath下。依赖可能是直接的（比如运行时依赖于Spring），也可能是间接的（比如依赖于**commons-dbcp**，**commons-dbcp**又依赖于**commons-pool**）。间接的依赖又被称作“传递”，它们是最难识别和管理的。

如果准备使用Spring，则需要拷贝一份所需模块的Spring的jar包。为了便于使用，Spring被打包成一系列的模块以尽可能地减少依赖，比如，如果不是在写一个web应用，那就没必要引入spring-web模块。这篇文档中涉及到的Spring模块，我们使用**spring-\***或**spring-\*.jar**的命名约定，其中，*****代表模块的短名字（比如，**spring-core**、**spring-webmvc**、**spring-jms**等等）。实际使用的jar包正常情况下都是带有版本号的（比如，**spring-core-4.3.0.RELEASE.jar**）。

每个版本的Spring都会在以下地方发布artifact：

- Maven中央仓库，默认的Maven查询仓库，并且不需要特殊的配置就可以使用。许多Spring依赖的公共库也可以从Maven中央仓库获得，并且大部分的Spring社区也使用Maven作为依赖管理工具，所以很方便。Maven中的jar包命名格式为**spring-\*-<version>.jar**，其groupId是org.springframework。
- 特别为托管Spring的公共的Maven仓库。除了最终的GA版本，这个仓库也托管了开发的快照版本和里程碑版本。jar包和Maven中央仓库中的命名一致，所以这也是一个获取Spring的开发版本的有用地方，可以和Maven中央仓库中部署的其它库一起使用。这个仓库也包含了捆绑了所有Spring jar包的发行版的zip文件，以便于下载。

因此，首先要做的事就是决定如何管理依赖关系，我们一般推荐使用自动管理的系统，比如Maven、Gradle或Ivy，当然你也可以手动下载所有的jar包。

下面列出了Spring的artifact，每个模块更完整的描述，参考 [2.2 模块](http://blog.csdn.net/tangtong1/article/details/51326887#modules) 章节。

**表2.1. Spring框架的artifact**

| groupId             | artifactId               | 描述                                       |
| ------------------- | ------------------------ | ------------------------------------------ |
| org.springframework | spring-aop               | 基于代理的AOP                              |
| org.springframework | spring-aspects           | 基于切面的AspectJ                          |
| org.springframework | spring-beans             | bean支持，包括Groovy                       |
| org.springframework | spring-context           | 运行时上下文，包括调度和远程调用抽象       |
| org.springframework | spring-context-support   | 包含用于集成第三方库到Spring上下文的类     |
| org.springframework | spring-core              | 核心库，被许多其它模块使用                 |
| org.springframework | spring-expression        | Spring表达式语言                           |
| org.springframework | spring-instrument        | JVM引导的检测代理                          |
| org.springframework | spring-instrument-tomcat | tomcat的检测代理                           |
| org.springframework | spring-jdbc              | JDBC支持包，包括对数据源设置和JDBC访问支持 |
| org.springframework | spring-jms               | JMS支持包，包括发送和接收JMS消息的帮助类   |
| org.springframework | spring-messaging         | 消息处理的架构和协议                       |
| org.springframework | spring-orm               | 对象关系映射，包括对JPA和Hibernate支持     |
| org.springframework | spring-oxm               | 对象XML映射                                |
| org.springframework | spring-test              | 单元测试和集成测试组件                     |
| org.springframework | spring-tx                | 事务基础，包括对DAO的支持及JCA的集成       |
| org.springframework | spring-web               | web支持包，包括客户端及web远程调用         |
| org.springframework | spring-webmvc            | REST web服务及web应用的MVC实现             |
| org.springframework | spring-webmvc-portlet    | 用于Portlet环境的MVC实现                   |
| org.springframework | spring-websocket         | WebSocket和SockJS实现，包括对STOMP的支持   |

##### Spring的依赖和被依赖

Spring对大部分企业和其它外部工具提供了集成和支持，把强制性的外部依赖降到了最低，这样就不需要为了简单地使用Spring而去寻找和下载大量的jar包了。基本的依赖注入只有一个强制性的外部依赖，那就是日志管理（参考下面关于日志管理选项的详细描述）。

下面列出依赖于Spring的应用的基本配置步骤，首先使用Maven，然后Gradle，最后Ivy。在所有案例中，如果有什么不清楚的地方，参考所用的依赖管理系统的文档或查看一些范例代码——Spring构建时本身使用Gradle管理依赖，所以我们的范例大部分使用Gradle或Maven。

##### Maven依赖关系管理

如果使用Maven作为依赖管理工具，甚至不需要明确地提供日志管理的依赖。例如，创建应用上下文并使用依赖注入配置应用程序，Maven的依赖关系看起来像下面一样：

```
<dependencies>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-context</artifactId>         <version>4.3.0.RELEASE</version>         <scope>runtime</scope>     </dependency> </dependencies>1234567812345678
```

就这样，注意如果不需要编译Spring API，可以把scope声明为runtime，这是依赖注入使用的典型案例。

上面的示例使用Maven中央仓库，如果使用Spring的Maven仓库（例如，里程碑或开发快照），需要在Maven配置中指定仓库位置。

release版本：

```
<repositories>     <repository>         <id>io.spring.repo.maven.release</id>         <url>http://repo.spring.io/release/</url>         <snapshots><enabled>false</enabled></snapshots>     </repository> </repositories>12345671234567
```

里程碑版本：

```
<repositories>     <repository>         <id>io.spring.repo.maven.milestone</id>         <url>http://repo.spring.io/milestone/</url>         <snapshots><enabled>false</enabled></snapshots>     </repository> </repositories>12345671234567
```

快照版本：

```
<repositories>     <repository>         <id>io.spring.repo.maven.snapshot</id>         <url>http://repo.spring.io/snapshot/</url>         <snapshots><enabled>true</enabled></snapshots>     </repository> </repositories>12345671234567
```

##### Maven的“物料清单式”依赖

使用Maven时可能会不小心混合了Spring不同版本的jar包。例如，你可能会发现第三方库或其它的Spring项目存在旧版本的传递依赖。如果没有明确地声明直接依赖，各种各样不可预料的情况将会出现。

为了解决这个问题，Maven提出了“物料清单式”（BOM）依赖的概念。可以在**dependencyManagement**部分导入**spring-framework-bom**以保证所有的Spring依赖（不管直接还是传递依赖）使用相同的版本。

```
<dependencyManagement>     <dependencies>         <dependency>             <groupId>org.springframework</groupId>             <artifactId>spring-framework-bom</artifactId>             <version>4.3.0.RELEASE</version>             <type>pom</type>             <scope>import</scope>         </dependency>     </dependencies> </dependencyManagement>12345678910111234567891011
```

使用BOM的另外一个好处是不再需要指定**<version>**属性了：

```
<dependencies>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-context</artifactId>     </dependency>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-web</artifactId>     </dependency> <dependencies>1234567891012345678910
```

##### Gradle依赖关系管理

为了在[Gradle](http://www.gradle.org/)构建系统中使用Spring仓库，需要在**repositories**部分包含合适的URL：

```
repositories {     mavenCentral()     // and optionally...     maven { url "http://repo.spring.io/release" } }1234512345
```

可以酌情把**repositories** URL中的**/release**修改为**/milestone**或**/snapshot**。一旦仓库配置好了，就可以按Gradle的方式声明依赖关系了。

```
dependencies {     compile("org.springframework:spring-context:4.3.0.RELEASE")     testCompile("org.springframework:spring-test:4.3.0.RELEASE") }12341234
```

##### Ivy依赖关系管理

使用[Ivy](http://ant.apache.org/ivy)管理依赖关系有相似的配置选项。

在**ivysettings.xml**中添加resolver配置使Ivy指向Spring仓库：

```
<resolvers>     <ibiblio name="io.spring.repo.maven.release"             m2compatible="true"             root="http://repo.spring.io/release/"/> </resolvers>1234512345
```

可以酌情把**root** URL中的**/release**修改为**/milestone**或**/snapshot**。一旦配置好了，就可以按照惯例添加依赖了（在ivy.xml中）：

```
<dependency org="org.springframework"     name="spring-core" rev="4.3.0.RELEASE" conf="compile->runtime"/>1212
```

##### 发行版的Zip文件

虽然使用支持依赖管理的构建系统是获取Spring框架的推荐方法，但是也支持通过下载Spring的发行版zip文件获取。

发行版zip文件发布在了Sprng的Maven仓库上（这只是为了方便，不需要额外的Maven或其它构建系统去下载它们）。

浏览器中打开<http://repo.spring.io/release/org/springframework/spring>，并选择合适版本的子目录，就可以下载发行版的zip文件了。发行文件以**-dist.zip**结尾，例如，**spring-framework-{spring-version}-RELEASE-dist.zip**。发行文件也包含[里程碑](http://repo.spring.io/milestone/org/springframework/spring)版本和[快照](http://repo.spring.io/snapshot/org/springframework/spring)版本。

#### 2.3.2 日志管理

对于Spring来说日志管理是非常重要的依赖关系，因为a）它是唯一的强制性外部依赖，b）每个人都喜欢从他们使用的工具看到一些输出，c）Spring集成了许多其它工具，它们都选择了日志管理的依赖。应用程序开发者的目标之一通常是在整个应用程序（包括所有的外部组件）的中心位置统一配置日志管理，这是非常困难的因为现在有很多日志管理的框架可供选择。

Spring中强制的日志管理依赖是Jakarta Commons Logging API（JCL）。我们编译了JCL，并使JCL的**Log**对象对继承了Spring框架的类可见。对用户来说所有版本的Spring使用相同的日志管理库很重要：迁移很简单因为Spring保存了向后兼容，即使对于扩展了Spring的应用也能向后兼容。我们是怎么做到的呢？我们让Spring的一个模块明确地依赖于**commons-logging**（JCL的典型实现），然后让所有其它模块都在编译期依赖于这个模块。例如，使用Maven，你想知道哪里依赖了**commons-logging**，其实是Spring确切地说是其核心模块**spring-core**依赖了。

**commons-logging**的优点是不需要其它任何东西就可以使应用程序运转起来。它拥有一个运行时发现[算法](http://lib.csdn.net/base/datastructure)用于在classpath中寻找其它日志管理框架并且适当地选择一个使用（或者告诉它使用哪个）。如果不需要其它的功能了，你就可以从JDK（java.util.logging或JUL）得到一份看起来很漂亮的日志了。你会发现大多数情况下你的Spring应用程序工作得很好且日志很好地输出到了控制台，这很重要。

##### 不使用Commons Logging

不幸的是，**commons-logging**的运行时发现算法虽然对于终端用户很方便，但存在一定的问题。如果我们能让时光倒流，重新开始Spring项目，我们会使用不同的日志管理依赖。首要选择可能是Simple Logging Facade for Java（[SLF4J](http://www.slf4j.org/)），它也被用于了其它一些使用Spring的工具中。

有两种方式关掉**commons-logging**：

1. 从**spring-core**模块中去除对**commons-logging**的依赖（因为这是唯一明确依赖于**commons-logging**的地方）
2. 依赖于一个特定的**commons-logging**且把其jar包换成一个空jar包（具体做法参考[SLF4J FAQ](http://slf4j.org/faq.html#excludingJCL)）

如下，在**dependencyManagement**中添加部分代码就可以排除掉**commons-logging**了：

```
<dependencies>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-core</artifactId>         <version>4.3.0.RELEASE</version>         <exclusions>             <exclusion>                 <groupId>commons-logging</groupId>                 <artifactId>commons-logging</artifactId>             </exclusion>         </exclusions>     </dependency> </dependencies>1234567891011121312345678910111213
```

现在这个应用可能是残缺的，因为在classpath上没有JCL API的实现，所以需要提供一个新的去修复它。下个章节我们将以SLF4J为例子为JCL提供一个替代实现。

##### 使用SLF4J

SLF4J是一个更干净的依赖，且运行时比**commons-logging**更有效率，因为它使用编译期而非运行时绑定其它日志管理框架。这也意味着你不得不明确地指出运行时想做什么，并定义和配置它。SLF4J可以绑定许多公共的日志管理框架，所以通常你可以选择一个已经使用的，绑定它并配置和管理。

SLF4J可以绑定许多公共的日志管理框架，包括JCL，同时也是其它日志管理框架和它本身的桥梁。所以为了在Spring中使用SLF4J，需要用SLF4J-JCL桥梁代替**commons-logging**依赖。一旦这样做了然后日志记录从Spring内部调用转变成调用SLF4J API，因此，如果应用中的其它库使用了这个API，然后将有一个统一的地方用于配置和管理日志。

通常的选择是把Spring桥接到SLF4J，然后从SLF4J到Log4J提供明确的绑定。需要提供4个依赖关系（且排除掉**commons-logging**）：桥梁、SLF4J API、绑定到Log4J和Log4J的实现本身。在Maven中看起来像下面一样：

```
<dependencies>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-core</artifactId>         <version>4.3.0.RELEASE</version>         <exclusions>             <exclusion>                 <groupId>commons-logging</groupId>                 <artifactId>commons-logging</artifactId>             </exclusion>         </exclusions>     </dependency>     <dependency>         <groupId>org.slf4j</groupId>         <artifactId>jcl-over-slf4j</artifactId>         <version>1.5.8</version>     </dependency>     <dependency>         <groupId>org.slf4j</groupId>         <artifactId>slf4j-api</artifactId>         <version>1.5.8</version>     </dependency>     <dependency>         <groupId>org.slf4j</groupId>         <artifactId>slf4j-log4j12</artifactId>         <version>1.5.8</version>     </dependency>     <dependency>         <groupId>log4j</groupId>         <artifactId>log4j</artifactId>         <version>1.2.14</version>     </dependency> </dependencies>123456789101112131415161718192021222324252627282930313233123456789101112131415161718192021222324252627282930313233
```

似乎这么多依赖仅仅用于获取日志。在类加载器问题上，它应该表现得比**commons-logging**更好，尤其是在像OSGi这样严格的容器中。而且，它也有性能优势因为绑定发生在编译期而非运行时。

对于SLF4J用户更普遍的选择是直接绑定[Logback](http://logback.qos.ch/)，这需要更少的步骤，生成更少的依赖。这样移除了额外的绑定因为Logback直接实现了SLF4J，所以仅仅需要两个库即可而不用四个库（**jcl-over-slf4j**和**logback**）。这样做的话还需要把slf4j-api依赖从其它外部依赖（不是Spring）中排除掉，因为在classpath下仅仅需要一个版本的API。

##### 使用Log4J

许多人使用Log4J作为日志管理框架。它是高效和完善的，实际上在构建和测试Spring的时候我们运行时就是使用它。Spring也提供了一些工具用于配置和初始化Log4J，所以某些模块在编译期可以选择依赖于Log4J。

为了使Log4J代替默认的JCL依赖（**commons-logging**），仅仅提供一个配置文件（**log4j.properties**或**log4j.xml**）放在classpath根目录下即可。Maven中的配置如下：

```
<dependencies>     <dependency>         <groupId>org.springframework</groupId>         <artifactId>spring-core</artifactId>         <version>4.3.0.RELEASE</version>     </dependency>     <dependency>         <groupId>log4j</groupId>         <artifactId>log4j</artifactId>         <version>1.2.14</version>     </dependency> </dependencies>123456789101112123456789101112
```

下面是log4j.properties的样例，用于打印日志到控制台：

```
log4j.rootCategory=INFO, stdout  log4j.appender.stdout=org.apache.log4j.ConsoleAppender log4j.appender.stdout.layout=org.apache.log4j.PatternLayout log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %t %c{2}:%L - %m%n  log4j.category.org.springframework.beans.factory=DEBUG12345671234567
```

##### 带有本地JCL的运行时容器

许多人在一个容器中运行Spring应用程序，而这个容器本身又提供了JCL的实现。IBM的Websphere Application Server（WAS）是一个原型。这经常引起一些问题，而且不幸的是没有很好的解决方案，简单地从应用中排除掉**commons-logging**在大部分情况下还不够。

更清楚地描述：这个问题通常并不与JCL本身有关，甚至是**commons-logging**，而是他们绑定了**commons-logging**到另一个框架（通常是Log4J）。这会失败是因为**commons-logging**改变了在旧版本（1.0）和新版本（1.1）中执行运行时发现算法的方式，其中，旧版本在一些容器中还在使用，新版本是现在大部分人使用的。Spring没有使用JCL API的其它部分，所以不会有什么问题，但是一旦Spring或你的应用试图记录日志就会发现Log4J不能工作了。（译者注：此处的意思是即使发生了上面的冲突，Spring也不会去检查，直接运行的时候需要打印日志的时候才会出错）

在WAS这个案例中，最简单的方法就是倒置类加载器的继承（IBM称作“parent last”，即把父类放后面），以便应用程序而不是容器控制JCL依赖。这种选择并不总是管用的，在公共领域有很多其它建议的替代方案，且你的里程可能会随着确切的版本和容器的特性而改变。（译者注：此处的意思是上面介绍的方法并不是唯一的，需要根据不同的版本和容器作出相应的方案）