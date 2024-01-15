- 一级缓存的问题
  collapsed:: true
	- 背景：今天我在写代码的时候发现，我在一个for循环里面重复执行一个sql，发现sql返回的实体对象还是之前的那个，多次循环查询都是一个对象，而且日志也没有打印sql，我怀疑Mybatis压根就没有执行这条sql。
	- 原因
		- mybatis会默认会开启一级缓存，一级缓存就是同一个`SqlSession`中，执行相同的sql语句，Mybatis会将第一次查询的数据写到缓存中（内存），第二次再次查询的时候就不会从数据库中查询，会直接范湖缓存中的结果。
		- 一级缓存只是相对于同一个`SqlSession`而言。所以在参数和SQL完全一样的情况下，我们使用同一个`SqlSession`对象调用一个Mapper方法，往往只执行一次SQL，因为使用SelSession第一次查询后，MyBatis会将其放在缓存中，以后再查询的时候，如果没有声明需要刷新，并且缓存没有超时的情况下，`SqlSession`都会取出当前缓存的数据，而不会再次发送SQL到数据库。
		- 如果要想每次查询都要去数据库查询，不使用Mybatis的一级缓存，只需要在查询sql中添加`flushCache`属性，将其设置为 `true` 后，只要语句被调用，都会导致本地缓存和二级缓存被清空，默认值：`false`。
		- 我这边还做了一个实验，就是如果在一个`SqlSession`中对先查询了记录A，然后在后续的逻辑中修改了记录A，然后我第二次再次查询记录A的时候发现去数据库查了。也就是说，Mybatis中你对这条记录做了修改，他就会将上一次记录的一级缓存给删除了。
	- 参考文章： [mybatis的缓存机制（一级缓存二级缓存和刷新缓存）和mybatis整合ehcache](https://blog.csdn.net/u012373815/article/details/47069223)
- tinyint类型
  collapsed:: true
	- 在mybatis generator项目中，tinyint类型字段的实体映射逻辑：
		- 若数据库定义字段为`tinyint(1)` ，映射之后的Java类型为`Boolean`
		- 若数据库定义字段为`tinyint(2)`，映射之后的Java类型为`Byte`
		- 若数据库定义字段为`tinyint(4)`，映射之后的Java类型也为`Byte`
- sum()函数
  collapsed:: true
	- `sum()`函数可能会返回null值，故在MyBatis查询中应该设置resultType为integer类型，不能是int。查询完成之后，还需要判断该值是否为null，从而避免代码出现空指针。