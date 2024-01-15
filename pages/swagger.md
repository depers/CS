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
    collapsed:: true
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
- 替代品SpringDoc
	- 参考文章：[秒懂SpringBoot之如何集成SpringDoc（全网目前最新最系统最全面的springdoc教程）](https://shusheng007.top/2023/06/21/springdoc/)