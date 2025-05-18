- Commons-pool2
  collapsed:: true
	- 参考文章
		- [apache-common-pool2对象池的使用](https://blog.csdn.net/u013332124/article/details/81042375)
		- [commons-pool2的简单使用](https://qiubyte.github.io/2019/10/31/2019/20191031-commons-pool2%E7%9A%84%E7%AE%80%E5%8D%95%E4%BD%BF%E7%94%A8/index.html)
		- [通用对象池化框架Apache Commons Pool 2简析](https://blog.csdn.net/nazeniwaresakini/article/details/108379725)
- easyExcel
  collapsed:: true
	- [SpringBoot+easyExcel 按照模板导出（动态合并单元格）](https://juejin.cn/post/7101590832339238943)
- Swagger
  collapsed:: true
	- 在Spring Boot项目中的使用
	    collapsed:: true
		- 1. 引入依赖
		  
		    ```
		    <dependency>
		         <groupId>io.springfox</groupId>
		         <artifactId>springfox-boot-starter</artifactId>
		         <version>3.0.0</version>
		     </dependency>
		    ```
		- 2.暴露静态资源和接口访问路径，这个参考：https://blog.csdn.net/Yu1441/article/details/110130931
	- 常用注解
		- 在controller方法上：
		  
		    ```java
		    @ApiOperation(value = "接口名称", notes = "接口描述", httpMethod = "POST")
		    ```
		- 在请求或是响应的实体类上：
		  
		    ```java
		    @ApiModel(value = "用户对象BO", description = "从客户端，由用户传入的数据封装在此entity中")
		    ```
		- 在请求或是响应的实体类的具体字段上：
		  
		    ```java
		    @ApiModelProperty(value = "用户名", name = "username", example = "imooc", required = true)
		    ```
	- 汇总文章
		- [Java Swagger 常用注解说明](https://mazq.cn/java/2020/08/06/Swagger-%E5%B8%B8%E7%94%A8%E6%B3%A8%E8%A7%A3%E8%AF%B4%E6%98%8E/)
		- [swagger多包扫描](https://liac.vip/archives/swagger%E5%A4%9A%E5%8C%85%E6%89%AB%E6%8F%8F)
	- 替代品SpringDoc
	  collapsed:: true
		- 参考文章：[秒懂SpringBoot之如何集成SpringDoc（全网目前最新最系统最全面的springdoc教程）](https://shusheng007.top/2023/06/21/springdoc/)
- lombok
  collapsed:: true
	- 注解
	  collapsed:: true
		- `@Data`注解：注在类上，提供类的`get`、`set`、`equals`、`hashCode`、`canEqual`、`toString`方法。
		- `@AllArgsConstructor` ： 注在类上，提供类的全参构造。
		- `@NoArgsConstructor` ： 注在类上，提供类的无参构造。
		- `@Setter` ： 注在属性上，提供 set 方法。
		- `@Getter` ： 注在属性上，提供 get 方法。
		- `@EqualsAndHashCode` ：    注在类上，提供对应的 equals 和 hashCode 方法。
		- `@Log4j/@Slf4j`： 注在类上，提供对应的 Logger 对象，变量名为 log。
		- `@Builder`：采用构建者模式，链式创建对象。
	- lombok默认是不会生成无参构造器的
	  collapsed:: true
		- 当你使用`@Builder`注解时，他会默认为你生成全参构造器。但是因为好多框架喜欢使用`Class.newInstance()`直接实例化对象，如果这个类没有无参构造器就会报错。
		- 所以建议使用同时使用`@AllArgsConstructor`和`@NoArgsConstructor`两个构造器。
	- lombok和Log4j2的结合使用
		- 参考文章：[log4j2+slf4j+lombok整合](https://blog.csdn.net/m0_57099067/article/details/125303294)
	- 参考文章
	  collapsed:: true
		- [Lombok@Builder注解使用和需要注意的坑](https://blog.csdn.net/a648119398/article/details/120513865)
		- [@Data注解 与 lombok](https://www.jianshu.com/p/c1ee7e4247bf)
- Mybatis
  collapsed:: true
	- 一级缓存的问题
		- 背景：今天我在写代码的时候发现，我在一个for循环里面重复执行一个sql，发现sql返回的实体对象还是之前的那个，多次循环查询都是一个对象，而且日志也没有打印sql，我怀疑Mybatis压根就没有执行这条sql。
		- 原因
			- mybatis会默认会开启一级缓存，一级缓存就是同一个`SqlSession`中，执行相同的sql语句，Mybatis会将第一次查询的数据写到缓存中（内存），第二次再次查询的时候就不会从数据库中查询，会直接范湖缓存中的结果。
			- 一级缓存只是相对于同一个`SqlSession`而言。所以在参数和SQL完全一样的情况下，我们使用同一个`SqlSession`对象调用一个Mapper方法，往往只执行一次SQL，因为使用SelSession第一次查询后，MyBatis会将其放在缓存中，以后再查询的时候，如果没有声明需要刷新，并且缓存没有超时的情况下，`SqlSession`都会取出当前缓存的数据，而不会再次发送SQL到数据库。
			- 如果要想每次查询都要去数据库查询，不使用Mybatis的一级缓存，只需要在查询sql中添加`flushCache`属性，将其设置为 `true` 后，只要语句被调用，都会导致本地缓存和二级缓存被清空，默认值：`false`。
			- 我这边还做了一个实验，就是如果在一个`SqlSession`中对先查询了记录A，然后在后续的逻辑中修改了记录A，然后我第二次再次查询记录A的时候发现去数据库查了。也就是说，Mybatis中你对这条记录做了修改，他就会将上一次记录的一级缓存给删除了。
		- 关闭一级缓存
		  ```xml
		  <configuration>
		      <settings>
		          <setting name="localCacheScope" value="Statement"/>
		      </settings>
		  </configuration>
		  ```
		- 参考文章： [mybatis的缓存机制（一级缓存二级缓存和刷新缓存）和mybatis整合ehcache](https://blog.csdn.net/u012373815/article/details/47069223)
	- 二级缓存
		- 二级缓存是针对Application级别的。
	- tinyint类型
		- 在mybatis generator项目中，tinyint类型字段的实体映射逻辑：
		  collapsed:: true
			- 若数据库定义字段为`tinyint(1)` ，映射之后的Java类型为`Boolean`
			- 若数据库定义字段为`tinyint(2)`，映射之后的Java类型为`Byte`
			- 若数据库定义字段为`tinyint(4)`，映射之后的Java类型也为`Byte`
	- sum()函数
		- `sum()`函数可能会返回null值，故在MyBatis查询中应该设置resultType为integer类型，不能是int。查询完成之后，还需要判断该值是否为null，从而避免代码出现空指针。
	- 批量插入
		- [MyBatis 批量插入数据的 3 种方法](https://juejin.cn/post/7016691244973686820)
	- 拦截器的编写
		- 参考文章
			- [MyBatis 拦截器使用方法总结](https://blog.csdn.net/wb1046329430/article/details/111501755)
	- 动态sql
		- `where`
			- *where* 元素只会在子元素返回任何内容的情况下才插入 “WHERE” 子句。而且，若子句的开头为 “AND” 或 “OR”，*where* 元素也会将它们去除。
		- `foreach`
			- 遍历元素。
		- `if`
			- 判断是否为空或者是null，多个条件中间用`and`
		- `trim`
		-
	- typehandler
	  collapsed:: true
		- 一般我们在项目中，直接继承`BaseTypeHandler`进行实现，这个接口一共有四个方法：
			- `void setParameter(PreparedStatement ps, int i, T parameter, JdbcType jdbcType)`：在Mybatis设置参数时该如何把Java类型的参数转换为对应的数据库类型
			- `T getResult(ResultSet rs, String columnName)`：在Mybatis获取数据结果集时如何把数据库类型转换为对应的Java类型
			- `T getResult(ResultSet rs, int columnIndex)`：在Mybatis通过字段位置获取字段数据时把数据库类型转换为对应的Java类型
			- `T getResult(CallableStatement cs, int columnIndex)`：Mybatis在调用存储过程后把数据库类型的数据转换为对应的Java类型
		- 参考文章
			- [Mybatis TypeHandler 介绍及使用](https://blog.csdn.net/Crystalqy/article/details/133923124)
- [transmittable-thread-local](https://github.com/alibaba/transmittable-thread-local)
  collapsed:: true
	- 参考文章
		- [TransmittableThreadLocal原理解析](https://juejin.cn/post/6998552093795549191)
		- [从ThreadLocal谈到TransmittableThreadLocal，从使用到原理](https://juejin.cn/post/7214901105977671717#heading-16)