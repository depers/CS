- 自定义反序列化器
  collapsed:: true
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
- 在Spring Boot中如何自定义ObjectMapper
	- 场景：在解析Joda框架的DateTime类型的时候，使用默认的ObjectMapper类会报错`org.springframework.http.converter.HttpMessageConversionException: Type definition error: [simple type, class org.joda.time.DateTime]`，原因是我们这边没有配置jackson针对DateTime类型的解析规则。
	- 解决方法：
	  collapsed:: true
		- 第一步：
			- 引入依赖
			  ```xml
			  <dependency>
			    <groupId>com.fasterxml.jackson.datatype</groupId>
			    <artifactId>jackson-datatype-joda</artifactId>
			  </dependency>
			  ```
		- 第二步：
			- 编写序列化规则
			  ```java
			  @Configuration
			  public class JacksonConfig {
			  
			      @Bean
			      @Primary
			      public Jackson2ObjectMapperBuilder jackson2ObjectMapperBuilder() {
			          JodaModule jodaModule = new JodaModule();
			          JacksonJodaDateFormat format = new JacksonJodaDateFormat(DateTimeFormat.forPattern("yyyy-MM-dd HH:mm:ss"));
			          jodaModule.addSerializer(DateTime.class, new DateTimeSerializer(format));
			          return new Jackson2ObjectMapperBuilder()
			                  .modules(jodaModule)
			                  .featuresToDisable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS)
			                  .serializationInclusion(JsonInclude.Include.NON_NULL);
			      }
			  }
			  ```
	- 参考文章：
		- [Spring Boot: Customize the Jackson ObjectMapper](https://www.baeldung.com/spring-boot-customize-jackson-objectmapper)
- 参考文章
	- [jackson example](https://mkyong.com/tag/jackson/)