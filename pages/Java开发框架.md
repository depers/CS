- Spring
	- 《Spring4.x企业级应用开发实战》
		- 第一章 Spring概述
		  collapsed:: true
			- Spring的体系结构
			  collapsed:: true
				- IoC
				  collapsed:: true
					- IoC容器
						- 用配置的方式对类的依赖关系进行描述
						- IoC容器负责依赖类之间的创建、拼接、管理和获取等工作
						- BeanFactory是Spring框架的核心接口
					- Context模块
						- ApplicationContext是Context模块的核心接口
				- AOP
				  collapsed:: true
					- 提供了AOP Alliance规范的实现
					- 整合了AspectJ框架
					- JDK5.0提供了引入了java.lang.instrument，允许JVM在启动的时候启用一个代理类，通过代理类可以在运行期修改类的字节码，改变一个类的功能，从而实现AOP的功能。
					-
				- 数据访问和集成
				  collapsed:: true
					- 不同数据形式可以采用不同的数据访问方式，比如JDBC、MyBatis或Hibernate
					- Spring建立了与数据形式和数据访问方式无关的统一的DAO层，将数据访问的检查型异常转换为了非检查异常，提供了统一的异常体系
					- 借助AOP技术，提供了声明式事务的功能
				- Web及远程操作
				  collapsed:: true
					- Spring提供了Web应用的各种工具类
					- Spring提供了类似于Struts的MVC框架
				- WebSocket
			- Spring对Java版本的要求
			  collapsed:: true
				- 推荐使用Java8.0，最低Java6.0
				-
			- Spring的新特性
			  collapsed:: true
				- 全面支持Java8
					- [jarjar工具](https://code.google.com/archive/p/jarjar/)
						- 我的理解是可以将原本的以jar包形式引用的代码，直接将其代码编译到自己的项目中，无需再引用这个jar。
					- Java8的Lambda表达式
					- Java8的时间和日期API
					  collapsed:: true
						- 如果我们的Controller需要从请求参数中获取Date、LocalDate或者是LocalDateTime，Spring为我们提供了这样的支持
							- 具体可以参考这篇文章： [Working with Date Parameters in Spring](https://www.baeldung.com/spring-date-parameters)
					- 重复注解的支持
					  collapsed:: true
						- Spring4.0只支持@Scheduled和@PropertySource可以重复定义
					- 空指针终结者：`Optional<>`
						- 在Spring4.0中使用Optional<>的两个场景
						  collapsed:: true
							- 一是使用@Autowired注入对象的时候
							  ```java
							  // 原来
							  @Autowired(required=false)
							  private UserDao userDao;
							  
							  // 现在
							  
							  @Autowired
							  private Optional<UserDao> userDao;
							  ```
							- 二是在定义Controller请求参数的时候，定义某些参数是可选的
							  ```java
							  // 原来
							  @RequestMapping("/hello")
							  public User getUser(String id,  @RequestParam(required=false) String username)
							  
							  
							  // 现在
							  @RequestMapping("/hello")
							  public User getUser(String id, Optional<String> username)
							  ```
		- 第二章 快速入门
		  collapsed:: true
			- 领域对象模型的实体类可以分为以下四种
			  collapsed:: true
				- VO（View Object）：表示视图层状态对应的对象
				- DTO（Data Transfer Object）：数据传输对象，一般泛指展示层和服务层之间的数据传输对象
				- DO（Domain Object）：领域对象，即业务实体对象
				- PO（Persistent Object）：持久化对象，表示持久层的数据结构（对应数据库表）
			- ModelAndView
			  collapsed:: true
				- 即包含视图信息，又包括视图渲染所需的模型数据信息
				- ModelAndView的第一个参数代表视图的逻辑名，第二个参数代表数据模型名称，第三个参数代表数据模型对象。其中数据模型对象将以数据模型名称为参数名放置到request的属性中：`request.setAttribute(name, value)`
		- 第三章 Spring Boot
		  collapsed:: true
			- 安装配置
			  collapsed:: true
				- 基于Maven环境配置
				  collapsed:: true
					- 简化依赖的版本管理方式
						- 继承Spring Boot提供的根默认配置依赖`spring-boot-starter-parent`
						- 如果不想继承，则可以选择导入Spring Boot提供的根配置，即`spring-boot-dependencies`
					- 引入spring-boot-maven-plugin，简化Spring Boot项目的打包部署
				- 基于Gradle环境配置
				- 基于Spring Boot CLI环境配置
				- 代码包结构规划
					- 包规划
						- dao：放置数据库操作的代码
						- domain：领域对象
						- service：具体的代码逻辑
						- web：Controller放置的位置
						- `Application.java`：应用主类，在类上需要标注`@SpringBootApplication`注解，并在main方法中通过`SpringApplication.run()`方法启动即可。
			- 持久层
			  collapsed:: true
				- 操作数据库的方式
				  collapsed:: true
					- 一通过Spring内置的轻量级的JdbcTemplate，可以直接在pom文件中添加`spring-boot-starter-jdbc`
					- 二使用第三方持久化框架Hibernate或Mybatis，使用Hibernate可以直接在pom文件中添加`spring-boot-starter-date-jpa`，使用Mybatis可以直接在pom文件添加`mybatis-spring-boot-starter`
					- 除了上面的依赖外，我们还要添加数据库的驱动依赖，比如MySQL的`mysql-connector-java`
				- Spring Boot中数据库的配置方式
				  collapsed:: true
					- 一通过自定义连接的方式，这种方式我们需要做以下三步
					  collapsed:: true
						- 1.配置数据库连接信息
						- 2.指定自定义连接池，常见的数据库连接池
						  collapsed:: true
							- DBCP
							- C3P0
							- HairkCP
							- Druid
						- 3.配置连接池配置信息
					- 二通过JNDI的方式
				- 初始化数据库脚本
				  collapsed:: true
					- 在Spring启动的时候，初始化预先配置的DDL或DML语句
				- 持久层涉及到的注解
					- `@Repository`
			- 业务层
			  collapsed:: true
				- 业务层两个重要的步骤
				  collapsed:: true
					- 一编写正确的业务逻辑
					- 二对业务代码中事务的管控，这里有两种配置方式
						- 第一种，在类Application上添加`@EnableTransactionManagement`注解，然后在Service方法上添加`@Transational`注解，这个方法就会被事物增强；如果在Service类级别上添加`@Transational`注解，那当前Service类的所有方法都将得到事务增强。
						- 第二种，自定义事务管理器，在类Application上添加`@EnableTransactionManagement`注解，然后在添加自定义的事务管理器txManager()方法，并在方法上标注`@Bean`注解。此时Spring启动会加载自定义的事务管理器，不会重新实例化其他的事务管理器。
				- 分布式事务的支持
					- atomikos
					- bitronix
				- 业务层涉及到的注解
				  collapsed:: true
					- `@Service`
			- 展示层
			  collapsed:: true
				- 书中的项目采用的jsp，并且采用了JSTL标签
				- 配置Spring MVC框架
				- 基于Spring Boot开发的web项目，在启动时需要通过spring-boot-maven-plugin插件命令来启动应用或者通过Spring Boot命令来运行，否则可能会存在访问视图页面报404的情况
			- 运维支持
			  collapsed:: true
				- Spring提供了一个功能完备且可定制的启动器-Actuator，实现对应用本身、数据库等服务健康检查的检测功能。
		- 第四章 Ioc容器
			- Ioc概念的解释
			  collapsed:: true
				- 这里我来说下我的理解，在代码开发的时候，原本程序中调用类与实现类的交互调用，使得程序越来越复杂，我们为了实现程序的解耦，原本调用类中对实现类的调用，变成了对其接口的调用，引入了一个中间人的角色，由中间人去维护调用类和实现类的关系，决定具体使用哪个实现类去完成调用逻辑。这个逻辑我们称为依赖注入，另一种对该功能的解释是控制反转。
			- Ioc的类型
			  collapsed:: true
				- 一构造函数注入
					- 在调用类的构造函数中将接口实现类的对象赋给接口实例，从而实现依赖注入
					- 缺点
						- 每次创建调用类对象时都要完成对实现类接口实例的注入，在某些场景下我们可能并不需要使用该实现类接口的实例，存在资源浪费的情况
				- 二属性注入
					- 属性注入是可以有选择的通过Setter方法完成对调用类所需依赖的实现类实例的注入，更加灵活
				- 三接口注入
					- 将调用类所有依赖注入的逻辑抽取到一个接口中，调用类通过实现该接口提供相应的注入方法。这种方式与构造函数注入和属性注入区别不大，还新增了一个接口增加了类的数量，不推荐使用。
				- Spring支持**构造函数注入**和**属性注入**。
			- 通过容器完成依赖关系的注入
				- 从上一节Ioc的类型中我们看到，我们虽然实现了调用类和实现类的解耦，但是在调用类的代码中仍然存在实现类接口的代码，要想将实现类接口的代码也剔除的话，我们就需要一个三方的容器来去维护和管理两个类之间的依赖关系，Spring Ioc容器就是为此而生的。
				- Spring Ioc容器的实现依赖于Java反射。
			- Java相关的知识点
				- 类加载器ClassLoader
				- Java反射相关知识
			- 资源访问
				- Spring提供的Resource接口，提供了更强大的底层资源访问的能力
					- [使用Resource](https://www.liaoxuefeng.com/wiki/1252599548343744/1282383017934882)
					- [Access a File from the Classpath in a Spring Application](https://www.baeldung.com/spring-classpath-file-access)
				- 资源加载
					- 资源地址表达式
						- `classpath:`和`classpath*:`的区别
							- `classpath:com/smart/module*.xml`只会加载**一个**模块的配置文件
							- `classpath*:com/smart/module*.xml`会加载com/smart目录下**所有的**以mudule开头的xml文件
						- 支持的地址前缀
							- `classpath:`：从类路径中加载，后面跟类的绝对地址
							- `file:`：使用`UrlResource`从文件系统中加载资源，可以是绝对地址或相对地址
							- `http://`：使用`UrlResource`从文件系统中加载资源
							- `ftp://`：使用`UrlResource`从FTP服务器加载资源
							- `没有前缀`：根据`ApplicationContext`的具体实现类采用对应类型的`Resource`
						- 支持Ant风格带通配符的资源地址，支持以下三种通配符
							- `?`：匹配文件名中的一个字符
							- `*`：匹配文件名中的任意字符
							- `**`：匹配多层路径
					- 资源加载器
						- ResourceLoader接口，仅支持带资源类型前缀的表达式，不支持Ant风格的资源路径表达式
						- ResourcePatternResolver，扩展了ResourceLoader接口，支持带资源类型前缀的表达式和Ant风格的资源路径表达式
						- PathMatchingResourcePatternResolver，是Spring提供的标准表达式
					- 注意点：在项目中使用`Resource`接口的`getFile()`获取工程内的文件，且该项目会被打成jar包，会报`FileNotFoundException`，应该使用`Resource#getInputStream()`方法去做。
	- spring-core
	  collapsed:: true
		- IOC
		  collapsed:: true
			- 对IOC的理解
			  collapsed:: true
				- 称为Inverse of Control，控制反转。也被叫做DI（Dependency Injection），依赖注入
				- 让调用者类对某一个接口实现类的依赖关系由第三方（容器或者协作类）注入，从而移除调用者类对某一接口实现类的依赖。换一个通俗的说话，比如说调用者类A要使用接口B的实现类C，故类A和类C之前有着依赖关系，如果我们将依赖关系硬编码到类A的逻辑中，类A代码的耦合度就比较高了，这还只是类A与类C之间有依赖关系，要是类A依赖的类特别多，那该怎么办？类A就需要维护多个类的维护工作，代码耦合度很高。要是有第三方负责去管理这些被调用的类，调用类只负责使用不负责维护，我们开发代码的耦合度就会大大的降低。
			- IOC的类型
			  collapsed:: true
				- 构造函数注入
				- 属性注入
				- 接口注入
			- 参考博客
			  collapsed:: true
				- [极简 Spring 框架 -- 浅析循环依赖](http://heeexy.com/2018/01/28/IoC/)
				- [徒手撸框架--实现IoC](https://diaozxin007.github.io/2018/01/08/spring-ioc/)
		- 在抽象类中使用@Autowired
		  collapsed:: true
			- 背景
			  collapsed:: true
				- 第一，Spring不会对抽象类进行组件扫描。
				- 第二，setter 注入在抽象类中是可能的，但是如果我们不为setter 方法使用final 关键字是有风险的。 如果子类重写 setter 方法，应用程序可能不稳定。
				- 第三，由于 Spring 不支持在抽象类中注入构造函数，我们通常应该让具体的子类提供构造函数参数。 这意味着我们需要在具体子类中进行构造函数注入。
			- 方法一：在 setter 方法中使用@Autowired
			- 方法二：构造函数注入
			- 参考文章
			  collapsed:: true
				- [Using @Autowired in Abstract Classes](https://www.baeldung.com/spring-autowired-abstract-class)
		- 注解@Scope
		  collapsed:: true
			- 作用
			  collapsed:: true
				- Scope，也称作用域，在 Spring IoC 容器是指其创建的 Bean 对象相对于其他 Bean 对象的请求可见范围。
			- Spring IoC容器的作用域
			  collapsed:: true
				- 基本作用域
				  collapsed:: true
					- `singleton`：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例。
					- `prototype`：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例。
				- Web 作用域
				  collapsed:: true
					- `reqeust`：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效。
					- `session`：对于每次HTTP Session，使用session定义的Bean都将产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效。
					- `globalsession`：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效。
				- 自定义作用域。
		- 注解@PostContruct
		  collapsed:: true
			- Spring 仅在 `bean` 属性初始化之后调用一次用 `@PostConstruct` 注释的方法。 请记住，即使没有要初始化的内容，这些方法也会运行。
			- 用`@PostConstruct` 注解的方法可以有任何访问级别，但不能是静态的。
			- 请注意，@PostConstruct 和@PreDestroy 注释都是 Java EE 的一部分。 由于 Java EE 在 Java 9 中被弃用，并在 Java 11 中被删除，我们必须添加一个额外的依赖项来使用这些注释：
			  ```xml
			  <dependency>
			      <groupId>javax.annotation</groupId>
			      <artifactId>javax.annotation-api</artifactId>
			      <version>1.3.2</version>
			  </dependency>
			  ```
			- 参考文章
				- [Guide To Running Logic on Startup in Spring](https://www.baeldung.com/running-setup-logic-on-startup-in-spring)
				- [Spring PostConstruct and PreDestroy Annotations](https://www.baeldung.com/spring-postconstruct-predestroy)
		- 注解@PreDestroy
		  collapsed:: true
			- 用`@PreDestroy` 注释的方法只运行一次，就在 Spring 从应用程序上下文中删除我们的 bean 之前。
			- 与`@PostConstruct` 相同，使用`@PreDestroy` 注释的方法可以具有任何访问级别，但不能是静态的。
			- 请注意，@PostConstruct 和@PreDestroy 注释都是 Java EE 的一部分。 由于 Java EE 在 Java 9 中被弃用，并在 Java 11 中被删除，我们必须添加一个额外的依赖项来使用这些注释：
			  ```xml
			  <dependency>
			      <groupId>javax.annotation</groupId>
			      <artifactId>javax.annotation-api</artifactId>
			      <version>1.3.2</version>
			  </dependency>
			  ```
			- 参考文章
				- [Guide To Running Logic on Startup in Spring](https://www.baeldung.com/running-setup-logic-on-startup-in-spring)
				- [Spring PostConstruct and PreDestroy Annotations](https://www.baeldung.com/spring-postconstruct-predestroy)
	- spring MVC
	  collapsed:: true
		- 过滤器
		  collapsed:: true
			- Filter、Inteceptor、ControllerAdvice、Aspect和Controller的关系
			  collapsed:: true
				- 如下图
				  ![10.png](../assets/10_1680702279599_0.png)
			- 过滤器-Filter
			  collapsed:: true
				- Filter是Servlet提供的过滤器，与Spring无关
				- 是所有过滤组件中最外层的，从粒度来说是最大的
				- 使用场景
				  collapsed:: true
					- 可以获取到Http的请求和响应信息
					- 将请求参数记录到日志文件
					- 资源请求的认证和授权
					- 在将请求正文（body）或报头（header）发送到servlet之前进行格式化
					- 压缩发送给客户端的响应数据
					- 通过添加一些cookie，标题信息等来更改响应
					- 设置请求或响应的报文编码
					- 可以在日志中统计请求处理的耗时
				- 不足
					- 使用Filter是不能获取到具体是**那个Controller的那个方法**处理某一个请求
			- Spring的OncePreRequestFilter
			  collapsed:: true
				- 与Servlet Filter的区别
				- 参考文章
					- [What is OncePerRequestFilter](https://www.baeldung.com/spring-onceperrequestfilter)
			- 拦截器-Intercepter
			  collapsed:: true
				- Interceptor是Spring提供的过滤器
				- 在自定义Interceptor的时候需要实现`org.springframework.web.servlet.HandlerInterceptor`接口
				- 不足
				  collapsed:: true
					- 通过preHandle方法的handle方法，我们可以**获取请求调用的Controller类和方法名**。但是并**不能获取请求的调用方法的具体参数**
				- 使用场景
				  collapsed:: true
					- 可以在日志中统计请求处理的耗时
			- Controller增强-`@ControllerAdvice`
			  collapsed:: true
				- 使用场景
					- 全局异常处理
					- 全局数据绑定
					- 全局数据预处理
			- 切面-aspect
		- 如何多次读取HttpServletRequest
		  collapsed:: true
			- 具体实现
				- jasper:cn/bravedawn/web/config/cachedrequest
			- 参考文章
				- [Reading HttpServletRequest Multiple Times in Spring](https://www.baeldung.com/spring-reading-httpservletrequest-multiple-times)
		- 异常处理
		  collapsed:: true
			- 方法一：为每一个controller添加一个@ExceptionHandler注解的方法
			  collapsed:: true
				- 代码
				  ```java
				  public class FooController{
				      
				      //...
				      @ExceptionHandler({ CustomException1.class, CustomException2.class })
				      public void handleException() {
				          //
				      }
				  }
				  ```
				- 缺点
				  collapsed:: true
					- 带注释的@ExceptionHandler方法只对特定的Controller有效，对整个应用程序不是全局的。当然，为每一个控制器添加一个@ExceptionHandler方法不太适合通用异常处理机制。
			- 方法二：定义一个HandlerExceptionResolver，为Rest API实现统一的异常处理机制
			  collapsed:: true
				- 现有的实现
					- `SimpleMappingExceptionResolver`
					  collapsed:: true
						- SimpleMappingExceptionResolver可以根据需要轻松地将任何异常映射到默认的错误视图。
					- `DefaultHandlerExceptionResolver`
					  collapsed:: true
						- 这个解析器是Spring3.0中引入的，在DispatcherServlet中默认启用。
						- 它用于将标准Spring异常解析为相应的HTTP状态码，即客户端错误4xx和服务器错误5xx状态码。下面是他处理的[Spring异常的完整列表](https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/mvc.html#mvc-ann-rest-spring-mvc-exceptions)，以及它们如何映射到状态代码。
						- 缺点
						  collapsed:: true
							- 虽然它正确的设置了响应的状态码，但有一个限制是它没有为响应体设置任何内容。对于REST API来说——状态码并不能提供给客户端足够的信息，响应也必须有一个主体，以允许应用程序提供关于故障的附加信息。
					- `ExceptionHandlerExceptionResolver`
					  collapsed:: true
						- 这个解析器是Spring3.1中引入的，在DispatcherServlet中默认启用。这个处理器是@ExceptionHandler机制如何工作的核心组件。
					- `ResponseStatusExceptionResolver`
					  collapsed:: true
						- 这个解析器是Spring3.0中引入的，在DispatcherServlet中默认启用。
						- 它的主要职责是能在自定义异常上使用@ResponseStatus注解，并将这些异常映射到HTTP状态码上。
						- 代码
						  ```java
						  @ResponseStatus(value = HttpStatus.NOT_FOUND)
						  public class MyResourceNotFoundException extends RuntimeException {
						      public MyResourceNotFoundException() {
						          super();
						      }
						      public MyResourceNotFoundException(String message, Throwable cause) {
						          super(message, cause);
						      }
						      public MyResourceNotFoundException(String message) {
						          super(message);
						      }
						      public MyResourceNotFoundException(Throwable cause) {
						          super(cause);
						      }
						  }
						  ```
						- 缺点
							- 与DefaultHandlerExceptionResolver一样，该解析器在处理响应体的方式上受到限制——可以映射状态码到响应上，但响应体仍然为空。
				- 自定义HandlerExceptionResolver
					- 要实现的功能：希望能够输出JSON或XML到响应体中，这取决于客户端要求的格式（通过Accept报头）
					- 代码
					  ```java
					  @Component
					  public class RestResponseStatusExceptionResolver extends AbstractHandlerExceptionResolver {
					  
					      @Override
					      protected ModelAndView doResolveException(
					        HttpServletRequest request, 
					        HttpServletResponse response, 
					        Object handler, 
					        Exception ex) {
					          try {
					              if (ex instanceof IllegalArgumentException) {
					                  return handleIllegalArgument(
					                    (IllegalArgumentException) ex, request, response);
					              }
					              ...
					          } catch (Exception handlerException) {
					              logger.warn("Handling of [" + ex.getClass().getName() + "] 
					                resulted in Exception", handlerException);
					          }
					          return null;
					      }
					  
					      private ModelAndView 
					        handleIllegalArgument(IllegalArgumentException ex, HttpServletRequest request, HttpServletResponse response) 
					        throws IOException {
					          response.sendError(HttpServletResponse.SC_CONFLICT);
					          String accept = request.getHeader(HttpHeaders.ACCEPT);
					          ...
					          return new ModelAndView();
					      }
					  }
					  ```
			- 方法三：@ControllerAdvice
			  collapsed:: true
				- Spring3.2通过@ControllerAdvice注解支持了全局的@ExceptionHandler。
				- 这是一种新的机制，脱离了旧的MVC模型，并利用了ResponseEntity以及@ExceptionHandler的类型安全性和灵活性。
				- @ControllerAdvice注释允许我们将之前分散的多个@ExceptionHandler合并为单个的全局错误处理组件。
				- 代码
				  ```java
				  @ControllerAdvice
				  public class RestResponseEntityExceptionHandler 
				    extends ResponseEntityExceptionHandler {
				  
				      @ExceptionHandler(value 
				        = { IllegalArgumentException.class, IllegalStateException.class })
				      protected ResponseEntity<Object> handleConflict(
				        RuntimeException ex, WebRequest request) {
				          String bodyOfResponse = "This should be application specific";
				          return handleExceptionInternal(ex, bodyOfResponse, 
				            new HttpHeaders(), HttpStatus.CONFLICT, request);
				      }
				  }
				  ```
				- 优点
					- 能够自定义响应body体和状态代码
					- 提供了多个异常映射到同一个方法，以便一起处理
					- 可以很好的新的RESTful ResponseEntity响应
				- 缺点
					- 用@ExceptionHandler处理的异常应与其方法参数的异常声明相匹配。如果他们不匹配，编译器不会报错，Spring也不会报错。但是，异常会在运行时实际抛出来时，异常解析机制将失败。
					  ```
					  java.lang.IllegalStateException: No suitable resolver for argument [0] [type=...]
					  HandlerMethod details: ...
					  ```
			- 方法四：ResponseStatusException (Spring 5 and Above)
				- Spring5引入了ResponseStatusException类
				- 我们可以创建它的一个实例，提供一个HttpStatus，并可选的提供一个reason和cause
				- 参考文章
					- [Spring ResponseStatusException](https://www.baeldung.com/spring-response-status-exception)
			- 参考文章
				- [Error Handling for REST with Spring](https://www.baeldung.com/exception-handling-for-rest-with-spring)
		- 开发过程中的错误记录
		  collapsed:: true
			- @RequestBody中的required默认是true，这个接口必须要传输json格式的数据，假如没有数据，就会报错：`Required request body is missing`。如果我们要自己做数据校验的话，可以将required设置为false。
			- Spring Boot请求(状态码是406)Could not find acceptable representation原因
				- 有可能是你的响应对象的属性没有写get/set方法导致的
	- spring-tx
	  collapsed:: true
		- Spring对事务管理的支持
		  collapsed:: true
			- 事务管理的关键抽象
			  collapsed:: true
				-
	- Spring Boot
	  collapsed:: true
		- 依赖管理
		  collapsed:: true
			- Spring Boot 的每个版本都提供了它支持的依赖项列表，因此，我们在引入其他的依赖时不需要在配置中指定依赖项的版本，Spring Boot会自行管理。具体可以参考文章：[springboot依赖的一些配置：spring-boot-dependencies、spring-boot-starter-parent、io.spring.platform](https://www.cnblogs.com/leeego-123/p/12665279.html)
		- 上传文件
		  collapsed:: true
			- 在Spring Boot上传文件的时候，如果你上传的文件是0kb，spring是会报错的，报的错是：`Error parsing HTTP request header java.io.EOFException: null`
		- 重要接口
		  collapsed:: true
			- Interface `ApplicationRunner` 和 `CommandLineRunner`
			  collapsed:: true
				- 作用：
				  collapsed:: true
					-
				- 参考文章
				  collapsed:: true
					- https://www.jianshu.com/p/5d4ffe267596
					- https://www.baeldung.com/running-setup-logic-on-startup-in-spring
				-
		- 日志
		  collapsed:: true
			- Spring Boot 默认使用 SLF4J+Logback 记录日志，其中SLF4J提供了日志接口，Logback提供的日志实现。
			- 日志配置的级别
			  collapsed:: true
				- 使用root级别，即项目的所有日志
				  collapsed:: true
					- 例如：
					  ```
					  logging.level.root=trace
					  ```
				- 使用package级别，即指定包下使用相应的日志级别
				  collapsed:: true
					- 例如：
					  ```
					  logging.level.cn.bravedawn=trace
					  ```
			- 参考
			  collapsed:: true
				- [使用SLF4J和Logback-廖雪峰](https://www.liaoxuefeng.com/wiki/1252599548343744/1264739155914176)
				- [Spring Boot日志配置及输出](http://c.biancheng.net/spring_boot/log-config.html)
	- Spring Test
	  collapsed:: true
		- 在单元测试中如果依赖Spring的RequestContext，怎么办
		  collapsed:: true
			- 先看代码：
			  ```Java
			  // Spring-test 有一个灵活的请求模拟，称为 MockHttpServletRequest。
			  MockHttpServletRequest request = new MockHttpServletRequest();
			  RequestContextHolder.setRequestAttributes(new ServletRequestAttributes(request));
			  ```
			- 参考文章
			  collapsed:: true
				- [How to Mock HttpServletRequest](https://www.baeldung.com/java-httpservletrequest-mock)
	- Spring Cloud
	  collapsed:: true
		- [spring-cloud-release](https://github.com/spring-cloud/spring-cloud-release)
		  collapsed:: true
			- 该项目的作用就是管理SpringCloud版本的发布，主要做了二件事，一个是分布版本的规则，二是管理各个发布版本的子项目的版本的映射关系。
			- 参考文章： https://www.cnblogs.com/hzhuxin/p/12393456.html
		- Open Feign
		  collapsed:: true
			- 配置规则
			  collapsed:: true
				- 第一种：自定义配置类
				  collapsed:: true
					- 自定义FeignClientsConfiguration配置类
					  collapsed:: true
						- openFeign允许我们为每个Feign客户端定制一套组件
						  collapsed:: true
							- 设置@FeignClinet的Configuration属性
							  collapsed:: true
								- 作用：可以对客户端的组件进行自定义，使用新的Bean定义覆盖原有的配置
								- 默认配置类：`org.springframework.cloud.openfeign.FeignClientsConfiguration`
								- 配置的定义的Bean
								  collapsed:: true
									- Decoder – *ResponseEntityDecoder*, which wraps *SpringDecoder*, used to decode the *Response*
									- Encoder – `SpringEncoder` is used to encode the *RequestBody*.
									- Logger – `Slf4jLogger` is the default logger used by Feign.
									- Contract – `SpringMvcContract`, which provides annotation processing
									- Feign-Builder – `HystrixFeign.Builder` is used to construct the components.
									- Client – `LoadBalancerFeignClient` or default Feign client
						- openFeign日志级别
						  collapsed:: true
							- `NONE`：不做任何记录（默认）
							- `BASIC`：仅记录请求方法和 URL 以及响应状态代码和执行时间
							- `HEADERS`：记录基本信息以及请求和响应标头
							- `FULL`：记录请求和响应的标题，正文和元数据
						- 自定义Http客户端
						  collapsed:: true
							- 使用Apache HttpClient
							- 使用OKHttp
				- 第二种：配置文件
				  collapsed:: true
					- 在配置文件中设置全局配置
					- 在配置文件中为每个FeignClient设置专属配置
				- 配置优先级：配置文件中每个FeignClient设置的专属配置 > 配置文件中的全局配置 > 配置类
				- 拦截器的追加规则
				  collapsed:: true
					- `RequestInterceptor` 是拦截器，通过用于在请求发送前做一些处理，比如添加头信息。他可以被专属FeignClient在配置文件中配置、全局配置文件中配置、配置类中配置。
					- 他的模式是追加，而不是覆盖。
					- 若在三种场景都配置了拦截器，则执行顺序是：专属FeignClient在配置文件中配置->全局配置文件中配置->配置类中配置。
					- 若在三种场景都配置了同一个拦截器，则这个拦截器就会被重复执行三次。
			- 数据压缩
			  collapsed:: true
				- 请求压缩配置
				  collapsed:: true
					- 配置代码
					  collapsed:: true
					  ```properties
					  feign.compression.request.enabled=true
					  feign.compression.request.mime-types=application/json
					  feign.compression.request.min-request-size=1
					  ```
						- 上述的配置是无效的，配置了上面的代码之后openFeign会判断当前请求的`content-type`是否包含在`mime-types`属性列表内并且请求的`content-length`必须大于`min-request-size`才会在请求的头信息中添加下面的几个属性：
						  collapsed:: true
							- Content-Encoding: gzip
							- Content-Encoding: deflate
				- 响应压缩配置
				  collapsed:: true
					- 配置代码
					  ```properties
					  feign.compression.response.enabled=true
					  feign.compression.response.useGzipDecoder=true
					  ```
			- 参考文章
			  collapsed:: true
				- [OpenFeign / SpringBoot 响应使用gzip压缩（含例子）](https://blog.csdn.net/Jokers_lin/article/details/126342022)
				- [SpringBoot 使用 Feign 无废话 All-in-one 指南](https://juejin.cn/post/7169549885723639838)
				- [openFeign夺命连环9问，这谁受得了？](https://www.cnblogs.com/cbvlog/p/15322926.html)
				- [Feign Client Exception Handling](https://www.baeldung.com/java-feign-client-exception-handling)
		- Sentinel
		  collapsed:: true
			- 官网：[Sentinel](https://sentinelguard.io/zh-cn/index.html)
			- 流量控制（flow controller）
			  collapsed:: true
				- 定义：
				  collapsed:: true
					- 其原理是监控应用流量的 **QPS** 或**并发线程数**等指标，当达到指定的**阈值**时对流量进行控制，以避免被瞬时的流量高峰冲垮，从而保障应用的**高可用性**。
					- 服务降级一般是指在服务器压力剧增的时候，根据实际业务使用情况以及流量，对一些服务和页面有策略的不处理或者用一种简单的方式进行处理，从而**释放服务器资源的资源以保证核心业务的正常高效运行。**
				- 三种流控效果（controlBehavior）
				  collapsed:: true
					- 快速失败
					  collapsed:: true
						- 默认的流量控制方式，当QPS超过任意规则的阈值后，新的请求就会被立即拒绝，拒绝方式为抛出`FlowException`。
					- warm up（热身）
					  collapsed:: true
						- 即**预热/冷启动**方式。当系统长期处于低水位的情况下，当流量突然增加时，直接把系统拉升到高水位可能瞬间把系统压垮。通过"冷启动"，让通过的流量**缓慢增加**，在**一定时间内**逐渐增加到**阈值上限**，给冷系统一个**预热**的时间，避免冷系统被压垮。
						- 对应**令牌桶算法**
					- 排队等待
					  collapsed:: true
						- 匀速排队方式会严格控制请求通过的间隔时间，也即是让请求以均匀的速度通过。
						- 对应**漏桶算法**
						- 适用场景：这种方式适合用于请求以突刺状来到，这个时候我们不希望一下子把所有的请求都通过，这样可能会把系统压垮；同时我们也期待系统以稳定的速度，逐步处理这些请求，以起到“**削峰填谷**”的效果，而不是拒绝所有请求。
				- 三种流控模式（strategy）
				  collapsed:: true
					- 直接拒绝：接口达到限流条件时，直接限流。
					  collapsed:: true
						- 默认的流量控制方式。
						- 当QPS超过任意规则的阈值后，新的请求就会被立即拒绝，拒绝方式为抛出`FlowException`。
					- 关联：当关联的资源达到阈值时，就限流自己。
					  collapsed:: true
						- **典型的使用场景**：一个是**支付**接口，一个是**下单**接口，此时一旦**支付接口达到了阈值**，那么订单接口就应该被限流，不然这边还在下单，用户等待或者直接被拒绝支付将会极大的影响用户体验。**简而言之：A关联B，一旦B到达阈值，则A被限流**。
					- 链路：只记录指定链路上的流量（指定资源从入口资源进来的流量，如果达到阈值，就可以限流）。
				- 两种统计类型
				  collapsed:: true
					- QPS
					  collapsed:: true
						- 定义：每秒请求数，即在不断向服务器发送请求的情况下，服务器每秒能够处理的请求数量。
						- 通俗理解：同时能接收的请求数量，也就是说同时能**接收**几个任务。
					- 并发线程数
					  collapsed:: true
						- 定义：指的是施压机施加的同时请求的线程数量。
						- 通俗理解：同时处理请求的线程数，也就是说同时有几个人能**干活**。
			- 熔断降级
			  collapsed:: true
				- 服务雪崩的定义
				  collapsed:: true
					- 多个微服务之间调用的时候，假设微服务A调用微服务B和微服务C，微服务B和微服务C有调用其他的微服务，如果整个链路上某个微服务的调用响应式过长或者不可用，对微服务A的调用就会占用越来越多的系统资源，进而引起系统雪崩，所谓的”雪崩效应”。
				- 定义
				  collapsed:: true
					- 应对微服务雪崩效应的一种链路保护机制，类似股市、保险丝
					- 熔断机制是应对雪崩效应的一种微服务链路保护机制，当整个链路的某个微服务不可用或者响应时间太长时，会进行服务的降级，进而熔断该节点微服务的调用，快速返回”错误”的响应信息。
			- 参考文章
			  collapsed:: true
				- [阿里限流神器Sentinel夺命连环 17 问？](https://www.cnblogs.com/cbvlog/p/15385100.html)
- lombok
  collapsed:: true
	- 官网：
- xxl job
  collapsed:: true
	- 路由策略配置
		- 参考文章
			- [xxl-job（四）路由策略](https://blog.csdn.net/w_t_y_y/article/details/117119864)
- Jackson
  collapsed:: true
	- 自定义反序列化器
		- 标准的反序列化器
			- 要求
				- 反序列化的类不能是内部类
				- json必须完整的切合对象属性，才能反序列化成功
		- 在ObjectMapper上自定义反序列化器
			- 适用场景
				- 只想获取json中一部分的json字段，不需要全部获取
		- 为泛型类型添加反序列化器
			- 适用场景
				- 如果需要反序列化的对象中包含泛型字段，我们可以通过自定义反序列化器去做处理
		- 参考文章
			- [Getting Started with Custom Deserialization in Jackson](https://www.baeldung.com/jackson-deserialization)
	- 参考文章
		- [jackson example](https://mkyong.com/tag/jackson/)
- Leaf      
  collapsed:: true
	- 简介
	- 业务系统对于ID号的要求
		- 全局唯一，不能重复
		- 趋势递增，有效的利用MySQL的聚集索引
		- 单调递增，保证下一个ID一定大于上一个ID，例如事务版本号、IM增量消息、排序等特殊需求
		- 信息安全，在一些特殊场景下需要ID是无规则的
	- 常见的生成案例
		- UUID
			- 优点：性能非常高：本地生成，没有网络消耗。
			- 缺点
				- 不易存储，通常为36位长度的字符串
				- 信息不安全，基于MAC地址生成的UUID算法可能会泄露MAC地址
				- UUID过长，MySQL建议主键越短越好，不适合做主键，性能较差
		- 类snowflake
			- 结构
				- 划分为64-bit
				- 1-bit保留位
				- 41-bit表示时间戳，69年的时间
				- 10-bit机器码
				- 12-bit-序列号，可以设置自增序列
			- 优点
				- 毫秒数在高位，自增序列在低位，整个ID都是趋势递增的。
				- 不依赖数据库等第三方系统，以服务的方式部署，稳定性更高，生成ID的性能也是非常高的。
				- 可以根据自身业务特性分配bit位，非常灵活。
			- 缺点
				- 强依赖机器时钟，如果机器上时钟回拨，会导致发号重复或者服务会处于不可用状态。
		- 数据库生成