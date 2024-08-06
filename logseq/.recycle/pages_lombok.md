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
  collapsed:: true
	- 参考文章：[log4j2+slf4j+lombok整合](https://blog.csdn.net/m0_57099067/article/details/125303294)
- 参考文章
  collapsed:: true
	- [Lombok@Builder注解使用和需要注意的坑](https://blog.csdn.net/a648119398/article/details/120513865)
	- [@Data注解 与 lombok](https://www.jianshu.com/p/c1ee7e4247bf)