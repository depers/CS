- Java语言
	- Java基础
	  collapsed:: true
		- 语言基础
		  collapsed:: true
			- 数据类型
			  collapsed:: true
				- 基本类型
					- 整型
						- byte，1个字节
						- short，2个字节
						- int，4个字节
						- long，8个字节
					- 浮点型
						- float，4个字节
						- double，8个字节
					- 布尔类型：boolean，这种数据类型表示一位信息，但它的“大小”并没有得到精确的定义。
					- 字符类型：char，2个字节，字符类型char表示一个字符。Java的char类型除了可表示标准的ASCII外，还可以表示一个Unicode字符：
					- 其他：引用类型（所有class和interface类型）
				- 包装类型
					- 基本类型都对应一个包装类型
						- Java核心库提供的包装类型可以把基本类型包装为class；
						- 自动装箱和自动拆箱都是在编译期完成的（JDK>=1.5）；
						- 装箱和拆箱会影响执行效率，且拆箱时可能发生NullPointerException；
						- 包装类型的比较必须使用equals()，枚举类型可以除外
						- 整数和浮点数的包装类型都继承自Number；
						- 包装类型提供了大量实用方法；
						- 所有的包装类型都是不变类；
					- 基本数据类型和其包装类的对应关系
						- byte-Byte
						- short-Short
						- int-Integer
						- long-Long
						- float-Float
						- double-Double
						- boolean-Boolean
						- char-Character
					- 自动装箱与拆箱
					- 进制转换
						- 十进制：Integer.toString
						- 十六进制：Integer.toHexString
						- 八进制：Integer.toOctalString
						- 二进制：Integer.toBinaryString
					- 处理无符号整型
						- Java并没有无符号整型（Unsigned）的基本数据类型
						- byte、short、int和long都是带符号整型，最高位是符号位
						- Byte.toUnsignedInt
				- Java中的具体类型
					- 原始数据类型，例如int，float
					- 非泛型的类和接口，例如 String 或 Random
					- 所有类型都是无界通配符的泛型类型，例如 Set<?> 或 Map<?, ?>
					- 集合类型，例如 List或 HashMap
					- 可具体化类型的数组，如 String[]、List[] 或 Map<?, ?>[]
				- 缓存池
			- 字符串
			  collapsed:: true
				- String的三种主要的声明方式
					- 方式一：直接使用双引号声明出来的`String`对象会直接存储在**常量池**中，这个对象指向的是常量池中的String对象。
					- 方式二：如果不是用双引号声明的`String`对象，可以使用`String`提供的`intern`方法。intern 方法会从字符串常量池中查询当前字符串是否存在，若不存在就会将当前字符串放入常量池中。
					- 方式三：`String s = new String("abc")`创建了2个对象，第一个对象是”abc”字符串存储在常量池中，第二个对象在JAVA Heap中的 String 对象。s指向的是Java堆上的对象。
				- 基本操作
					- 比较：必须使用equals()
					- 是否包含：contains()
					- 去除首尾空格
					  collapsed:: true
						- tirm()：空白字符包括空格，\t，\r，\n和空格
						- strip()：去除\u3000
					- 提取子串：substring()
					- 删除索引位置的字符：deleteCharAt()
					- 字符串替换：replace()
					- 分割字符串：split()
					- 按分隔符拼接字符串：join()
					- 拼接字符串：concat()
					- 格式化字符串
					  collapsed:: true
						- formatted()
						- format()
						- 占位符
							- %s：显示字符串；
							- %d：显示整数；
							- %x：显示十六进制整数；
							- %f：显示浮点数；
								- String.format("value is %f", 32.33434)，显示浮点数
								- String.format("value is %32.12f", 32.33434)，显示小数点后显示12位，不够填充0，整体显示位32位，不够的地方补充空格
							- %c：显示Unicode字符；
					- 类型转换
					- 转换为char数组
					  collapsed:: true
						- char[] cs = "Hello".toCharArray(); // String -> char[]
						- String s = new String(cs); // char[] -> String
							- s不会直接引用char[]，而是复制
							- 如果修改了char[]，并不会影响s
					- 返回字符串索引下表字母的ascII十进制码值：codePointAt()
				- 编码
					- 字符编码笔记：ASCII，Unicode 和 UTF-8
					- 将字符串转为字节数组：byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
					- 将已知编码的字节数组转为字符串：String s2 = new String(b, StandardCharsets.UTF_8); // 按UTF-8转换
				- 不可变
					- 概述
						- 在 Java 8 中，String 内部使用 char 数组存储数据
						- 在 Java 9 之后，String 类的实现改用 byte 数组存储字符串，同时使用 coder 来标识使用了哪种编码
						- 不可变特性可以参考：https://www.liaoxuefeng.com/wiki/1252599548343744/1255938912141568
					- 不可变的好处
						- 可以缓存 hash 值
						- String Pool的需要
						- 安全性
						- 线程安全
				- Sting-StringBuffer-StringBuilder的比较
				  collapsed:: true
					- 可变性
						- String不可变
						- StringBuffer和StringBuilder可变
					- 线程安全
						- String不可变，是线程安全的
						- StringBuilder 不是线程安全的
						- StringBuffer 是线程安全的，内部使用 synchronized 进行同步
				- String.intern()
				  id:: 64043de8-605f-43aa-a7b0-a711a39e4d4a
					- 作用：如果字符串常量池中已经包含一个等于此String对象的字符串，则返回池中这个字符串的**String对象**；否则，将此String对象包含的字符串添加到常量池中，并且返回此**String对象**。
					- JDK6中，常量池和堆是不同的内存区域，所以使用`new String("a")`是分别创建了两个不同的对象。
					- JDK7新的变化
						- 将String常量池 从 Perm 区移动到了 Java Heap区
						- 涉及到从常量池获取对象的时候，若这个对象在堆上已经存在，则不再常量池创建新的对象，而是返回堆上已经存在对象的引用地址。
					- 可以保证相同内容的字符串变量引用同一的内存对象。
					- String Pool
				- new String("abc")
			- 运算
			  collapsed:: true
				- 参数传递
					- Java的参数传递是：值传递，
					- 对于基本类型（原始类型），在参数传递中是值传递
					- 对于引用类型，本质上是将对象的地址以值的方式传递到形参中，修改信息的是同一个对象。
					- 如果在方法中重置了对象的引用，则修改信息的是不同的对象。
					- 参考文章
						- [这一次，彻底解决Java的值传递和引用传递](https://segmentfault.com/a/1190000016773324)
				- 整数运算
				  collapsed:: true
					- 整数类型：byte, short, int, long
					- 溢出：整数由于存在范围限制，如果计算结果超出了范围，就会产生溢出
					- 加减乘除
						- `+`/`+=`
						- `-`/`-=`
						- `*`/`*=`
						- `/`/`/=`
					- 自增/自减
						- `++`
						- `--`
						- 不建议把上面的运算符写到变量前面
					- 移位运算
						- `<<`，左移相当于乘2
						- `>>`，右移相当于除2
						- `>>>`，无符号右移，也相当于除2，与右移运算符不同的是
					- 位运算
					  collapsed:: true
						- `&`，与预算
						- `|`，或运算
						- `~`，非运算
						- `^`，异或运算
					- 逻辑运算符
					  collapsed:: true
						- `&&`优先级高于`||`
					- [运算优先级](https://www.liaoxuefeng.com/wiki/1252599548343744/1255888634635520)
					- 类型转换
						- [隐式类型转换：++和+=](http://www.cyc2018.xyz/Java/Java%20%E5%9F%BA%E7%A1%80.html#%E9%9A%90%E5%BC%8F%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2)
						- 参与运算的两个数类型不一致，那么计算结果为较大类型的整型
						- 大范围的整数转型为小范围的整数。强制转型使用(类型)。强转的结果可能是错的。
				- 浮点数运算
				  collapsed:: true
					- float与double
						- // float f = 1.1; 是错的，Java 不能隐式执行向下转型，因为这会使得精度降低。
						- 1.1f 字面量才是 float 类型
						- 1.1 字面量属于 double 类型
					- 特点
						- 不能做位运算和移位运算
						- 浮点数的运算常常存在误差
					- 类型提升：一个浮点数和一个整数的运算，整型可以自动提升到浮点型
					- 溢出：浮点数除0时不会报错，会返回特殊值
						- NaN表示Not a Number
						- Infinity表示无穷大
						- -Infinity表示负无穷大
					- 强制转型（将浮点型转为整型）
						- 浮点数的小数部分会被丢掉
						- 四舍五入需要加0.5
						- 如果转型后超过了整型能表示的最大范围，将返回整型的最大值
				- 布尔运算
				  collapsed:: true
					- 短路运算：如果一个布尔运算的表达式能提前确定结果，则后续的计算不再执行，直接返回结果
					- 三元运算符：b ? x : y
				- 运算符
				  collapsed:: true
					- 逻辑运算符
					  collapsed:: true
						- 与：`&&`
						- 或：`||`
						- 非：`!`
					- 算术运算符
					  collapsed:: true
						- 加：`+`/`+=`/`++`
						- 减：`-`/`-=`/`--`
						- 乘：`*`/`*=`
						- 除：`/`/`/=`
					- 移位运算符
					  collapsed:: true
						- `<<`
							- 运算规则：**左移位会丢弃左边指定位数，右边补0**。
							- 左移位操作，相当于乘2。
							- int类型左移位数大于等于32位操作时，会先求余（%）后再进行左移操作。例如左移40位相当于左移8位（40%32=8）。
							- long类型左移位数大于等于64位操作时，会先求余（%）后再进行右移操作。例如左移70位相当于左移6位（70%64=6）。
							- double，float在二进制中的表现比较特殊，因此不能进行位移操作。
							- 整型byte，short移位前会先转换为int类型（32位）再进行移位。
						- `>>`
							- 运算规则：**丢弃右边指定位数，左边补上符号位**。符号位0代表的是正数，1代表的是负数。正数右移左侧补0，负数右移左侧补1。
							- 右移位操作，相当于除2。
							- 和左移一样，int类型移位大于等于32位时，long类型大于等于64位时，会先做求余处理再位移处理，byte，short移位前会先转换为int类型（32位）再进行移位。
						- `>>>`
							- 运算规则：**丢弃右边指定位数，左边补上0**。
							- 对于正数移位来说等同于：`>>`，负数通过此移位运算符能移位成正数。
						- 参考文章
							- [Java中的移位运算符](https://zhuanlan.zhihu.com/p/30108890)
					- 其他运算符
			- 流程控制
			  collapsed:: true
				- 输入和输出
				  collapsed:: true
					- 输出
						- System.out.println()，输出并换行
						- System.out.print()，输出不换行
						- System.out.printf()，格式化输出
					- 格式化输出：
						- printf()
						- 占位符%?
					- 输入：
						- Scanner scanner = new Scanner(System.in);
						- scanner.nextLine()/nextInt()...
				- if判断
				  collapsed:: true
					- if
					- if...else
					- if...else if...else
				- switch多重选择
				  collapsed:: true
					- 基础语法：switch(value){...case v1: ...break...default...}
					- switch的计算结果必须是整型、字符串或枚举类型；
					- switch的case语句后面可以放多个判断条件，类似：case 1, 2:
					- Java12：switch(value)...{case v1 ->...default}，不用写break
					- Java13 yield语法：我们可以从内部返回一个值
					- Java14：switch语句正式升级为表达式，不再需要break
				- while循环
				  collapsed:: true
					- while循环先判断循环条件是否满足，再执行循环语句；
					- while循环可能一次都不执行；
					- 编写循环时要注意循环条件，并避免死循环；
				- do while循环
				  collapsed:: true
					- do while循环先执行循环，再判断条件；
					- do while循环会至少执行一次；
				- for循环
				  collapsed:: true
					- for循环通过计数器可以实现复杂循环；
					- for each循环可以直接遍历数组的每个元素；
					- 最佳实践：计数器变量定义在for循环内部（初始化值，结束条件，更新语句），循环体内部（就是你要循环执行的代码）不修改计数器；
				- break和continue
				  collapsed:: true
					- 相同点
						- 都用于while循环和for循环
						- 都通常配合if使用
					- 不同点
						- break总是跳出最近的一层循环，而continue语句可以提前结束本次循环
			- 数组操作
			  collapsed:: true
				- 初始化数组
					- int[] a = new int[5]; int类型数组初始化之后是0
					- int[] b = {1, 2, 3, 4, 5};
				- 数组操作
					- 遍历数组
						- for
						- for each
						- 打印数组：Arrays.toString()
					- 数组排序
						- 使用Arrays.sort()进行排序
					- 多维数组
						- 二维数组就是数组的数组，三维数组就是二维数组的数组；
						- 多维数组的每个数组元素（每行数组）长度都不要求相同；
						- 打印多维数组可以使用Arrays.deepToString()；
						- 二位数组的长度是行数；
						- 最常见的多维数组是二维数组，访问二维数组的一个元素使用array[row][col]。
					- 命令行参数
						- main方法的args字符串数组
						- $ javac Main.java
						- $ java Main -version
				- System.arraycopy
					- 参考博客：https://www.geeksforgeeks.org/system-arraycopy-in-java/
			- 关键字final和static
			  collapsed:: true
				- final
					- 修饰类
						- 如果一个在声明类时用final关键字来修饰，那这个类是不能够被继承的。也就是说这个类时最终的。例如String类。
						- 类声明中的 final 关键字并不意味着该类的对象是不可变的。我们可以自由改变类对象的字段：
					- 修饰方法
						- 子类是无法重写基类的private的方法的，private隐式的被指定为final。
						- 被final修饰的方法，是无法被子类覆盖的。
						- 如果我们类的某些方法被其他方法调用，我们应该考虑将被调用的方法设为final。否则，覆盖它们会影响调用者的工作并导致令人惊讶的结果。
						- 将类的所有方法设为最终方法与将类本身标记为最终方法有什么区别？
							- 在第一种情况下，我们可以扩展类并向其添加新方法。
							- 在第二种情况下，我们不能扩展。
					- 修饰变量
						- 标记为 final 的变量不能重新分配。 一旦最终变量被初始化，它就不能被改变。
						- 修饰原始类型变量
						- 修饰引用变量
						- 修饰字段
							- 修饰原始类型变量
							- 修饰引用类型变量
							- 修饰类字段（类的属性）
								- 声明常量
									- 根据命名约定，类常量应为大写，组件之间用下划线 (“_”) 字符分隔
								- 必须在构造函数完成之前初始化任何 final 字段
									- static final修饰的类字段的初始化时机
										- 在声明的时候初始化该字段
										- 在静态代码块中初始化该字段
									- final修饰的类字段的初始化时机
										- 在声明的时候初始化该字段
										- 在实例初始化代码块中初始化该字段
										- 在构造函数中初始化该字段
					- 参考实现：JavaTrain/src/main/java/cn/bravedawn/basic/keyword/final_
				- static
					- 静态变量
					- 静态方法
						- 只能访问所属类的静态字段和静态方法，方法中不能有 this 和 super 关键字，因为这两个关键字与具体对象关联。
					- 静态语句块
					- 静态内部类
					- 静态导包
					- 实例化顺序
			- 日期与时间
			  collapsed:: true
				- 基本概念
					- 时区
					- 本地化Locale
				- Date和Calendar
					- 时间戳：System.currentTimeMillis()
					- 标准API
						- 旧的：java.util，主要包括Date、Calendar和TimeZone这几个类；
						- 新的：java.time，主要包括LocalDateTime、ZonedDateTime、ZoneId等；
					- 格式化时间
						- yyyy：年
						- MM：月
						- dd：日
						- HH：小时（24小时制）
						- hh：小时（12小时制）
						- mm：分钟
						- ss：秒
						- sss：毫秒
					- Date
					- SimpleDateFormat
						- 不是线程安全
					- Calendar
						- 利用Calendar.getTime()可以将一个Calendar对象转换成Date对象
						- 相比于Date
							- 多了做简单的日期和时间运算的功能
							- 提供了时区转换的功能
				- Java8新的时间API体系
					- 本地日期和时间
						- LocalDateTime
							- 它表示一个本地日期和时间
							- 按照ISO 8601格式打印
							- 可以转换为LocalDate和LocalTime
							- of方法创建指定的日期和时间
							- 字符串解析为日期和时间
							- 加减运算
							- 日期和时间的修改
							- with方法进行更复杂的运算
							- 判断时间的先后
							- LocalDateTime无法与时间戳进行转换，因为LocalDateTime没有时区，无法确定某一时刻
						- LocalDate
							- 它表示一个本地日期
						- LocalTime
							- 它表示一个本地时间
					- 带时区的日期和时间
						- ZonedDateTime
							- 创建
							- 时区转换
							- 转换为LocalDateTime
					- 时刻
						- Instant
					- 时区
						- ZoneId
						- ZoneOffset
					- 时间间隔
						- Duration：表示两个时刻之间的时间间隔
						- Period：表示两个日期之间的天数
					- 时间格式类
						- DateTimeFormatter
							- 线程安全
							- 创建
							- 格式化输出
					- 互转关系
						- LocalDateTime和ZoneId可以转换为ZonedDateTime
						- ZonedDateTime可以转为LocalDateTime，丢失时区信息
						- ZonedDateTime可以转化为Instant和long
						- Instant和long也可以转换为ZonedDateTime
				- 最佳实践
					- 旧API转新API
					- 新API转旧API
					- 数据库中采用长整型存储时间
			- 正则表达式
			  collapsed:: true
				- 功能：正则表达式是用字符串描述的一个匹配规则，使用正则表达式可以快速判断给定的字符串是否符合匹配规则。Java标准库java.util.regex内建了正则表达式引擎。
				- 匹配规则
					- 匹配任意字符：.匹配一个字符且仅限一个任意字符
					- 匹配数字：\d仅限单个数字字符
					- 匹配常用字符：\w可以匹配一个字母、数字或下划线
					- 匹配空格字符：\s可以匹配一个空格字符，注意空格字符不但包括空格，还包括tab字符（在Java中用\t表示）
					- 匹配非数字：\D则匹配一个非数字
					- 重复匹配
						- 修饰符*可以匹配任意个字符，包括0个字符
						- 修饰符+可以匹配至少一个字符
						- 修饰符?可以匹配0个或一个字符
				- 匹配复杂规则
					- 匹配开头和结尾
					- 匹配指定范围
					- 或规则匹配
					- 使用括号
						- 提取公共部分，括起子规则
						- 分组匹配
				- 使用Pattern只做一次编译，不建议使用String.matches()
				- 非贪婪匹配?
				- 搜索和替换
					- 分割字符串：String.split()
					- 搜索字符串：Matcher.find()
					- 替换字符串：String.replaceAll()
					- 反向引用
					- Matcher.appendReplacement()
			- 枚举
			  collapsed:: true
				- 背景：定义的普通常量类，编译器无法检查每个值的合理性
				- 枚举的比较：相比equals方法，建议使用==
				- 枚举的实例方法
					- name()
					- 空笔记
				- 枚举的switch
			- 随机数
			  collapsed:: true
				- 为什么说我们生成的随机数是伪随机的？
				  collapsed:: true
					- 随机数生成器是一个函数y=f(x)，而随机种子则是变量x。所以一旦x和f(x)确定了，那么产生的随机数y也就确定。“伪随机”正是通过，在随机数生成器中传入的随机种子得到结果产生随机数。之所以为“伪随机”，是因为能够出现的结果以及次序其实已经在随机数生成器这个函数中确定了，如果f(x)一定，而程序通过输入x的变化，而产生不同结果，达到随机的效果。“伪”指的是有规律，而不是“假”。
				- 使用Java API
				  collapsed:: true
					- 使用Math.random()生成随机数
					  collapsed:: true
						- Math 类的 random 方法将返回一个范围从 0.0（包括）到 1.0（不包括）的 double 值
					- 使用Random.next()生成随机数
						- nextInt(n)，生成一个在0(包括)到n(不包括)之间的一个数，带参数的方法中，n必须大于0，否则就会报IllegalArgumentException
						- 使用无参的nextInt方法可以获取任何随机数，经常会拿到负数
						- 使用有参的nextInt方法，可以得到一个范围内的数字
						- 为Random设置相同的种子之后，每次生成的都是相同的随机数。
					- 使用ThreadLocalRandom生成随机数
						- ThreadLocalRandom类与Random类有三个重要区别
							- 1. 不需要显式地初始化ThreadLocalRandom的一个新实例。这有助于我们避免创建大量无用的实例和浪费垃圾回收器时间的情况。
							- 2. 不能为ThreadLocalRandom设置种子。
							- 3. Random类在多线程环境中表现不好。
					- 使用SplittableRandom生成随机数
						- Java8新的快速生成器，用于并行计算的生成器。重要的是要知道实例不是线程安全的
						- 提供了ints()方法，返回IntStream
					- 使用SecureRandom生成随机数
						- 安全敏感的应用程序，我们应该考虑使用SecureRandom。这是一个密码学上的强生成器
				- 使用三方API
				  collapsed:: true
					- 使用Apache Common Math3生成随机数
						- 在Apache commons项目的公共数学库中提供了很多生成器，RandomDataGenerator使用Well19937c算法进行随机数的生成。
					- 使用XoRoShiRo128PlusRandom生成随机数
						- 最快的随机数生成器实现之一，它是由米兰大学信息科学系开发的。
				- 参考文章
				  collapsed:: true
					- Generating Random Numbers in Java
			- JSON
			  collapsed:: true
				- jackson
					- 将一个对象转换为json字符串
						- 参考文章
							- [How to convert Java object to / from JSON (Jackson)](https://mkyong.com/java/how-to-convert-java-object-to-from-json-jackson/)
		- 面向对象
		  collapsed:: true
			- Object通用方法
			  collapsed:: true
				- equals
				  collapsed:: true
					- Java SE中针对equals()的原则
					  collapsed:: true
						- 自反性（Reflexive）：对于非null的x来说，x.equals(x)必须返回true；
						- 对称性（Symmetric）：对于非null的x和y来说，如果x.equals(y)为true，则y.equals(x)也必须为true；
						- 传递性（Transitive）：对于非null的x、y和z来说，如果x.equals(y)为true，y.equals(z)也为true，那么x.equals(z)也必须为true；
						- 一致性（Consistent）：对于非null的x和y来说，只要x和y状态不变，则x.equals(y)总是一致地返回true或者false；
						- 对null的比较：x.equals(null)永远返回false
					- 手动编写equals的步骤（可参考：JavaTrain：cn.bravedawn.obj.object.EqualsExample#equals）
					  collapsed:: true
						- 第一步：先确定实例“相等”的逻辑，即哪些字段相等，就认为实例相等；
						- 第二步：用instanceof判断传入的待比较的Object是不是当前类型，如果是，继续比较，否则，返回false；
						- 第三步：对引用类型用Objects.equals()比较，对基本类型直接用==比较；
					- 对于实体类
					  collapsed:: true
						- 对于整型包装类型，在-128到127之间的比较都用到了缓存池，这里的equals()和==的作用是一样的。超过这个范围的值比较要使用equals()方法，不能使用==
						- 对于浮点型包装类型，值的比较使用equals()，不能使用==
						- 对于字符型包装类型，equals()和==的作用是一样的
						- 对于布尔型包装类型，equals()和==的作用是一样的
					- 继承违反equals()的对称性
					  collapsed:: true
						- 实现：子类继承父类，翻写子类的equals()方法，具体可以参考：cn.bravedawn.obj.object.equalsandhashcode.equals.WrongVoucher
						- 使用组合修复equals()的对称性：其实是治标不治本，具体实现可参考：cn.bravedawn.obj.object.equalsandhashcode.equals.Voucher
					- 使用场景
					  collapsed:: true
						- 如果不调用List的contains()、indexOf()这些方法，那么放入的元素就不需要实现equals()方法
						- 对于实体类，像基本类型的包装类型或是String类，通常使用默认的equals()实现就可以。但是对于有自身属性的值对象，我们就需要手动实现equals()方法
					- 辅助工具
					  collapsed:: true
						- IDE生成
						- Apache Commons Lang
						- Google Guava
						- Project Lombok
					- 总结
					  collapsed:: true
						- 对于基本数据类型的包装类型，值的比较建议使用equals，不要使用==
						- 对于基本类型，== 判断两个值是否相等，基本类型没有equals()方法
						- 对于引用类型，== 判断两个变量是否引用同一个对象（对象引用的地址），而 equals()判断引用的对象是否等价
						- 若一个对象没有覆写equals()方法，则equals()方法的默认实现是通过==比较内存地址实现的
					- 参考文章
					  collapsed:: true
						- 廖雪峰-编写equals方法
						- Java equals() and hashCode() Contracts
					- 参考实现：JavaTrain/src/main/java/cn/bravedawn/obj/object/equalsandhashcode/equals
				- hashCode
				  collapsed:: true
					- 一般原则
					  collapsed:: true
						- 内部一致性：hashCode() 的值可能仅在 equals() 中的属性更改时才会更改
						- 等于一致性：彼此相等的对象必须返回相同的hashCode()，也就是说调用equals方法的两个对象相等，调用hashCode()产生的整数结果也相同。
						- 冲突：不相等的对象可能具有相同的 hashCode()
					- 注意
					  collapsed:: true
						- hashCode() 返回哈希值，而 equals() 是用来判断两个对象是否等价。等价的两个对象散列值一定相同，但是散列值相同的两个对象不一定等价
						- 在覆盖 equals() 方法时应当总是覆盖 hashCode()方法，保证等价的两个对象哈希值也相等。否则基于hashCode定位的HashMap就无法正常工作
				- toString
				  collapsed:: true
					- 一个自定义的类如果不覆写toString方法的话，默认返回类名+@+散列值的十六进制表示
				- clone
				  collapsed:: true
					- 方法实现：实现Cloneable接口，重写clone方法（clone() 是 Object 的 protected 方法，它不是 public）
					- 对象拷贝
					  collapsed:: true
						- 浅拷贝
						  collapsed:: true
							- 拷贝对象和原始对象的属性的引用类型引用的是同一个对象
							- 特点
							  collapsed:: true
								- 主对象的内存地址不同，是不同对象。属性对象的内存地址相同，是同一对象。
								- 浅拷贝只复制“主”对象，但不会复制“主”对象的里面的对象（属性），”里面的对象“会在原来的对象和它的副本之间共享。
						- 深拷贝
						  collapsed:: true
							- 拷贝对象和原始对象的属性的引用类型引用是不同对象
							- 特点
							  collapsed:: true
								- 主对象的属性对象内存地址不同，都是不同对象。
								- 深拷贝是一个整个独立的对象拷贝，深拷贝会拷贝所有的属性,并拷贝属性指向的动态分配的内存。当对象和它所引用的对象一起拷贝时即发生深拷贝。深拷贝相比于浅拷贝速度较慢并且花销较大。
							- 方法
							  collapsed:: true
								- 1. 构造函数
								  2. 覆写clone方法
								  3. Serializable序列化
								  4. Json序列化
					- 引用拷贝
					  collapsed:: true
						- 创建一个指向对象的引用变量的拷贝。指两个不同的引用变量指向同一个对象实例，即他们指向的是同一个相同的引用地址，也就是同一个对象。
						- 特点：
						  collapsed:: true
							- 对象的内存地址一样，同一个对象
					- 最佳实践
					  collapsed:: true
						- 最好不要去使用 clone()，可以使用拷贝构造函数或者拷贝工厂来拷贝一个对象
						- 使用 clone() 方法来拷贝一个对象即复杂又有风险，它会抛出异常，并且还需要类型转换
					- 参考文章
					  collapsed:: true
						- [Java深入理解深拷贝和浅拷贝区别](https://blog.csdn.net/riemann_/article/details/87217229)
				- Object.equals()的逻辑
				  collapsed:: true
					- 先判断两个对象是否相等，若是返回true，否则false；若两个参数都为null也返回true；
					- 若第一个参数不为null，则调用他的equals方法进行判断；
			- 面向对象
				- 类和接口的定义
				  collapsed:: true
					- 类：类是用户定义的蓝图或原型，可以从中创建对象。它表示对同一类型的所有对象通用的属性或方法的集合。
					- 接口：像类一样，接口可以有方法和变量，但是在接口中声明的方法默认是抽象的(只有方法签名，没有主体)。接口指定类必须做什么，而不是如何做。它是类的蓝图
				- 类的字段类型的默认值
				  collapsed:: true
					- 基本类型
					  collapsed:: true
						- boolean：false
						- byte：0
						- short：0
						- int：0
						- long：0
						- float：0.0
						- double：0.0
						- char：nul（Assic码表对应十进制0）
					- 引用类型
					  collapsed:: true
						- Boolean：null
						- Byte：null
						- Short：null
						- Integer：null
						- Long：null
						- Float：null
						- Double：null
						- Char：null
				- 访问权限
				  collapsed:: true
					- 定义
					  collapsed:: true
						- Java中，可以使用访问修饰符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。
					- private
					  collapsed:: true
						- 在同一类内可见。使用对象：变量、方法、类（接口）。 注意：不能修饰类（外部类）
						- 定义private方法的理由是内部方法是可以调用private方法的
					- default
					  collapsed:: true
						- (即缺省）: 在同一包内可见，不使用任何修饰符。使用对象：类（接口）、变量、方法。
					- protected
					  collapsed:: true
						- 对同一包内的类和所有子类可见。使用对象：类（接口）、变量、方法。 注意：不能修饰类（外部类）
					- public
					  collapsed:: true
						- 对所有类可见。使用对象：类（接口）、变量、方法
						- 一个.java文件只能包含一个public类，但可以包含多个非public类。
					- 权限访问图
					  collapsed:: true
						-
				- 方法
				  collapsed:: true
					- 定义方法
					  collapsed:: true
						- 方法参数
						  collapsed:: true
							- 传值引用
							  collapsed:: true
								- 判断值传递还是引用传递：函数中对传递的参数进行修改是否会影响原来的值，若影响则为引用传递；若不影响则为值传递。
								- 基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响
								- 引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象（其实是引用地址的传递）。双方任意一方对这个对象的修改，都会影响对方（因为指向同一个对象嘛）
							- 可变参数：[type]... names
						- 返回值
						- 访问权限
						- return语句
					- this关键字
					  collapsed:: true
						- 在方法内部，可以使用一个隐含的变量this，它始终指向当前实例.
						- 通过this.field就可以访问当前实例的字段和方法。
				- 构造方法
				  collapsed:: true
					- 若一个类没有定义构造方法，Java会为每个类自动创建默认的无参构造方法
					- 一旦定义构造方法，Java就不会再定义默认无参构造方法。若想保留需手动显式实现
					- 可以定义多个构造方法，编译器根据参数自动判断
					- 可以在一个构造方法内部调用另一个构造方法，便于代码复用，调用其他构造方法的语法是this(…)
					- 若子类没有定义无参构造函数，则实例化子类时，会默认调用父类的无参构造函数
				- 重载
				  collapsed:: true
					- 特点（定义）
						- （Overload）存在于同一个类中，指一个方法与已经存在的方法名称上相同，但是参数类型、个数、顺序至少有一个不同。返回类型可以相同也可以不同。
						- 每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。
						- 最常用的地方就是构造器的重载。
						- Java中不允许用户重载运算符。
					- Java中方法重载的三种方式
					  collapsed:: true
						- 更改参数的数量
						- 更改参数的数据类型
						- 改变方法参数的顺序
					- 类型升级
					  collapsed:: true
						- 如果重载的参数类型与方法实际传入的类型不一致怎么办？换句话说实参的数据类型与形参的数据类型不一样，Java如何去选择合适的重载方法？
						- Java将会进行类型转换，将实参的数据类型转换到更高一级的数据类型，从而去匹配合适的重载方法，如果没有匹配到就会报错。
						- 在类型升级的过程中，Java会自动将原始数据类型转为包装类型去类型转换匹配图中去寻找。
						- 类型转换匹配图，例如实参如果是Byte类型，但是形参没有Byte类型，Java就会去找是否有Short、Integer....的重载方法。
					- 返回值问题
					  collapsed:: true
						- 如果两个方法参数的参数类型、个数、顺序都相同。返回值不同，是无法通过编译的。
						- 如果两个方法参数的参数类型、个数、顺序至少有一个不同，返回值可以相同也可以不同。
					- 重载main方法
					  collapsed:: true
						- 在Java中main方法是可以重载的。
					- 重载（overload）和覆盖（override）的区别
					  collapsed:: true
						- 重载是关于同一个函数有不同的签名。覆盖是关于相同的功能，相同的签名，但通过继承连接的不同类。
						- 重载是编译时多态性的一个例子，而覆盖是运行时多态性的一个例子。
					- 重载的优点
					  collapsed:: true
						- 方法重载提高了程序的可读性和可重用性。
						- 方法重载降低了程序的复杂性。
						- 使用方法重载，程序员可以高效地执行任务。
						- 使用方法重载，可以使用稍微不同的参数和类型访问执行相关功能的方法。
						- 类的对象也可以使用构造函数以不同的方式初始化。
					- 将null作为实参传给重载方法
					  collapsed:: true
						- 不要直接将null作为实参直接传递给形参为包装类型的重载方法，否则会编译错误。
						- 将null赋值给明确数据类型的变量之后，再传递给重载方法，就是正常的。
					- 参考文章
					  collapsed:: true
						- Java 重写(Override)与重载(Overload)
						- Method Overloading in Java
					- 参考实现：JavaTrain/src/main/java/cn/bravedawn/obj/inherit/polymorphic/overloading
				- 继承
				  collapsed:: true
					- Java只允许一个class继承自一个类，因此，一个类有且仅有一个父类。只有Object特殊，它没有父类。
					- 里氏替换原则
					  collapsed:: true
						- 含义一：子类必须实现父类的抽象方法，但不得重写（覆盖）父类的非抽象（已实现）方法。否则：子类重写的父类的方法，导致相同的方法的实现不同，导致程序的逻辑发生了变化
						- 含义二：子类中可以增加自己特有的方法
						- 含义三：当子类的方法重载父类的方法时，方法的前置条件（即方法的输入/入参）要比父类方法的输入参数更宽松（大于）。（例如父类方法的入参为HashMap，则子类的入参应该为Map）
						- 含义四：当子类的方法实现父类的方法时（重写/重载或实现抽象方法），方法的后置条件（即方法的输出/返回值）要比父类更严格或相等（小于等于）。 （例如父类方法的返回值为Map，则子类的入参应该为Map或为HashMap）。否则： 若在继承时，子类的方法返回值类型范围比父类的方法返回值类型范围大，在子类重写该方法时编译器会报错
					- protected
					  collapsed:: true
						- protected关键字可以把字段和方法的访问权限控制在继承树内部，一个protected字段和方法可以被其子类，以及子类的子类所访问
					- super
					  collapsed:: true
						- 若父类定义了有参构造方法且没有显示定义无参构造方法，子类需显式的复写父类的构造方法，需要在子类的构造方法中通过super关键字显式的调用父类的构造方法
						- 若父类定义了无参构造方法，子类的无参构造方法中会默认调用父类的无参构造方法，而且会先调用父类的后调用子类的
					- 阻止继承
					  collapsed:: true
						- final
						- sealed
						- permits
						- non-sealed
					- 向上转型
					  collapsed:: true
						- 把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）
					- 向下转型
					  collapsed:: true
						- 把一个父类类型强制转型为子类类型，就是向下转型（downcasting）
						- 可以强制向下转型，最好借助instanceof判断
						- 这种是可以的：Person p1 = new Student;Student s1 = (Student) p1; // downcasting ok
					- instanceof
					  collapsed:: true
						- 作用
						  collapsed:: true
							- 判断一个变量所指向的实例是否是指定类型，或者这个类型的子类。
							- 用来测试对象是否属于给定类型的二元运算符。
							- 它也称为类型比较运算符，因为它将实例与类型进行比较。
						- 注意
						  collapsed:: true
							- 如果被比较的对象和它被比较的类型之间没有关系，则不能使用 `instanceof` 运算符。
							- 如果一个引用变量为`null`，那么对任何instanceof的判断都为`false`。
							- 在 Java 中，每个类都隐式继承自 Object 类。因此，使用带有 Object 类型的 instanceof 运算符将始终计算为 true。
							- 从技术上讲，我们只允许在 Java 中通过 instanceof 和Java中的具体类型一起使用。
						- Java 14 带来了新版的 instanceof操作，将参数类型检查和绑局部变量类型合并到了一起：obj instanceof String str
						- 参考文章：https://www.baeldung.com/java-instanceof
					- 区分继承和组合
					  collapsed:: true
						- 继承是is关系，组合是has关系
				- 多态
				  collapsed:: true
					- 多态
						- 多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法
						- 多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码
					- 覆写
						- 定义：在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写（Override）
						- 实际意义：如果子类覆写了父类的方法，子类的引用在实际调用这个方法的时候，调用的是子类的方法。
					- 实例初始化代码块
					  collapsed:: true
						- 实例初始化代码块（Instance Initializer block）用于初始化实例数据成员。每次创建类的对象时都会运行它。
						- 实例初始化代码块的执行顺序
						  collapsed:: true
							- 1. 先执行实例类的构造器中父类构造器（super()方法）
							- 2. 执行实例初始化代码块
							- 3. 执行实例类的构造器中的代码
							- 参考图
						- 参考文章
						  collapsed:: true
							- Instance initializer block
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/obj/inherit/polymorphic/instanceinitializerblock
				- 抽象类和接口
				  collapsed:: true
					- 抽象类
						- 背景：由于多态的存在，每个子类都可以覆写父类的方法。我们发现父类的方法其实并没有实际的意义，想要去掉方法的执行语句
						- 定义
							- 抽象方法用abstract修饰
							- 抽象方法所在的类必须是抽象类
							- 抽象类是无法实例化的。可以通过实现一个匿名内部类来实例化对象
						- 优势
							- 上层代码只定义规范
							- 通过抽象类Person类型去引用具体的子类实例
							- 具体的业务逻辑由不同的子类实现
					- 接口
						- 如果一个抽象类没有字段，所有方法全部都是抽象方法，就可以将该抽象类改写为接口
						- 特点
							- 一个类可以实现多个interface
							- 接口定义的所有方法默认都是public abstract的
							- 接口是无法实例化的。可以通过实现一个匿名内部类来实例化对象
							- 接口中是无法定义静态语句块的
						- 与抽象类的比较
						  collapsed:: true
							-
						- default
						  collapsed:: true
							- 在接口中可以有自己的方法实现，通过default方法（JDK>=1.8）
							- default方法的目的是：当我们需要给接口新增一个方法时，会涉及到修改全部子类。如果新增的是default方法，那么子类就不必全部修改，只需要在需要覆写的地方去覆写新增方法。
							- default方法和抽象类的普通方法的区别：因为interface没有字段，default方法无法访问字段，而抽象类的普通方法可以访问实例字段。
				- 包
				  collapsed:: true
					- import
					  collapsed:: true
						- 如果两个类在同一个包内，他俩之间的相互引用是不需要使用import关键字的
						- import static的语法：它可以导入可以导入一个类的静态字段和静态方法
					- Java内建的package机制是为了避免class命名冲突
					- JDK的核心类使用java.lang包，编译器会自动导入
					- JDK的其它常用类定义在java.util.，java.math.，java.text.*，……；
					- 包名推荐使用倒置的域名，例如org.apache
					- package-info.java
					  collapsed:: true
						- pacakge-info.java是一个Java文件，可以添加到任何的Java源码包中。pacakge-info.java的目标是提供一个包级的文档说明或者是包级的注释。
				- 内部类
				  collapsed:: true
					- 内部类
					  collapsed:: true
						- 可以用Outer.this引用Outer实例
						- 可以修改Outer Class的private字段
						- 可以访问Outer Class的private字段和方法
					- 匿名内部类
					  collapsed:: true
						- 通过实现一个接口或是抽象类来定义一个匿名内部类，从而实例化一个接口或是抽象类
						- 匿名类也完全可以继承自普通类
					- 静态内部类
					  collapsed:: true
						- 和内部类类似，但是使用static修饰
						- 不再依附于Outer的实例，而是一个完全独立的类，因此无法引用Outer.this
						- 可以访问Outer的private静态字段和静态方法
				- classpath和jar
				  collapsed:: true
					- classpath
					  collapsed:: true
						- JVM通过环境变量classpath决定搜索class的路径和顺序
						- 不推荐设置系统环境变量classpath，始终建议通过-cp命令传入，例如：java -cp . com.example.Hello
						  collapsed:: true
							- .指的是当前目录
							- -cp：执行类的代码
					- jar
					  collapsed:: true
						- jar包相当于目录，可以包含很多.class文件，方便下载和使用
						- jar包中的/META-INF/MANIFEST.MF文件，MANIFEST.MF是纯文本，可以指定Main-Class和其它信息。如果存在Main-Class，我们就不必在命令行中指定启动的类名了。
					- 运行一个java程序
					  collapsed:: true
						- 使用命令：java -cp E:\code\mall\JavaTrain\target\javatrain.jar cn.bravedawn.obj.inherit.innerclass.anonymousclass.Test
				- 模块
				  collapsed:: true
					- 背景
					  collapsed:: true
						- jar文件就是class文件的容器，但是jar只是用于存放class的容器，它并不关心class之间的依赖。如果我们编写了一个jar，它还引用了多个jar的代码，如果我们要执行这个jar：java -cp app.jar:a.jar:b.jar:c.jar cn.bravedawn.sample.Main，这里我们要写一堆的三方包。如果漏写了某个运行时需要用到的jar，那么在运行期极有可能抛出ClassNotFoundException。
						- Java 9开始引入的模块，主要是为了解决“依赖”这个问题。让程序在编译和运行的时候能自动定位到b.jar，这种自带“依赖关系”的class容器就是模块。
					- 模块路径
					  collapsed:: true
						- 模块系统使用 **模块路径** 来查找在不同的模块工件（module artifact）中定义的模块。
						- 在不同的阶段可以使用不同类型的模块路径，如下表所示。在使用`javac`编译时，表中的4个模块路径都可以适用。模块系统会首先检查`--module-source-path`指定的模块路径，其次`--upgrade-module-path`，接着是`--system`，最后是`--module-path`或`-p`。
						  :LOGBOOK:
						  CLOCK: [2023-01-09 Mon 21:34:09]--[2023-01-09 Mon 21:34:09] =>  00:00:00
						  :END:
						  ![模块路径.jpeg](../assets/模块路径_1673271258276_0.jpeg)
						- 模块路径使用操作系统上路径分隔符来进行分隔：Windows上是分号（`;`），macOS和Linux上是冒号（`:`）。
					- 模块的类型
					  collapsed:: true
						- 具名模块（Named Module）
						  collapsed:: true
							- 具名模块也称为应用模块（Application Module），通常在模块根目录下有module-info.java文件的话，那么这个模块就称为**具名模块**。
						- 无名模块（Unnamed Module）
						  collapsed:: true
							- **无名模块**指的就是不包含module-info.java的jar包，通常这些jar包都是java9之前构建的。值得注意的是：
							  collapsed:: true
								- 无名模块可以读取到其他所有的模块，并且会将自己包下的所有类都暴露给外界。
								- 具名模块不能读取无名模块，因为具名模块无法在module-info.java中声明对无名模块的依赖。
								- 无名模块导出所有包的目的在于让其他无名模块可以加载这些类。
						- 自动模块（Automatic Module）
						  collapsed:: true
							- 任何无名模块放到模块路径（module path）上会自动变为**自动模块**。
					- 编写模块
					  collapsed:: true
						- 编译：javac -d bin .\src\module-info.java .\src\cn\bravedawn*.java
						  collapsed:: true
							- -d：指定放置生成的类文件的位置
							- 用法: javac <options> <source files>
						- 生成jar包：jar –create –file hello.jar –main-class cn.bravedawn.Main -C bin .
						  collapsed:: true
							- –create(-c)：创建新jar
							- –file(-f)：指定jar包命名
							- –main-class(-e)：为捆绑到可执行 jar 文件的独立应用程序指定应用程序入口点，换句话说就是为可执行jar指定启动类
							- -C 目录 .：更改为指定的目录并包含其中的文件(可以理解为首先cd到指定目录，然后将目录的所有文件归档到jar包中)
							- 执行完上述命令打出jar文件其实是可以直接运行的，使用：java -jar hello.jar
						- 创建模块（将jar包转换成模块）：jmod create –class-path .\hello.jar hello.jmod
						- 运行模块：java –module-path .\hello.jar –module opp.module
						  collapsed:: true
							- –module-path：一个;目录分开的列表，每个目录都是一个目录的模块。指的是运行模块jar的目录
							- –module：指定模块名
					- 模块描述符
					  collapsed:: true
						- 作用
						  collapsed:: true
							- 为了描述模块之间的关系，用于定义模块信息，类似于Maven中的pom文件，Java9称之为模块描述符。
							- 模块描述符是一个固定名称的java文件，所有的模块描述符文件名称固定位 **module-info.java**，其内部存在特定的结构。
						- 关键字
						  collapsed:: true
							- module: 用来定义一个模块，后面紧跟模块名称，在同一个模块路径下，模块名称不允许相同。
							- exports: 用来指定开放那个包作为API供外部调用，没有开放的api不允许被调用。
							- requires: 用来执行依赖的模块，依赖必须显示指定。
					- 打包JRE
					  collapsed:: true
						- 目的
						  collapsed:: true
							- 要分发我们自己的Java应用程序，只需要把这个jre目录打个包给对方发过去，对方直接运行上述命令即可，既不用下载安装JDK，也不用知道如何配置我们自己的模块，极大地方便了分发和部署。
						- 步骤
						  collapsed:: true
							- 打包生产一个完整的并且带有我们自己opp.module模块的JRE：jlink –module-path hello.jmod –add-modules java.base,java.xml,hello.world –output jre/
							- 运行jre：jre/bin/java –module opp.module
					- 访问权限
					  collapsed:: true
						- Java的class的四级访问权限在模块中并不适用，class的这些访问权限只在一个模块内有效。
						- A模块要想访问B模块的某个class，必要条件是B模块要明确地导出了可以访问的包。
					- 参考文章
					  collapsed:: true
						- [Java模块系统介绍](http://ypk1226.com/2019/10/16/java/java9-module/)
						- [使用JDK9提供的模块化系统，来定义自己的模块](https://blog.csdn.net/gybshen/article/details/116886776)
						- [Java平台模块系统（3）- JDK工具](https://zhuanlan.zhihu.com/p/97284537)
				- 序列化
				  id:: 641475d2-462e-43b7-a273-77ab40289cde
				  collapsed:: true
					- serialVersionUID
						- 定义为代表类定义的版本，在反序列化时，jvm会将字节流状态的类中的serialVersionUID与本地类中的serialVersionUID进行比较，如果相同，则进行序列化，不相同就抛InvalidClassException异常。
						- 在实现序列化接口的时候，我们一般显式的给serialVersionUID设置一个固定值。这样无论类后期增加成员变量还是删除成员变量，都不会发生错误。
						- 如果在实现Serializable接口的时候，没有显式指定一个固定值，java序列化机制是会自动生成一个serialVersionUID，这个自动值会受类名称、它所实现的接口、以及所有的共有的私有的和受保护的成员变量的影响。如果这些值改变，那么这个自动值也会改变。在反序列化时，便会出错。
		- 异常处理
		  collapsed:: true
			- 异常体系
			  collapsed:: true
				- 分类
					- 检查性异常：需强制捕获
					- 运行时异常：无需强制捕获
					- 错误：无需捕获的严重错误
				- 关键字
					- try： 用于监听
					- catch： 用于捕获异常
					- finally：finally语句块总是会被执行
					- throw：用于抛出异常
					- throws：用在方法签名中，用于声明该方法可能抛出的异常
			- 捕获异常
			  collapsed:: true
				- 多catch语句
					- catch的顺序非常重要：子类必须写在前面
					- 多个catch语句只有一个能被执行
				- finally语句
					- finally语句不是必须的，可写可不写
					- finally总是最后执行
					- finally是用来保证一些代码必须执行的
				- 捕获多种异常
					- 一个catch语句也可以匹配多个非继承关系的异常
					- 因为处理异常的逻辑想通过，可以用|合并到一起，像这样catch (IOException | NumberFormatException e)
			- 抛出异常
			  collapsed:: true
				- 调用printStackTrace()可以打印异常的传播栈，对于调试非常有用
				- 保存原始的Exception信息
					- A方法调用B方法，两个方法相继抛出异常，A方法的异常信息将会丢失，说明新的异常丢失了原始异常信息
					- 为了追踪到完整的异常栈，在构造异常的时候，把原始的Exception实例传进去，新的Exception就可以持有原始Exception信息
				- 屏蔽异常（抑制异常）
					- 定义：若在catch和finally中都抛出异常，原来在catch中的异常就会消失，因为只能抛出一个异常。没有被抛出的异常（catch中的异常），称为“被屏蔽”的异常（Suppressed Exception）
					- 保存输出屏蔽异常的方法
						- 方法一：将catch中的异常使用一个变量进行保存，然后在finally的异常中，使用e.addSuppressed(origin)方法添加到屏蔽异常的数组中
						- 方法二：try-with-resource代码块可以直接捕获屏蔽异常
			- 自定义异常
			  collapsed:: true
				- Java标准库定义的常用异常
				  collapsed:: true
					- Exception
						- RuntimeException
						  collapsed:: true
							- NullPointerException
							- IndexOutOfBoundsException
							- SecurityException
							- IllegalArgumentException：参数检查不合法，应该抛出
							  collapsed:: true
								- NumberFormatException：将字符串转为整型时就会报这个错
						- IOException
						  collapsed:: true
							- UnsupportedCharsetException
							- FileNotFoundException
							- SocketException
						- ParseException
						- GeneralSecurityException
						- SQLException
						- TimeoutException
				- 大型项目中定义异常的继承体系
					- 1. 定义一个BaseException作为根异常
					- 2. BaseException通常从RuntimeException派生
			- NullPointerException
			  collapsed:: true
				- 查看NullPointerException的详细信息，我们可以看到具体的对象是否为null，可以添加JVM参数开启该功能：-XX:+ShowCodeDetailsInExceptionMessages
			- 断言
			  collapsed:: true
				- assert的语法：assert x > 0 : "<提示话术>"; 这句代码的意思就是说，如果x > 0为false，就会抛出AssertionError，并终止执行
				- 断言会抛出AssertionError异常，导致程序结束退出
				- assert如果断言失败会抛出，JVM默认是会关闭断言指令，需要给Java虚拟机传递-enableassertions（可简写为-ea）参数启用断言
				- 对特定的类启用断言：-ea:com.itranswarp.sample.Main
				- 对特定的包启用断言：-ea:com.itranswarp.sample...，注意后面有三个.
				- 对可恢复的错误不能使用断言，而应该抛出异常；
			- 反射相关的异常
			  collapsed:: true
				- InvocationTargetException
				  collapsed:: true
					- 背景
					  collapsed:: true
						- 反射操作中，代理类通过反射调用目标类的方法时，目标类的方法可能抛出异常。反射可以调用各种目标方法，因此目标方法抛出的异常是多种多样无法确定的。这意味着反射操作可能抛出一个任意类型的异常。可以用 Throwable 去接收这个异常，但这无疑太过宽泛。
					- 作用
					  collapsed:: true
						- 解决通过反射调用目标方法时，统一对目标方法可能抛出来的异常进行封装，便使得反射操作中的异常更易管理。
						- 当反射操作的目标方法中出现异常时，都统一包装成一个必检异常 InvocationTargetException。InvocationTargetException内部的 target 属性则保存了原始的异常。
					- 特点
					  collapsed:: true
						- 来自 java.lang.reflect包
						- 是必检类型的异常
				- UndeclaredThrowableException
					- 特点
					  collapsed:: true
						- 来自 java.lang.reflect包
						- 是必检类型的异常
					- 作用
					  collapsed:: true
						- 在代理类中难免会在执行某些方法时抛出一些代理类和被代理类共同实现的接口或者被代理类方法中没有声明的必检异常。
						- 如果不抛出，则它是必检异常，必须抛出；如果抛出，则父接口或父类中没有声明该必检异常，不能抛出。
						- 必检异常会被包装为免检异常 UndeclaredThrowableException 后抛出。所以说 UndeclaredThrowableException 也是一个包装了其他异常的异常。
		- 加解密与安全
		  collapsed:: true
			- 编码算法
			  collapsed:: true
				- ASCII码
					- 美国制定了一套字符编码，对英语字符与二进制位之间的关系，做了统一规定。这被称为 ASCII 码
					- ASCII 码一共规定了128个字符的编码
				- Unicode码
					- 背景：世界上存在多种编码方式，同一个二进制数字可以被解释成不同的符号，很容易出现乱码
					- Unicode将世界上所有的符号都纳入其中，每一个符号都给予了独一无二的编码
					- Unicode存在的问题
						- 不能区分Unicode和ASCII码，无法确定多个字节表示一个符号还是多个符号。
						- Unicode 的每个符号需要三到四个字节表示，但是英文字母只需要一个字节，十分浪费存储。导致Unicode出现了多种存储方式，也就是说有许多种不同的二进制格式，可以用来表示 Unicode
					- 相关网站
						- Unicode字符百科
						- Unicode
				- UTF-8编码
					- UTF-8 是 Unicode 的实现方式之一
					- uft-8是一种变长的编码方式，可以使用1~4个字表示一个符号，根据符号的不同变化字节长度
				- URL编码
					- 背景：因为出于兼容性考虑，很多服务器只识别ASCII字符。但如果URL中包含中文、日文这些非ASCII字符怎么办
					- URL编码规则
						- 如果字符是A~Z，a~z，0~9以及-、_、.、*，则保持不变；
						- 如果是其他字符，先转换为UTF-8编码，然后对每个字节以%XX表示；
					- 注意
						- URL编码是编码算法，不是加密算法
						- URL编码的目的是把任意文本数据编码为%前缀表示的文本，编码后的文本仅包含A~Z，a~z，0~9，-，_，.，*和%，便于浏览器和服务器处理
				- Base64编码
					- 背景：可以将二进制数据变成文本格式，这样好多文本中就可以处理二进制数据了。例如，电子邮件协议就是文本协议，如果要在电子邮件中添加一个二进制文件，就可以用Base64编码，然后以文本的形式传送。
					- 作用
						- 是一种编码算法，不是加密算法。
						- Base64编码可以把任意长度的二进制数据变为纯文本，且只包含A~Z、a~z、0~9、+、/、=这些字符
					- 原理
						- 把3字节的二进制数据按6bit一组
						- 每一组高位补两个0
						- 用4个int整数表示，然后查Base64索引表，把int整数用索引对应到字符，得到编码后的字符串。
					- 缺点
						- 传输效率会降低，因为它把原始数据的长度增加了1/3
			- 哈希算法
			  collapsed:: true
				- 定义：哈希算法（Hash）又称摘要算法（Digest），它的作用是：对任意一组输入数据进行计算，得到一个固定长度的输出摘要。
				- 特点
					- 相同的输入一定得到相同的输出
					- 不同的输入大概率得到不同的输出
				- 目的：为了验证原始数据是否被篡改
				- Java字符串的hashcode方法
					- 它的输入是任意字符串，输出是固定的4字节int整数
					- 两个相同的字符串永远会计算出相同的hashCode
					- 在覆盖 equals() 方法时应当总是覆盖 hashCode()方法，保证等价的两个对象哈希值也相等。否则基于hashCode定位的HashMap就无法正常工作
				- 哈希碰撞
					- 定义：两个不同的输入得到了相同的输出。哈希算法的输出长度越长，就越难产生碰撞，也就越安全
					- 安全的哈希算法满足的条件
						- 碰撞概率低
						- 不能猜测输出
				- 常见的哈希算法
				- 用途
					- 验证软件安装文件是否被人篡改
					- 数据库用户密码存储
				- 加盐
					- 目的：使黑客的彩虹表失效，即使用户使用常用口令，也无法从MD5反推原始口令
					- 彩虹表：提前计算好的密码和其哈希值对照表
					- 定义：对密码额外添加随机数，这个方法称之为加盐（salt），其算法：digest = md5(salt+inputPassword)
			- BouncyCastle
			  collapsed:: true
				- BouncyCastle就是一个提供了很多哈希算法和加密算法的第三方库。它提供了Java标准库没有的一些算法，例如，RipeMD160哈希算法。
				- 使用第三方算法前需要通过Security.addProvider()注册
			- Hmac算法
			  collapsed:: true
				- Hmac算法就是一种基于密钥的消息认证码算法，它的全称是Hash-based Message Authentication Code，是一种更安全的消息摘要算法。
				- HMAC算法包括一个秘密密钥和哈希函数。
					- 秘密密钥是一个唯一的信息或字符串。它是由发件人和消息的接收器所知。
					- 散列函数是一种将一个序列转换为另一个序列的映射算法。
				- HamcMd5相比于md5+salt的优势
					- HmacMD5使用的key长度是64字节，更安全
					- Hmac是标准算法，同样适用于SHA-1等其他哈希算法
					- Hmac输出和原有的哈希算法长度一致
			- 对称加密算法
			  collapsed:: true
				- 定义：用一个密码进行加密和解密的算法
					- 加密：secret = encrypt(key, message);
					- 解密：secret = encrypt(key, message);
					- 需要指定算法名称、工作模式和填充模式
				- DES
					- 注意：由于密钥过短，可以在短时间内被暴力破解，所以现在已经不安全了
				- AES
					- 特点
						- 可以加密任意长度的明文
					- 参考文章
						- [Java AES Encryption and Decryption](https://www.baeldung.com/java-aes-encryption-decryption)
				- IDEA
			- 口令加密算法
			  collapsed:: true
				- 背景：由于用户输入的密码安全性较弱，并不能达到加密算法对密码的长度要求，而且安全性也远不如随机数产生的随机口令。
				- 定义：使用用户口令（密码），采用随机数（salt），综合多种对称加密和摘要算法，生成密钥key。
				- 用途
					- 设计一个通用的“口令”加密软件，将随机生成的salt存储在U盘中，在用户输入密码时读取U盘中的salt，这样就得到了一个USB key的加密软件。
			- 密钥交换算法
			  collapsed:: true
				- 背景：为了解决在不安全的信道上面安全的传输密钥的问题
				- Diffie-Hellman算法
					- DH算法的本质就是双方各自生成自己的私钥和公钥，私钥仅对自己可见，然后交换公钥，并根据自己的私钥和对方的公钥，生成最终的密钥secretKey，DH算法通过数学定律保证了双方各自计算出的secretKey是相同的
					- 具体使用
						- 通过dh算法，通信双方确认密钥
						- 使用确认的密钥，采用例如AES这样的加密算法进行加解密
					- 缺点
						- 不能防止中间人攻击
			- 非对称加密算法
				- 定义：非对称加密就是加密和解密使用的不是相同的密钥，只有同一个公钥-私钥对才能正常加解密。
				- 特性
					- RSA密钥有256/512/1024/2048/4096等不同的长度。
				- 优势
					- 对称加密可以安全地公开各自的公钥，在N个人之间通信的时候：使用非对称加密只需要N个密钥对，每个人只管理自己的密钥对。而对称加密则需要N*(N-1)/2个密钥，因此每个人需要管理N-1个密钥，密钥管理难度大，而且非常容易泄漏
				- 缺点：
					- 运算速度非常慢，比对称加密要慢很多
					- 长度越长，密码强度越大，当然计算速度也越慢
					- 特定长度密钥只能加密一定长度的数据，例如使用512bit的RSA加密时，明文长度不能超过53字节，使用1024bit的RSA加密时，明文长度不能超过117字节
					- 不能防止中间人攻击
				- 应用案例
					- 小红和小明通信，他俩首先互换自己的RAS公钥给对方
					- 小红将AES的密钥用小明的RSA公钥加密，小明用自己的RSA私钥解密得到AES密钥
					- 双方使用这个共享的AES口令用AES加密通信
			- 签名算法
				- 目的：使用数字签名的目的是为了确认信息确实由某个发送的，任何人都不能伪造，并且发送方也不能抵赖
				- 使用
					- 数字签名就是用发送方的私钥对原始数据进行签名，只有用发送方公钥才能通过签名验证
					- 使用私钥加密生成数字签名：signature = encrypt(privateKey, sha256(message))，签名是针对原始消息的哈希进行签名
					- 使用公钥解密验证签名：hash = decrypt(publicKey, signature)
					- 使用解密后的哈希与原始消息的哈希进行对比
				- 用途
					- 防止伪造
					- 防止抵赖
					- 检测篡改
				- 常用的数字签名算法
					- MD5withRSA
					- SHA1withRSA
					- SHA256withRSA
				- DSA签名
					- 算法
						- SHA1withDSA
						- SHA256withDSA
						- SHA512withDSA
					- 优势
						- 和RSA数字签名相比，DSA的优点是更快
				- ECDSA签名
					- 特点
						- 可以从私钥推出公钥
						- 比特币的签名算法就采用了ECDSA算法
						- BouncyCastle提供了ECDSA的完整实现
			- 数字证书
				- 背景：摘要算法用来确保数据没有被篡改，非对称加密算法可以对数据进行加解密，签名算法可以确保数据完整性和抗否认性，把这些算法集合到一起，并搞一套完善的标准，这就是数字证书
				- 定义：集合了多种密码学算法，用于实现数据加解密、身份认证、签名等多种功能的一种安全标准
				- 特点
					- 数字证书就是集合了多种密码学算法，用于实现数据加解密、身份认证、签名等多种功能的一种安全标准
					- 数字证书采用链式签名管理，顶级的Root CA证书已内置在操作系统中
					- 数字证书存储的是公钥，可以安全公开，而私钥必须严格保密
				- 优势
					- 可以防止中间人攻击
				- Java数字证书的生成：keytool -storepass 123456 -genkeypair -keyalg RSA -keysize 1024 -sigalg SHA1withRSA -validity 3650 -alias mycert -keystore my.keystore -dname "CN=www.sample.com, OU=sample, O=sample, L=BJ, ST=BJ, C=CN"
					- keyalg：指定RSA加密算法；
					- sigalg：指定SHA1withRSA签名算法；
					- validity：指定证书有效期3650天；
					- alias：指定证书在程序中引用的名称；
					- dname：最重要的CN=www.sample.com指定了Common Name，如果证书用在HTTPS中，这个名称必须与域名完全一致。
		- 泛型
		  collapsed:: true
			- 背景
			  collapsed:: true
				- 解决的问题：Java数据类型和自定义对象类型较多，一种公共的数据结构或是算法，需要针对不同的类型和对象进行不同的处理。而且特别容易出错，例如类型强转错误
				- 定义：泛型编写模板代码来适应任意类型，又通过编译器保证了类型安全。例如ArrayList<T>，然后在代码中为用到的类创建对应的ArrayList<类型>，就可以创建任意类型的ArrayList
			- 相关名词
			  collapsed:: true
				- 类型变量（Type Varibles）：也称为泛型参数，用于指定一个泛型类型名称的标识符。也就是我们常见的E，T，K等标记符。
				- 参数化类型（Parameterized Types）：泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。这是一种行为。
			- 特点
			  collapsed:: true
				- 泛型的好处是使用时不必对类型进行强制转换，它通过编译器对类型进行检查
				- 泛型的继承关系：可以把ArrayList<Integer>向上转型为List<Integer>（T不能变，这里的T指的是Integer），但不能把ArrayList<Integer>向上转型为ArrayList<Number>或List<Number>（T不能变成父类）
				- 泛型可以同时定义多种类型，例如Map<K, V>
				- Java的泛型只能在类、构造器和方法上进行声明
			- Java中的泛型标记符
			  collapsed:: true
				- E - Element (在集合中使用，因为集合中存放的是元素)
				- T - Type（Java 类）
				- K - Key（键）
				- V - Value（值）
				- N - Number（数值类型）
				- ？ - 表示不确定的 java 类型
			- 泛型的使用
			  collapsed:: true
				- 泛型类
				  collapsed:: true
					- 泛型类的定义
					- 泛型类的继承
					  collapsed:: true
						- 在子类继承泛型类时，父类的泛型定义处是必须要传泛型实参的
					- 注意点
					  collapsed:: true
						- 在使用泛型的时候传入泛型实参，就会根据泛型实参对具体参数进行类型限制
						- 在使用泛型实参的时候不传泛型实参，在泛型类中使用的泛型方法或成员变量定义的类型可以为任何类型
						- 泛型的类型参数只能是引用类型，不能是原始类型
				- 泛型接口
				  collapsed:: true
					- 泛新接口的定义
					- 使用
					  collapsed:: true
						- 当实现泛型接口的类，传入泛型实参时，所有使用泛型的地方要替换成实参类型
						- 为实现泛型接口的类，未传入泛型实参时，需将泛型的声明也添加到类中
				- 泛型方法
				  collapsed:: true
					- 泛型方法的定义
					- 泛型类中的泛型方法
					- 静态方法和泛型
			- 擦拭法
			  collapsed:: true
				- Java泛型的局限性
					- 局限一：<T>不能是基本类型，例如int，因为实际类型是Object，Object类型无法持有基本类型
					- 局限二：无法取得带泛型对象的Class
						- 特殊案例
							- 可以通过类的继承和接口实现关系，获取泛型的Class对象
							- 具体实现：cn.bravedawn.generic.typeerasure.tclass.Main
						- [Java 获取泛型类型](https://www.jianshu.com/p/6bb9b8d6ee7a)
					- 局限三：无法判断带泛型的类型，这里是有解决办法的，这个可以参考cn.bravedawn.generic.typeerasure.GenericType
					- 局限四：不能实例化T类型
						- 泛型中不能new T()的原因有两个
							- 一是因为擦除，不能确定类型
							- 二是无法确定T中是否包含无参构造函数
					- 局限五：不能定义泛型参数化的静态成员变量
					  collapsed:: true
						- public class GenericsExample<T>{   private static T member; //This is not allowed}
					- 局限六：不能定义泛型异常类
					  collapsed:: true
						- public class GenericException<T> extends Exception {}
				- 不恰当的覆写方法
				  collapsed:: true
					- 不能覆写Object方法的equals(Object)为equals(T)
				- 泛型继承
				  collapsed:: true
					- 继承泛型类型的情况下，子类可以获取父类的泛型类型。这里可以参考cn.bravedawn.generic.typeerasure.IntPair
			- 限定通配符
			  collapsed:: true
				- <? extends T>
				  					- 作用：对泛型参数的上界进行限制，必须是泛型T或是他的子类
				  					- 作为方法参数时控制泛型参数类型为指定类型或是他的子类
				  - 上界描述符extends适合读取（get）的场景（可以获取具体类型和Object类型），并不适合写入（set，传入null除外）的场景
				  - 当<? extends T>作为泛型方法参数或是泛型变量声明的时候，这条规则都适用
				    collapsed:: true
				  	- 泛型方法参数声明：cn.bravedawn.generic.wildcards.upperbounds.v2.Main
				  	- 泛型变量声明：cn.bravedawn.generic.wildcards.upperbounds.v3.Test#main
				  				- <? super T>
				  					- 作用：对泛型参数的下界进行限制，必须是泛型T或者他的父类
				  					- 作为方法参数时控制泛型参数类型为指定类型或是他的父类
				   collapsed:: true
				  collapsed:: true
				  - 下界描述符super适合写入（set）的场景，并不适合读取（get只能拿到Object类型）的场景
				  - 也不是所有的父类类型都可以set的原因：<? super Apple>，可以set的元素可以是Apple的子类和她自己，他的父类是不行的，原因是我不知道他的父类有哪些
				  			- PECS原则
				  			  collapsed:: true
				  				- Producer Extends Consumer Super
				  				- 如果需要返回T，它是生产者（Producer），要使用extends通配符；如果需要写入T，它是消费者（Consumer），要使用super通配符
				  			- 桥接方法
				  			  collapsed:: true
				  				- 背景
				  collapsed:: true
				  					- 在jdk1.5之前例如集合的操作都是没有泛型支持的, 所以生成的字节码中参数都是用Object接收的, 所以也可以往集合中放入任意类型的对象, 集合类型的校验也被拖到运行期。
				  					- 在jdk1.5之后引入了泛型, 因此集合的内容校验被提前到了编译期, 但是为了兼容jdk1.5之前的版本java使用了泛型擦除, 所以如果不生成桥接方法就和jdk1.5之前的字节码不兼容了。
				  				- 作用：实现jdk1.5之前代码的兼容
				  				- 定义：在编译一个继承泛型类或是实现泛型接口的类和接口的时候，编译器会创建一个合成方法。称为桥接方法，他是类型擦除过程中的一部分。
				  			- 参考文章：
				  			  collapsed:: true
				  				- [廖雪峰-泛型](https://www.liaoxuefeng.com/wiki/1252599548343744/1265104600263968)
				  		- 注解
				  		  collapsed:: true
				  			- 定义
				  			  collapsed:: true
				  				- 提供了一种安全的类似注释的机制，用来将任何的信息或元数据（metadata）与程序元素（类、方法、成员变量等）进行关联。为程序的元素（类、方法、成员变量）加上更直观更明了的说明，这些说明信息是与程序的业务逻辑无关，并且供指定的工具或框架使用。Annontation像一种修饰符一样，应用于包、类型、构造方法、方法、成员变量、参数及本地变量的声明语句中。
				  			- 作用
				  			  collapsed:: true
				  				- 由编译器使用的注解
				  collapsed:: true
				  					- @Override：让编译器检查该方法是否正确地实现了覆写
				  					- @SuppressWarnings：告诉编译器忽略此处代码产生的警告
				  				- 由工具处理.class文件使用的注解，比如有些工具会在加载class的时候，对class做动态修改，实现一些特殊的功能。这类注解会被编译进入.class文件，但加载结束后并不会存在于内存中。这类注解只被一些底层库使用，一般我们不必自己处理。
				  				- 跟踪代码依赖性，实现替代配置文件功能。在程序运行期能够读取的注解，它们在加载后一直存在于JVM中，这也是最常用的注解。
				  			- 原理
				  			- 元注解
				  			  collapsed:: true
				  				- `@Documented`：注解是否将包含在JavaDoc中
				  				- `@Retention`： 什么时候使用该注解，定义注解的生命周期
				  collapsed:: true
				  					- `RetentionPolicy.SOURCE`: 在编译阶段丢弃。这些注解在编译结束之后就不再有任何意义，所以它们不会写入字节码。@Override, @SuppressWarnings都属于这类注解。
				  					- `RetentionPolicy.CLASS`: 仅class文件。在类加载的时候丢弃。在字节码文件的处理中有用，它们不会被加载进JVM。注解默认使用这种方式
				  					- `RetentionPolicy.RUNTIME` : 始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息。我们自定义的注解通常使用这种方式。该类型的注解会被加载进JVM，并且在运行期可以被程序读取
				  				- `@Target`：注解用于什么地方，默认值为任何元素，表示该注解用于什么地方。可用的ElementType 参数包括：
				  					- `ElementType.CONSTRUCTOR`：用于描述构造器
				  					- `ElementType.FIELD`: 成员变量、对象、属性（包括enum实例）
				  					- `ElementType.LOCAL_VARIABLE`: 用于描述局部变量
				  					- `ElementType.METHOD`: 用于描述方法
				  					- `ElementType.PACKAGE`：用于描述包
				  					- `ElementType.PARAMETER`： 用于描述参数
				  					- `ElementType.TYPE`：用于描述类、接口(包括注解类型) 或enum声明
				  					- `ElementType.ANNOTATION_TYPE`：用于描述注解类型
				  				- `@Inherited`：是否允许子类继承该注解
				  				- `@Repeatable`：定义Annotation是否可重复。这个注解应用不是特别广泛。
				  			- 常见标准的Annotation
				  				- @Override，标记类型注解，用作标注方法。它说明了被标注的方法重写了父类的方法，起到了断言的作用。如果我们使用了这种注解在一个没有覆盖父类方法的方法时，java 编译器将以一个编译错误来警示。
				  				- @Deprecated，标记类型注解，用于废弃代码。
				  				- @SuppressWarnings，非标记类型注解，它的作用是告诉编译器对被注解的作用域内部警告保持静默。
				  					- @SuppressWarnings("unchecked")：执行了未检查的转换时的警告，例如当使用集合时没有用泛型 (Generics) 来指定集合保存的类型。
				  					- @SuppressWarnings("serial")：某类实现Serializable(序列化)， 但没有定义 serialVersionUID 时的警告
				  					- @SuppressWarnings("deprecation")：表示不检测过期的方法,不显示使用了不赞成使用的类或方法时的警告。
				  			- 定义一个注解
				  			  collapsed:: true
				  				- 1. 用@interface声明一个注解
				  					- Annotation 型定义为@interface，所有的Annotation 会自动继承java.lang.Annotation这一接口，并且不能再去继承别的类或是接口
				  				- 2. 定义参数成员和默认值
				  					- 参数成员只能用public 或默认(default) 这两个访问权修饰
				  					- 参数成员只能用基本类型byte、short、char、int、long、float、double、boolean八种基本数据类型
				  					- String、Enum、Class、annotations等数据类型
				  					- 以及以上类型的数组
				  				- 3. 用元注解配置注解
				  			- 处理注解
				  			  collapsed:: true
				  				- 使用反射API判断是否有Annotation修饰
				  					- Class.isAnnotationPresent(AnnotationClass)
				  					- Field.isAnnotationPresent(AnnotationClass)
				  					- Method.isAnnotationPresent(AnnotationClass)
				  					- Constructor.isAnnotationPresent(AnnotationClass)
				  				- 使用反射API读取Annotation
				  					- Class.getAnnotation(AnnotationClass)
				  					- Field.getAnnotation(AnnotationClass)
				  					- Method.getAnnotation(AnnotationClass)
				  					- Constructor.getAnnotation(AnnotationClass)
				  				- 使用反射API读取Annotation有两种方法（读取Class上面修饰的注解）
				  					- 方法一是先判断Annotation是否存在，如果存在，就直接读取
				  					- 方法二是直接读取Annotation，如果Annotation不存在，将返回null
				  				- 读取方法、字段和构造方法的Annotation和Class类似
				  					- 获取到Annotation之后，将注解进行强转，就可以获取注解的属性了
				  					- 参考实现：cn.bravedawn.annotation.fruitexample.FruitInfoUtil
				  				- 读取方法参数使用getParameterAnnotations()
				  					- 参考实现：cn.bravedawn.annotation.parameterexample.AnnotationParametersUtil
				  				- 获取一个元素(Class、 Method、Constructor、Field)上的注解对象
				  					- getAnnotation(Class<T> annotationClass)
				  					- getAnnotations()
				  					- getAnnotationsByType(Class<T> annotationClass)
				  					- getDeclaredAnnotation(Class<T> annotationClass)
				  					- getDeclaredAnnotations()
				  					- getDeclaredAnnotationsByType(Class<T> annotationClass)
				  			- 参考文章
				  				- [廖雪峰-处理注解](https://www.liaoxuefeng.com/wiki/1252599548343744/1265102026065728)
				  		- 反射
				  		  collapsed:: true
				  			- 定义
				  			  collapsed:: true
				  				- Java的反射是指程序在运行期可以拿到一个对象的所有信息
				  				- 反射是为了解决在运行期，对某个实例一无所知的情况下，如何调用其方法
				  			- Class类
				  			  collapsed:: true
				  				- 特点
				  					- 除基本类型外，Java的其他类型都是Class（包括interface），Class的本质是数据类型
				  					- JVM每加载一个类，就会为其创建一个Class类型的实例
				  					- 由于JVM为每个加载的类创建了对应的Class实例，并在实例中保存了该类的所有信息，包括类名、包名、父类、实现的接口、所有方法、字段等，因此，如果获取了某个Class实例，我们就可以通过这个Class实例获取到该实例对应的类的所有信息。
				  				- 获取Class实例的方法
				  					- 方法一：直接通过一个类的静态变量class获取
				  					- 方法二：如果我们有一个实例变量，可以通过该实例变量提供的getClass()方法获取
				  					- 方法三：如果知道一个class的完整类名，可以通过静态方法Class.forName()获取
				  				- Class实例比较和instanceof的差别
				  					- 用instanceof不但匹配指定类型，还匹配指定类型的子类。
				  					- 用==判断class实例可以精确地判断数据类型，但不能作子类型比较。
				  				- 通过反射生产对象的方式
				  					- 方法一：调用Class提供的`newInstance()`方法，创建无参构造函数的实例
				  					- 方法二：先通过Class对象获取指定的`Constructor`对象，再调用Constructor对象的newInstance()方法来创建实例。这种方法可以用指定的构造器构造类的实例
				  				- 动态加载
				  					- JVM在执行Java程序的时候，并不是一次性把所有用到的类全部加载到内存，而是第一次需要用到类时才加载。
				  					- 利用JVM动态加载类的特性，我们才能在运行期根据条件加载不同的实现类。
				  				- 重要方法
				  					- `isInterface()`：该对象是否是一个接口
				  					- `isAnonymous()`：是否是匿名类
				  					- `class.newInstance()`
				   collapsed:: true
				  - 会直接调用该类的无参构造函数进行实例化
				  					- `class.getDeclaredConstructor(Class<?>... parameterTypes).newInstance()`
				   collapsed:: true
					- getDeclaredConstructor()方法会根据他的参数对该类的构造函数进行搜索并返回对应的构造函数，没有参数就返回该类的无参构造函数，然后再通过newInstance进行实例化。
			- 访问字段
			  collapsed:: true
				- 通过Class实例获取字段信息，Class提供了 以下几个方法来获取字段
					- Field getField(name)：根据字段名获取某个public的field（包括父类）
					- Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
					- Field[] getFields()：获取所有public的field（包括父类）
					- Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）
				- 允许访问非public字段：setAccessible(true)
				- 获取字段的信息
					- getName()：返回字段名称，例如，"name"；
					- getType()：返回字段类型，也是一个Class实例，例如，String.class；
					- getModifiers()：返回字段的修饰符，它是一个int，不同的bit表示不同的含义
				- 获取字段值：field.get(object)
				- 设置字段值：field.set(object, value)
			- 调用方法
			  collapsed:: true
				- 通过Class实例获取Method信息，Class提供了 以下几个方法来获取方法
					- Method getMethod(name, Class...)：获取某个public的Method（包括父类）
					- Method getDeclaredMethod(name, Class...)：获取当前类的某个Method（不包括父类）
					- Method[] getMethods()：获取所有public的Method（包括父类）
					- Method[] getDeclaredMethods()：获取当前类的所有Method（不包括父类）
				- 获取Mehtod对象的方法信息
					- getName()：返回方法名称，例如："getScore"；
					- getReturnType()：返回方法返回值类型，也是一个Class实例，例如：String.class；
					- getParameterTypes()：返回方法的参数类型，是一个Class数组，例如：{String.class, int.class}；
					- getModifiers()：返回方法的修饰符，它是一个int，不同的bit表示不同的含义。
			- 调用构造方法
			  collapsed:: true
				- Class.newInstance()的局限
					- 只能调用该类的public无参数构造方法
					- 如果构造方法带有参数，或者不是public，就无法直接通过Class.newInstance()来调用
				- 通过Class实例获取Constructor的方法
					- getConstructor(Class...)：获取某个public的Constructor；
					- getDeclaredConstructor(Class...)：获取某个Constructor；
					- getConstructors()：获取所有public的Constructor；
					- getDeclaredConstructors()：获取所有Constructor;
				- Constructor总是当前类定义的构造方法，和父类无关，因此不存在多态的问题
				- 调用非public的Constructor时，必须首先通过setAccessible(true)设置允许访问，否则setAccessible(true)可能会失败。
			- 获取继承关系
			  collapsed:: true
				- 获取父类类型：Class getSuperclass()
				- 获取当前类实现的所有接口：Class[] getInterfaces()
				- 通过Class对象的isAssignableFrom()方法可以判断一个向上转型是否可以实现
				- *isAssignableFrom()**判断当前的**Class**对象所表示的类，是不是参数中传递的**Class**对象所表示的类的父类，超接口，或者是相同的类型。是则返回**true**，否则返回**false*
			- 获取注解信息
			  collapsed:: true
				- Annotation[] getAnnotations() ：返回Method对象上的注解信息。
			- 动态代理
			  collapsed:: true
				- 定义
					- 若一个接口没有实现类，但在代码运行期动态创建了一个接口对象的方式，我们称之为动态代码。JDK提供动态创建接口对象的方式，就叫动态代理。
				- Java标准库提供了动态代理功能，允许在运行期动态创建一个接口的实例
				- 动态代理是通过Proxy创建代理对象，然后将接口方法“代理”给InvocationHandler完成的
			- 特殊方法
			  collapsed:: true
				- Reflection.getCallerClass()：获取当前方法的调用类的class对象
			- 方法句柄
			  collapsed:: true
				- 方法句柄MethodHandle
					- 类似于反射，可以实现方法的间接调用。
		- SPI机制
		  collapsed:: true
			- 定义
				- 是JDK内置的一种 服务提供发现机制，可以用来启用框架扩展和替换组件，主要是被框架的开发人员使用
				- 核心思想是解耦
			- 实现
				- 定义一个接口
				- 为接口提供不同的实现
				- 在resources下新建META-INF/services/目录，以接口名新建一个文件，然后将接口实现类的全限定名写在该文件中
			- SPI机制的使用
				- JDBC DriverManager
					- 在Java17中可以参考java.sql.DriverManager#ensureDriversInitialized这个方法
					- 在SPI加载驱动的时候相应jar包对java.sql.Driver接口的实现类都会被实例化
				- Common-Logging
					- 这里定义的接口是org.apache.commons.logging.LogFactory
					- 具体的接口逻辑参考：org.apache.commons.logging.LogFactory#getFactory，这里面就有尝试使用java spi服务发现机制，在META-INF/services下寻找org.apache.commons.logging.LogFactory的实现
				- 插件体系
					- Eclipse使用OSGi作为插件系统的基础，通过规定固定的文件结构去管理插件的生命周期
				- Spring中SPI机制
					- Spring在做自动装配的时候，会加载META-INF/spring.factories文件，而加载的过程是由SpringFactoriesLoader加载的。
					- Spring中具体的代码在org.springframework.core.io.support.SpringFactoriesLoader#loadFactoryNames
			- SPI深入原理
				- 使用流程
				  collapsed:: true
					- 定义标准，比如java.sql.Driver
					- 具体厂商或是开发者实现
						- 在META-INF/services/目录下定义接口全限定名的文件，填写实现类的全限定名
						- 编写接口实现
					- 开发人员使用，这里可以参考JavaTrain项目的cn.bravedawn.spi.example.Test
				- SPI和API之间的区别
				  collapsed:: true
					- API是我们直接调用一个方法，以达到某一个目标，代码逻辑组织在实现者的包中
					- SPI是我们需要拓展和实现，以达到某一个目标，代码逻辑组织在调用者的包中
				- SPI机制的实现原理
				  collapsed:: true
					- 源码类：java.util.ServiceLoader
					- 具体阅读笔记参考：cn.bravedawn.spi.example.Test
				- SPI的缺点
				  collapsed:: true
					- 不能按需加载，必须遍历所有实现并实例化，造成浪费
					- 获取某个实现类的方式不够灵活，只能通过Iterator形式获取
					- 多线程下使用ServiceLoader类的实例是不安全的
				- 参考文章
				  collapsed:: true
					- [Java SPI机制：ServiceLoader实现原理及应用剖析](https://juejin.cn/post/6844903891746684941)
		- XML
		  collapsed:: true
			- XML文档的定义文件
				- DTD（此类文件的后缀名为 dtd）
				- XML Schema（此类文件的后缀名为 xsd）
			- XPath（XML Path Language）
				- 一种小型的查询语言能够根据 XML结构树在树中寻找节点。
				- javax.xml.xpath包提供了强大的 XPath解析功能，可以基于它实现 XML的解析。
				-
		- Java核心类和接口
		  collapsed:: true
			- BigInteger
			  collapsed:: true
				- 背景
					- Java中，由CPU原生提供的整型最大范围是64位long型整数。使用long型整数可以直接通过CPU指令进行计算，速度非常快
					- 若使用的整数范围超过了long型，此时就需要用软件来模拟一个大整数
				- 定义：java.math.BigInteger就是用来表示任意大小的整数。BigInteger内部用一个int[]数组来模拟一个非常大的整数
				- 特点
					- 是不可变类
					- 没有范围限制，缺点是速度比较慢
				- 转换为基本类型
					- xxxValue()：会丢失高位信息，结果不一定准确
					- xxxValueExact()：精准的转换，如果转换超出范围，将直接抛出ArithmeticException异常
				- 输出字节数组的16进制表示：new BigInteger(1, hash).toString(16)
			- BigDecimal
			  collapsed:: true
				- RoundingModed定义了8中舍入规则
				  collapsed:: true
					- ROUND_UP：向远离零的方向舍入
						- 若舍入位为非零，则对舍入部分的前一位数字加1；若舍入位为零，则直接舍弃。即为向外取整模式。
					- ROUND_DOWN：向接近零的方向舍入
						- 不论舍入位是否为零，都直接舍弃。即为向内取整模式。
					- ROUND_CEILING：向正无穷大的方向舍入
						- 若 BigDecimal 为正，则舍入行为与 ROUNDUP 相同；若为负，则舍入行为与 ROUNDDOWN 相同。即为向上取整模式。
					- ROUND_FLOOR：向负无穷大的方向舍入
						- 若 BigDecimal 为正，则舍入行为与 ROUNDDOWN 相同；若为负，则舍入行为与 ROUNDUP 相同。即为向下取整模式。
					- ROUNDHALFUP：向“最接近的”整数舍入
						- 若舍入位大于等于5，则对舍入部分的前一位数字加1；若舍入位小于5，则直接舍弃。即为四舍五入模式。
					- ROUNDHALFDOWN：向“最接近的”整数舍入
						- 若舍入位大于5，则对舍入部分的前一位数字加1；若舍入位小于等于5，则直接舍弃。即为五舍六入模式。
					- ROUNDHALFEVEN：向“最接近的”整数舍入
						- 若（舍入位大于5）或者（舍入位等于5且前一位为奇数），则对舍入部分的前一位数字加1；
						- 若（舍入位小于5）或者（舍入位等于5且前一位为偶数），则直接舍弃。即为银行家舍入模式。
					- ROUND_UNNECESSARY：
						- 断言请求的操作具有精确的结果，因此不需要舍入。
						- 如果对获得精确结果的操作指定此舍入模式，则抛出ArithmeticException。
				- BigDecimal的三个toString方法
					- 三个方法
						- `toEngineeringString`：有必要时使用工程计数法。工程记数法是一种工程计算中经常使用的记录数字的方法，与科学技术法类似，但要求10的幂必须是3的倍数
						- `toPlainString`：不使用任何指数
						- `toString`：有必要时使用科学计数法
					- 具体实现：JavaTrain/src/main/java/cn/bravedawn/basic/math/bigdecimal/BigDecimalExample2.java
					- 参考文章：https://www.cnblogs.com/happy520/p/7090199.html
			- Serializable interfaces
			  collapsed:: true
				- 参考 ((641475d2-462e-43b7-a273-77ab40289cde))
			- Cloneable interfaces
			  collapsed:: true
				- Java8
					- 静态工厂方法：Comparator.comparing()
				- 参考文章
					- Comparator and Comparable in Java
			- Comparable
			  collapsed:: true
				- comparable用于我们在编写实体类时比较对象的主要方式。它定义了一种将对象与其他同类对象进行比较的策略。这被称为类的“自然排序”。
				- Comparable接口是用于定义默认排序的好选择。
			- Comparator
			  collapsed:: true
				- omparator 接口定义了一个带有两个参数的 compare(arg1, arg2) 方法，这些参数表示比较对象。
				- 已经有 Comparable，为什么还要使用 Comparator 呢？
					- 一：有时我们无法修改要排序的对象的类的源代码，从而导致无法使用 Comparable。
					- 二：使用比较器可以避免向我们的领域类添加额外的代码。
					- 三：可以定义多种不同的比较策略，这在使用 Comparable 时是不可能的。
				- 避免使用减法定义比较器
					- 由于整数溢出，“Integer.MAX_VALUE – (-1)”将小于零。具体代码实现参考：JavaTrain/src/main/java/cn/bravedawn/basic/coreclass/compare/java8/AvoidSubtractionTrick.java
			- AutoCloseable
			- BeanInfo
			- PropertyDescriptor
	- Java进阶
		- 集合框架
		  collapsed:: true
			- Java Collection Framwork
			  collapsed:: true
				- 背景
				  collapsed:: true
					- 集合框架是在Java 1.2之后推出的，之前对Java对象进行集合操作的类是Array，Vectors或是HashTable，这些集合类都没有公共接口，尽管所有集合的主要目标是相同的，但所有这些集合的实现都是独立定义的，它们之间没有相关性。而且，用户很难记住每个集合类中出现的所有不同的方法、语法和构造函数。
					- 这些集合(Array、Vector或Hashtable)都没有实现标准的成员访问接口，因此程序员很难编写适用于所有类型集合的算法。
				- 集合框架的优点
					- 一致的API:：API有一组基本的接口，如Collection、set、List或Map，所有实现这些接口的类(ArrayList、LinkedList、Vector等)都有一些公共的方法集。
					- 减少编程工作量：程序员不必担心Collection的设计，相反，他可以专注于在他的程序中最好地使用它。因此，面向对象编程(即)抽象的基本概念已经成功地实现了。
					- 提高程序速度和质量：通过提供有用数据结构和算法的高性能实现来提高性能，因为在这种情况下，程序员不需要考虑特定数据结构的最佳实现。他可以简单地使用最好的实现来大幅提高算法/程序的性能。
				- Methods of the Collection Interface
				  collapsed:: true
					- 1. add(Object)：添加一个对象到该集合中
					- 2. addAll(Collection c)：将集合中所有的元素添加到该集合中
					- 3. clear()：清除该集合所有的元素
					- 4. contains(Object o)：若该集合中包含该元素，则返回true
					- 5. containsAll(Collection c)：若该集合中包含给定集合的所有元素，则返回true
					- 6. equals(Object o)：比较指定对象与此集合是否相等
					- 7. hashCode()：用于返回此集合的哈希码值
					- 8. isEmpty()：判断集合是否为空
					- 9. iterator()：返回一个遍历集合中元素的迭代器
					- 10. parallelStream()：返回一个以此集合为源的并行流
					- 11. remove(Object o)：用于从集合中删除给定对象。如果有重复值，则该方法删除第一个出现的对象
					- 12. removeAll(Collection c)：用于从集合中删除给定集合中提到的所有对象
					- 13. removeIf(Predicate filter)：用于删除集合中满足给定谓词的所有元素
					- 14. retainAll(Collection c)：用于仅保留此集合中包含在指定集合中的元素
					- 15. size()：用于返回集合中元素的数量
					- 16. spliterator()：用于在此集合中的元素上创建Spliterator
					- 17. stream()：用于返回以此集合为源的顺序流
					- 18. toArray()：用于返回包含此集合中所有元素的数组
				- 集合框架的其他接口
				  collapsed:: true
					- Iterable Interface
						- 集合框架的根接口
						- 功能：为集合提供一个迭代器
						- 方法
							- iterator()：返回一个迭代器
							- forEach(Consumer<? super T> action)：运行给定的action遍历元素
							- spliterator()：创建一个Spliterator
					- Enumeration Interface
						- 枚举从 1.0 版开始就出现在 Java 中。 它是一个接口，任何实现都允许一个一个地访问元素。 简单来说，它用于迭代 Vector 和 Hashtable 等对象的集合。
						- 与Iterator的区别
							- ![iterator和enumeration的区别.png](../assets/iterator和enumeration的区别_1676257615300_0.png)
					- Collection Interface
					  collapsed:: true
						- 由集合框架中的所有类实现，包含了每个集合都有的所有基本方法，这个接口建立了一个实现集合类的基础
					- List Interface
					  collapsed:: true
						- 专门用于列表类型的数据，我们可以在其中存储对象的所有有序集合。
						- 实现该接口的类
						  collapsed:: true
							- ArrayList
							- LinkedList
							- Vector
							- Stack
					- Queue Interface
					  collapsed:: true
						- 队列接口维护FIFO(先进先出)顺序。
						- 实现该接口的类
						  collapsed:: true
							- PriorityQueue
					- Deque Interface
					  collapsed:: true
						- 这是队列数据结构的一个非常微小的变化。Deque也称为双端队列，是一种数据结构，我们可以在其中从队列的两端添加和删除元素。该接口扩展了Queue接口。
						- 实现该接口的类
						  collapsed:: true
							- ArrayDeque
					- Set Interface
					  collapsed:: true
						- 对象的无序集合，其中不能存储重复的值。
						- 实现该接口的类
						  collapsed:: true
							- HashSet
							- LinkedHashSet
							- TreeSet
					- Map Interface
					  collapsed:: true
						- Map是一种支持数据的键值对映射的数据结构。此接口不支持重复键，因为同一个键不能有多个映射。
						- 实现该接口的类
						  collapsed:: true
							- HashMap
							- TreeMap
			- Collections
			  collapsed:: true
				- 基本操作
					- 获取list，map，set的不变实体
					- addAll()：方法添加集合到另一个集合
					- copy()：复制元素
					- binarySearch()：查找元素，查找之前先要做升序排序
					- sort()：对集合进行排序
					- disjoint()：判断两个集合是否不相交
				- 具体实现
					- JavaTrain/src/main/java/cn/bravedawn/collection/collections
				- 参考文章
					- [Collections Class in Java](https://www.geeksforgeeks.org/collections-class-in-java/)
					  id:: 63a8ef52-fbe6-4838-b3e2-620dbb283662
			- Collection Interface
			  collapsed:: true
				- JDK 不提供此接口的任何直接实现：它提供更具体的子接口（如 Set 和 List）的实现。此接口通常用于传递集合并在需要最大通用性的地方操作它们。
				- 如果集合实现没有实现特定的操作，它应该定义相应的方法来抛出 UnsupportedOperationException。
			- List
			  collapsed:: true
				- 定义：List是最基础的一种集合：它是一种有序列表
				- List<E>接口两个实现
				  collapsed:: true
					- ArrayList，通过数组实现
					- LinkedList，通过链表实现
					- 他两的区别
					  :LOGBOOK:
					  CLOCK: [2023-01-11 Wed 20:23:34]--[2023-01-11 Wed 20:23:35] =>  00:00:01
					  :END:
					  ![ArrayList和LinkedList的区别.jpeg](../assets/ArrayList和LinkedList的区别_1673439826139_0.jpeg){:height 143, :width 626}
				- 特点
				  collapsed:: true
					- List接口允许我们添加重复的元素
					- List允许添加null值
					- List是一个有序列表
				- 操作
				  collapsed:: true
					- 创建List
						- 法一：List<Integer> list = new ArrayList();
						- 法二：List<Integer> list2 = new LinkedList();
						- 法三：List<Integer> list3 = List.of(1, 2, 4);
					- 遍历List
						- for循环
						- for each遍历，Java也是通过Iterator来实现的
						- Iterator遍历，是最高效的方法
					- List转Array
						- 法一：是调用toArray()方法直接返回一个Object[]数组
						  ```java
						  List list = List.of("apple", "pear", "banana");
						  Object[] array = list.toArray();
						  ```
						- 法二：调用toArray(T[])方法
						  ```java
						  List list = List.of(12, 34, 56);
						  Integer[] array = list.toArray(new Integer[3]);
						  ```
							- 另外两种写法
								- `Integer[] array = list.toArray(new Integer[list.size()]);`
								- `Integer[] array = list.toArray(Integer[]::new);`
					- Array转List
						- 方法一：
						  ```Java
						  Integer[] array = { 1, 2, 3 };
						  List<Integer> list = List.of(array);
						  ```
							- Java9以后的版本可以使用这个方法
							- List.of()返回的是一个**只读**的list
							- 对只读List调用add()、remove()方法会抛出UnsupportedOperationException
						- 方法二：
						  ```java
						  Integer[] array = { 1, 2, 3 };
						  List<Integer> list = Arrays.asList(array);
						  ```
					- 注意
						- 若要调用List的`contains()`、`indexOf()`方法，放入的元素需要实现`equals()`方法，因为这些方法的内部是通过元素的equals进行判断的
				- LinkedList
				  collapsed:: true
					- 介绍
						- 使用双向链表来存储元素
						- 实现了List和Deque接口，实现了所有的List可选的列表操作，继承了AbstractSequentialList类
						- 实现了所有可选的列表操作并允许所有元素（包括null）
					- 特点
						- 可以包含重复的元素
						- 维护插入的顺序
						- 非同步的，可以通过调用 Collections.synchronizedList 方法来检索它的同步版本
						  id:: 63a8ef52-c395-4958-9d97-65e6d05e4e55
						- 它的Iterator和ListIterator迭代器是fail-fast
						- 它可以用作list，stack，queue
					- 使用
					  collapsed:: true
						- 创建：LinkedList<Integer> list = new LinkedList<>()
						- 添加元素
						  collapsed:: true
							- add()
							- addAll()
							- addFirst()
							- addLast()
						- 移除元素
						  collapsed:: true
							- removeFirst()
							- removeLast()
							- removeFirstOccurrence()
							- removeLastOccurrence()
						- 队列操作
						  collapsed:: true
							- linkedList.poll()，检索第一个元素并从list删除该元素，若list为空，则返回null
							- linkedList.pop()，检索第一个元素并从list删除该元素，若list为空，则抛出java.util.NoSuchElementException
							- linkedList.push(1)，在list头部插入元素
						- 总结
							- ArrayList 通常是默认的 List 实现，大家常常会使用这个实现
							- 在恒定时间做插入、删除操作时，采用LinkedList往往是更好的选择。ArrayList更适合恒定的访问时间和有效的内存使用。
					- 参考文章：
					  collapsed:: true
						- javapoint：https://www.baeldung.com/java-linkedlist
						- baeldung：https://www.javatpoint.com/java-linkedlist
				- ArrayList
				  collapsed:: true
					- 介绍
						- ArrayList是构建在数组之上的List实现之一
					- 特点
						- 一个值可以重复出现多次
						- 随机访问的时间复杂度是O(1)
						- 插入和删除的时间复杂度是O(n)
						- 搜索未排序的list需要 O(n) 的时间，二分搜索排序的list需要 O(logn) 的时间
					- 使用
						- 创建一个ArrayList
						  collapsed:: true
							- 默认无参构造函数
							- 构造函数接受初始容量
							- 构造函数接受 Collection
						- 添加一个元素到ArrayList
						  collapsed:: true
							- 添加一个元素：add()
							- 一次插入一个Collection或一些元素：addAll()
						- 迭代ArrayList
						  collapsed:: true
							- ListIterator可以从两个方向上遍历列表
							- Iterator只能从一个方向上遍历列表
						- 搜索ArrayList
						  collapsed:: true
							- 搜索没有排序的List
							  collapsed:: true
								- 从头部搜索元素并返回下标：indexOf()
								- 从尾部搜索元素并返回下标：lastIndexOf()
							- 搜索排序的List
							  collapsed:: true
								- 先排序：Collections.sort(copy)
								- 后搜索：Collections.binarySearch(copy, "f")
						- 从ArrayList中移除元素
							- 从list中移除元素
							- 通过迭代器去移除元素
							- 通过使用Java8 Stream API
					- 参考文章：
					  collapsed:: true
						- Baeldung：Guide to the Java ArrayList
						- javatpoint：Java ArrayList
					- 代码实现：cn.bravedawn.collection.list.arraylist
					- Imutable ArryaList
					  collapsed:: true
						- 五种实现
							- 一、使用JDK提供了可以从现有集合中获取不可修改集合的方法：Collections.unmodifiableList(list)
							- 二、在Java9中提供了List<E>.of(E… elements)静态工厂方法，来创建不可变列表
							- 三、Guava提供也提供了创建不可变列表的方法，该操作实际上创建了一个新的副本：ImmutableList.copyOf(list)
							- 四、Guava还提供了一个构造器，返回强类型的ImmutableList，而不是简单的List：ImmutableList.<String>builder().addAll(list).build()
							- 五、Apache Collections Commons提供了创建不可变列表的方法：ListUtils.unmodifiableList(list)
						- 参考文章：https://www.baeldung.com/java-immutable-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/arraylist/ImmutableArrayListExample.java
				- CopyOnWriteArrayList
				  collapsed:: true
					- 特点
					  collapsed:: true
						- CopyOnWriteArrayList适合在迭代遍历场景较多，频繁修改场景较少的情况。读多写少。
					- CopyOnWriteArrayList的迭代遍历
						- 介绍
						  collapsed:: true
							- CopyOnWriteArrayList允许以线程安全的方式迭代列表而不需要显示进行同步
						- 迭代的API设计
						  collapsed:: true
							- CopyOnWriteArrayList在修改元素时，比如新增add()或是删除remove()操作时，并不直接操作元数据，操作的是副本数据（CopyOnWriteArrayList 的全部内容被复制到新的内部副本中）
							- 在 CopyOnWriteArrayList 上调用 iterator()方法时，我们会返回一个由 CopyOnWriteArrayList 内容的不可变快照备份的迭代器
						- 在遍历CopyOnWriteArrayList允许插入元素
							- 在遍历CopyOnWriteArrayList时插入元素，不影响之前创建的迭代器
						- 在遍历CopyOnwriteArrayList不允许移除元素
							- 由于复制机制，不允许对返回的 Iterator执行 remove() 操作，否则就会报错 UnsupportedOperationException
						- 参考文章：https://www.baeldung.com/java-copy-on-write-arraylist
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/copyonwritearraylist
				- List的比较和使用场景
				- List的应用
				  collapsed:: true
					- 多维列表
					  collapsed:: true
						- 创建二维数组：ArrayList<ArrayList<Integer>>
						- 创建三维数组：ArrayList<ArrayList<ArrayList<String>>>
						- 参考文章：https://www.baeldung.com/java-multi-dimensional-arraylist
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/multidimensinalarraylist
					- Iterator转换为List
					  collapsed:: true
						- 六种方法
						  collapsed:: true
							- 一、使用while循环将Iterator转为List
							- 二、在Java8中使用 Iterator的forEachRemaining()方法来实现Iterator转List
							- 三、使用Java8 Stream API实现 Iterator -> (Iterable) -> List
							- 四、使用 Guava 实现 Iterator 转为不可变的 List
							- 五、使用 Guava将Iterator转为可变的List
							- 六、使用 Apache commons Collections实现Iterator转为List
						- 参考文章：https://www.baeldung.com/java-convert-iterator-to-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/iteratortolist
					- 从List获取随机元素
					  collapsed:: true
						- 五种实现
						  collapsed:: true
							- 一、使用Random.next生成随机数，获取List中的随机元素，除此之外，我们也可以使用Math.random()实现
							- 二、使用专用的 ThreadLocalRandom 类为每个线程创建一个新实例，避免多线程情况下选择相同的值
							- 三、选择多个随机元素，重复随机获取一个元素的过程
							- 四、选择多个随机元素，不会出现重复的元素
							- 五、使用Collections.shuffle(givenList)获得随机的多个元素
						- 参考文章：https://www.baeldung.com/java-random-list-element
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/pickrandomitem
					- 将list分区
					  collapsed:: true
						- 背景：Java标准库不支持List的分区操作，Guava、Apache Commons Collections对该操作都有实现
						- 使用Guava实现分区
						  collapsed:: true
							- 使用Guava获取列表-List的分区
							- 使用Guava获取集合-Collection的分区
							- 使用Guava分区，分区（子列表）是原始集合的子列表视图，对原始集合的修改会同步反映在分区中
						- 使用Apache Commons Collections实现分区
						  collapsed:: true
							- 用Apache commons Collections分区，分区（子列表）是原始集合的子列表视图，这意味着原始集合中的更改将反映在分区中
							- 使用Java8 Collectors.partitioningBy()实现分区，生成的分区不是原列表的视图，因此原列表发生的任何更改都不会影响分区
							- 使用Java8 Collectors.groupingBy() 实现分区，生成的分区不是原列表的视图，因此原列表发生的任何更改都不会影响分区
							- 使用Java8 按分隔符拆分列表
						- 参考文章：https://www.baeldung.com/java-list-split
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/splitlisttosublists
					- 移除list中为null的元素
					  collapsed:: true
						- 三种方法
						  collapsed:: true
							- 方法一：使用Java原生提供的方法去移除null元素，会直接修改原list
							- 方法二：使用Guava移除null元素
							  collapsed:: true
								- 移除null会修改原列表
								- 移除null不修改原列表
							- 方法三：使用Apache commons Collections 移除null元素，会直接修改原列表
							- 方法四：使用Java8 Lambda移除null元素
							  collapsed:: true
								- 并行移除
								- 串行移除
								- 使用list.removeIf()方法
						- 参考文章：https://www.baeldung.com/java-remove-nulls-from-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/removenull
					- 移除list中重复的元素
					  collapsed:: true
						- 三种方法
						  collapsed:: true
							- 使用原生Java 移除重复元素
							  collapsed:: true
								- 使用HashSet实现，它是一个无序集合，移除重复元素之后列表的顺序可能和原列表元素顺序不同
								- 使用LinkedHashSet保证移除重复元素后列表的元素顺序与原列表元素顺序相同
							- 使用Guava移除重复元素
							  collapsed:: true
								- 使用Sets.newHashSet()，无法保证与原列表元素顺序一致
								- 使用Sets.newLinkedHashSet()，保证与原列表元素顺序一致
							- 使用Java stream distinct()移除重复元素，distinct()方法返回的是一个与原列表顺序一致的列表
						- 参考文章：https://www.baeldung.com/java-remove-duplicates-from-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/removeduplicate
					- 在list中查找一个元素
					  collapsed:: true
						- 四种方法
						  collapsed:: true
							- 使用Java原生api查找列表中的一个元素
							  collapsed:: true
								- contains()
								- indexOf()
								- Java Looping
								- Looping with an Iterator
							- 通过Java8 Stream API查找元素
							- 使用Guava查找列表中的一个元素，采用Iterables.tryFind()方法
							- 使用Apache Commons Collections实现查找一个元素
						- 参考文章：https://www.baeldung.com/find-list-element-java
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/findlistelement
					- list的UnsupportedOperationException异常
					  collapsed:: true
						- 说明：当我们对list执行相关操作的时候，往往就会抛出这个异常
						- 出现场景
						  collapsed:: true
							- 第一种：对java.util.Arrays.ArrayList的对象，使用add()操作
							- 第二种：对不可变列表进行修改操作时，会抛出 java.lang.UnsupportedOperationException
						- 参考文章：https://www.baeldung.com/java-list-unsupported-operation-exception
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/unsupportedoperationexception
					- 复制一个list到另一个list
					  collapsed:: true
						- 五种方法
							- 使用ArraysList的结构体参数传入
							  collapsed:: true
								- 可变类，复制之后对原列表元素对象属性的修改，会同步体现在复制后的列表上
								- 不可变类，复制之后对原列表元素的修改，不会同步到复制后的列表上
							- 使用addAll()方法
							  collapsed:: true
								- 可变类，复制之后对原列表元素对象属性的修改，会同步体现在复制后的列表上
								- 不可变类，复制之后对原列表元素的修改，不会同步到复制后的列表上
							- 使用Collections.copy()方法
							  collapsed:: true
								- 若原列表与目标列表长度一致，原列表中的元素会按照下标覆盖目标列表
								- 若原列表与目标列表长度不一致，原列表的元素会按照下标覆盖目标列表，目标列表其余元素会自动追加到后面
							- 使用Java8 stream，他除了拷贝外还提供了skip()和filter()等功能
							  collapsed:: true
								- 可变类，复制之后对原列表元素对象属性的修改，会同步体现在复制后的列表上
								- 不可变类，复制之后对原列表元素的修改，不会同步到复制后的列表上
							- 使用Java10提供的List.copyOf()方法
							  collapsed:: true
								- 可变类，复制之后对原列表元素对象属性的修改，会同步体现在复制后的列表上
								- 不可变类，复制之后对原列表元素的修改，不会同步到复制后的列表上
							- 使用clone()方法
							  collapsed:: true
								- 空笔记
						- 参考文章：https://www.baeldung.com/java-copy-list-to-another
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/copylist
					- 从列表中删除特定值的所有匹配项
					  collapsed:: true
						- 方法
						  collapsed:: true
							- 用while循环，移除一个列表中的所有特定元素
							- 使用for循环，移除一个列表中的所有特定元素
							- for-each循环，移除一个列表中的所有特定元素
							- Iterator循环，移除一个列表中的所有特定元素
							- Collecting，创建一个新的list去保存我们想要的元素
							- 使用Java8 Stream api移除元素
							- 【推荐使用】使用removeIf()移除不需要的元素
						- 参考文章：https://www.baeldung.com/java-remove-value-from-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/removealloccurencevalue
					- 添加多个项到列表中
					  collapsed:: true
						- 三种方法
						  collapsed:: true
							- 添加多个元素到列表中
							  collapsed:: true
								- 可变对象：添加到新的list中的是对象的引用，所以修改其两个list中都有的元素属性，会同步体现到两个列表中
								- 不可变对象：由于Integer是不可变对象，所有两个list中都有的元素，修改其中一个元素，不会同步体现在两个列表中
							- 通过Collections.addAll()方法进行添加
							- 使用Java8 Stream forEachOrdered()
						- 参考文章：https://www.baeldung.com/java-add-items-array-list
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/addmultipleitems
					- 移除列表的第一个元素
					  collapsed:: true
						- 在ArrayList中移除第一个元素
						  collapsed:: true
							- remove(0)
							- 缺点：ArrayList移除一个元素的时间复杂度是O(n)，因为他涉及到数组其余元素的位置移动
						- 在LinkedList中移除第一个元素
						  collapsed:: true
							- removeFirst()
							- LinkedList移除一个元素的时间复杂度是O(1)
						- 参考文章：https://www.baeldung.com/java-remove-first-element-from-list
						- 参考实现：JavaTrain/cn/bravedawn/collection/list/removefirstelement
					- 遍历列表
					  collapsed:: true
						- 六种方法：
						  collapsed:: true
							- 方法一：使用for循环
							- 方法二：增强的for循环
							- 方法三：使用Iterator
							- 方法四：使用ListIterator遍历
							- 方法五：使用Iterable.forEach()
							- 方法六：使用Stream.foreach()
						- 参考文章：https://www.baeldung.com/java-iterate-list
						- 参考实现：JavaTrain/cn/bravedawn/collection/list/iteratoroverlist
					- 两个列表的交集
					  collapsed:: true
						- 求两个字符串列表的交集
						  collapsed:: true
							- 使用Java8 Stream流操作进行处理
						- 求两个自定义对象列表的交集
						  collapsed:: true
							- 方法
							  collapsed:: true
								- 重写自定义类的equals方法，因为列表的contains方法就是基于equals方法实现的
								- 使用Java8 Stream流进行处理
						- 参考文章：https://www.baeldung.com/java-lists-intersection
						- 参考实现：JavaTrain/cn/bravedawn/collection/list/intersectiontwolists
					- 对列表中重复计算的元素进行计数
					  collapsed:: true
						- 六种方法
						  collapsed:: true
							- 方法一：通过使用Map.put()去遍历，该实现兼容所有的Java版本
							- 方法二：通过使用forEach()和Map.put()去遍历，该实现不兼容Java8之前的版本
							- 方法三：通过使用Map.compute()去遍历
							- 方法四：通过使用Map.merge()去遍历
							- 方法五：通过使用Stream API的Collectors.toMap()去遍历
							- 方法六：通过使用Stream API的Collectors.groupingBy() 和 Collectors.counting()去遍历
						- 参考文章：https://www.baeldung.com/java-count-duplicate-elements-arraylist#loop-with-mapmerge
						- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/list/countduplicateelements
					- 查找两个列表的不同
			- Set
			- Map
			  collapsed:: true
				- 背景
				  collapsed:: true
					- 为什么不用list而要用map呢
					  collapsed:: true
						- 因为性能，在一个未排序的list中查找一个特定值，需要的时间复杂度是O(n)；在一个已排序的list中查找的话需要的时间复杂度是O(logn)，例如使用二分搜索
						- 使用map的话插入和检索一个元素，需要的时间复杂度是O(1)
				- HashMap
					- 特点
					  collapsed:: true
						- Map是一种key-value映射表的数据结构
						- Map中不存在重复的key，因为放入相同的key，只会把原有的key-value对应的value给替换掉
						- Map中存储的映射关系是不保证顺序的
					- 基本操作
						- put
						- get
						- null可以作为键，null映射键值将会被放到下标为0的存储桶中
						- remove
						- 检查key或者value是否在映射中
						- Map的遍历
							- 方法一：通过循环遍历Map实例的keySet()方法返回的Set集合
							- 方法二：通过循环遍历Map实例的entrySet()方法返回的Set集合
						- 具体实现参考：JavaTrain/src/main/java/cn/bravedawn/collection/map/hashmap/HashMapExample.java
					- 关于key需要注意
					  collapsed:: true
						- 可以在HashMap中使用任何类作为键。为了使映射正常工作，我们需要为equals()和hashCode()提供一个实现
						- hashCode()和equals()只需要在我们希望用作映射键的类中重写
					- Java8新增的方法
					  collapsed:: true
						- forEach()
						- getOrDefault()
						- putIfAbsent()
						- merge()
						- compute()
						- 具体的实现参考：JavaTrain/src/main/java/cn/bravedawn/collection/map/hashmap/java8
					- HashMap的内部实现
					  collapsed:: true
						- 存储结构
						  collapsed:: true
							- 内部包含了一个 Entry 类型的数组 table。也就是我们说的桶数组。
							- Entry 存储着键值对。它包含了四个字段，从 next 字段我们可以看出 Entry 是一个链表。
							- 即数组中的每个位置被当成一个桶，一个桶存放一个链表。
							- HashMap 使用拉链法来解决冲突，同一个链表中存放哈希值和散列桶取模运算结果相同的 Entry。
						- HashMap中检索一个元素的方法
						  collapsed:: true
							- 方法一：遍历所有元素，找到和键匹配的元素返回。这种时间复杂度是O(n)
							- 方法二：使用HashMap的put()和get()方法，实现平均时间复杂度O(1)和空间复杂度O(n)
						- HashMap中put和get操作的实现
						  collapsed:: true
							- HashMap将元素存储在所谓的桶（bucket）中，桶的数量称为容量。
							- bucket的数据结构可能是列表或是平衡树。
							- 当我们向映射中添加一个元素时，将使用键的hashCode()方法来确定将存储该值的bucket。如果该桶已经包含一个值，会调用键对象的equals()方法判断桶内是否有相同键，若有则会覆盖原有的键所对应的value值；若没有则该值将被添加到属于该桶的列表(或树)中。如果负载因子大于映射的最大负载因子，则容量翻倍。
							- 当我们想从映射中获取一个值时，HashMap以相同的方式计算桶——使用hashCode()。然后遍历在该bucket中找到的对象，并使用键的equals()方法在链表上顺序查找，时间复杂度显然和链表的长度成正比。
						- HashMap中键的不变性
						  collapsed:: true
							- 在大多数情况下，我们应该使用不可变键，即就是要保证key的散列值不变。
							- 一旦键改变，我们就不再能够获得相应的值，而是返回null。这是因为HashMap用错误的hashcode找到错误的bucket，然后在错误的bucket中搜索。
						- 哈希碰撞
						  collapsed:: true
							- 要使其正确工作，相等的键必须具有相同的散列，然而，不同的键可以具有相同的散列。如果两个不同的键具有相同的散列，则属于它们的两个值将存储在同一个bucket中。在桶内，值存储在一个列表中，并通过遍历所有元素来检索。它的代价是O(n) ，这里的n指的是桶里键值对的大小。
							- 从Java 8(参见JEP 180)开始，如果一个桶包含8个或更多的值，则存储在一个桶内的值的数据结构将从链表更改为红黑树，这将使性能提高到O(log n)，这里的n指的是桶里键值对的大小。如果某个时刻桶中只剩下2到6个键值对时，则将回退回链表。
						- 容量和负载因子
						  collapsed:: true
							- 为了避免多个桶具有多个值，如果75%(负载系数)的桶变为非空的，则容量将翻倍。
							- 默认负载系数为75%，初始容量为16。两者都可以在构造函数中设置。
						- 底层代码解析：Java HashMap的底层实现
						- 具体的实现参考：JavaTrain/src/main/java/cn/bravedawn/collection/map/hashmap/internals
				- LinkedHashMap
				  collapsed:: true
					- 特点（与HashMap的区别）
					  collapsed:: true
						- 也接受空键和空值。
						- LinkedHashMap是通过哈希表和链表实现，增强了哈希映射的功能。
						- 除了默认大小为 16 的底层数组外，它还维护一个贯穿其所有条目的双向链表，为LinkedHashMap.Entry有两个名为before，after的指针，分别指向上一个和下一个条目。从而保证了元素的顺序。
						- 注意LinkedHashMap的这个链表定义了迭代的顺序，默认是元素的插入顺序（insertion-order）。
					- Access-Order LinkedHashMap
					  collapsed:: true
						- 在LinkedHashMap的构造函数中有一个accessOrder的参数，若该参数为true，则就会设置迭代顺序为 LRU(Least Recently Used)，即最近最少使用。
					- 性能
					  collapsed:: true
						- 基本操作：与HashMap相同，如果没有哈希冲突，map的基本操作（put、get、remove、containsKey）平均时间复杂度是O(1) 。但是由于维护双向链表的额外开销，LinkedHashMap的这种恒定时间性能可能会比 HashMap的恒定时间差一点。
						- 迭代：LinkedHashMap 的集合视图的迭代也需要类似于 HashMap的线性时间 O(n) 。但是，LinkedHashMap 在迭代过程中的线性时间性能优于 HashMap的线性时间。这是因为，对于LinkedHashMap，O(n) 中的 n 只是映射中的条目数，而与容量无关。而对于 HashMap，n 是容量和大小的总和，O(size+capacity)。
						- 负载因子和初始化容量：负载因子和初始容量的定义与 HashMap相同。但是请注意，对于 LinkedHashMap而言，为初始容量选择过高的值的成本没有 HashMap高，因为此类的迭代时间不受容量的影响。
						- 这里可以参考：底层代码解析：Java HashMap的底层实现
					- 并发
					  collapsed:: true
						- 与HashMap相同，LinkedHashMap也是不同步的。最好在创建时就使用Collections.synchronizedMap()方法将其变成一个同步的map。
					- 具体的实现参考：JavaTrain/src/main/java/cn/bravedawn/collection/map/linkedhashmap
				- TreeMap
				  collapsed:: true
					- 特点
					  collapsed:: true
						- 不允许空键，但可能包含许多空值。空键是不允许的，因为compareTo()或compare()方法会抛出一个NullPointerException
						- 因为TreeMap 树映射的属性，可以方便的获取 “最大的键”，“最小的键”，“大于或小于某个值的键”。
						- 可以自定义TreeMap的排序规则。
						- 不是线程安全的
					- 默认排序
					  collapsed:: true
						- 当TreeMap的键为整数时，默认顺序是按照整数键的升序顺序进行排序的
						- 当TreeMap的键为字符串时，默认顺序是按照字符串键的首字母的字母顺序进行排序的
					- 与HashMap和LinkedHashMap的区别
					  collapsed:: true
						- 存储不同：与HashMap和LinkedHashMap不同，TreeMap在任何地方都不使用散列原则，因为它不使用数组来存储它的条目。
						- 排序不同：HashMap映射不能保证存储的键的顺序，特别是不能保证这个顺序随着时间的推移保持不变，但是树映射可以保证键总是按照指定的顺序排序。
					- TreeMap的内部实现
					  collapsed:: true
						- TreeMap继承了AbstractMap类。实现了NavigableMap接口，它的内部工作基于红黑树的原则。
						- 红黑数是一个平衡二叉树，这个属性保证了像搜索、获取、放置和删除这样的基本操作需要的时间复杂度是O(log n)。
						- 红黑数的排序规则是由元素的自然顺序或构造时定义的比较器决定的。
				- WeakHashMap
				  collapsed:: true
					- Strong, Soft, and Weak References
					  collapsed:: true
						- Strong Reference
						  collapsed:: true
							- 强引用是我们在日常编程中使用的最常见的引用类型。
							- 任何具有指向它的强引用的对象都不适合进行GC。
							- 强引用的创建：Integer prime = 1;
						- Soft Reference
						  collapsed:: true
							- 一个有软引用指向的对象不会被垃圾回收，直到JVM绝对需要内存。
							- 我们将一个强引用对象a转换为软引用对象后，并将a置为null，此时对象a就有资格进行GC，但只在JVM绝对需要内存时才会被收集。
							- 软引用的创建：SoftReference<Integer> soft = new SoftReference<Integer>(prime);
						- Weak Reference
						  collapsed:: true
							- 只有被弱引用指向的对象会被垃圾回收，在这种情况下，GC不会等到它需要内存。
							- 我们将一个强引用对象a转换为软引用对象后，并将a置为null，此时对象a将在下一个GC周期中被垃圾回收，因为没有其他强引用指向它。
							- 弱引用的创建：WeakReference<Integer> soft = new WeakReference<Integer>(prime);
							- WeakReference类型的引用被用作WeakHashMap中的键。
					- WeakHashMap as an Efficient Memory Cache
					  collapsed:: true
						- 实验一：map中包含一个键值对，当把key的弱引用对象置为null后，调用gc后会自动触发垃圾回收，清空map。
						- 实验二：map中包含两个键值对，当把其中一个key的弱引用对象置为null后，调用gc后会自动触发垃圾回收，map会移除该key对应的键值对。
				- ConcurrentHashMap
				  collapsed:: true
					- 特点
					  collapsed:: true
						- ConcurrentHashMap是线程安全的。
						- ConcurrentHashMap中key和value是不允许存在null值的。
						- 在多线程环境下，ConcurrentHashMap的性能较好。
						- 包括size(), isEmpty(), containsValue()等聚合方法的结果仅在map未在其他线程中更新时才有用。
						- size()和mappingCount()的底层逻辑相同，但是size返回int值，mappingCount返回long值。
						- ConcurrentHashMap中的键没有排序。
				- ConcurrentSkipListMap
				  collapsed:: true
					- 参考文章：Guide to the ConcurrentSkipListMap
				- Hashtable
				  collapsed:: true
					- HashTable和HashMap的区别
					  collapsed:: true
						- 相同点
						  collapsed:: true
							- 快速失败的迭代
							- 不可预测的迭代顺序
						- 不同点
						  collapsed:: true
							- HashMap 不提供任何枚举，而 Hashtable 不提供快速失败的枚举
							- Hashtable 不允许空键和空值，而 HashMap 允许一个空键和任意数量的空值
							- Hashtable 的方法是同步的，而 HashMaps 的方法是不同步的
					- Java8提供的API
					  collapsed:: true
						- remove：移除一个条目，前提是他的value与预期的一致。
						- replece：替换一个条目，前提是他的value与预期的一致。
						- putIfAbsent：如果键不存在，就将他添加到map中。
						- computeIfAbsent：如果键不存在，就将mappingFunction运算的结果作为value，添加到map中。
						- computeIfPresent：若key对应的键值对存在，则将remappingFunction的运算结果作为value添加到map中。
						- compute：将remappingFunction函数的运算结果作为map的value。
						- merge：若键不存在，则将第二个参数作为其value；若键存在，则第三个参数remappingFunction的运算结果作为其新的value。
						- foreach：遍历map
						- replaceAll：
					- 参考文章
					  collapsed:: true
						- An Introduction to Java.util.Hashtable Class
				- EnumMap
				  collapsed:: true
					- 特点
					  collapsed:: true
						- EnumMap 是一个 Map 实现，它专门以 Enum作为其键。
						- EnumMap 是一个有序映射，插入的键值对会按照插入的顺序进行排列。
					- 构造函数
					  collapsed:: true
						- 1. EnumMap的构造函数的参数为 键的类型。
						- 2.可以将原有的EnumMap作为构造函数的参数，构造其副本。
						- 3. 如果有一个键是枚举的非空 Map，也可以作为EnumMap的构造函数的入参，从而构造他的副本。
					- 添加和检索元素
					  collapsed:: true
						- 添加：put
						- 检索：get
					- 检查元素是否存在
					  collapsed:: true
						- containsKey()
						- containsValue()
						- null可以作为EnumMap的value值
					- 移除元素
					  collapsed:: true
						- remove(key)：根据key移除一个元素。
						- remove(key, value)：只有根据键找到的键值对，其value值与指定的值相等时，才会移除。
					- 集合视图
					  collapsed:: true
						- 值视图：values()
						- 键视图：keySet()
						- 条目视图：entrySet()
						- 视图的易变性
						  collapsed:: true
							- 在原始map的修改会提现在子视图上面
							- 对子视图的修改也会体现在原始map上面
					- 参考实现：JavaTrain/src/main/java/cn/bravedawn/collection/map/enummap
					- 参考文章：A Guide to EnumMap
				- TreeMap和HashMap的比较
				  collapsed:: true
					- 不同点
					  collapsed:: true
						- 内部实现
						  collapsed:: true
							- HashMap是由桶（bucket，数组）和链表（或是红黑树）组成，根据key值的哈希确认键值对存储的桶，然后将键值对添加到链表或是红黑树中。
							- TreeMap扩展了AbstractMap类并实现了NavigableMap接口。TreeMap将键值对元素存储在红黑树中，这是一种自平衡二叉搜索树。
						- 排序
						  collapsed:: true
							- HashMap对元素的排序方式不做保证，在迭代它的键和值时，顺序是随机的。
							- TreeMap中元素是按照key的自然顺序进行排序的，或是可以使用Comparator或Comparable来定义Map中元素的排列顺序。
						- null
						  collapsed:: true
							- HashMap最多允许存储一个空键和多个空值。
							- TreeMap不允许空键，但可能包含许多空值。
					- 性能分析
						- HashMap
							- HashMap为大多数操作(如add()、remove()和contains())提供了预期的恒定时间性能O(1)。因此，它明显比TreeMap快。
							- 我们大概知道在我们的集合中要维护多少项，不希望以自然顺序提取项。在这种情况下，HashMap是我们的最佳选择，因为它提供恒定的插入、搜索和删除时间。
						- TreeMap
							- 对于大多数操作，如add()，remove()和contains()， TreeMap提供了O(log(n))的性能。
							- TreeMap可以节省内存(与HashMap相比)，因为它只使用保存项目所需的内存量，而不像HashMap使用连续的内存区域。
							- 为了保持预期的性能，树应该保持它的平衡，这需要相当多的努力，因此使实现复杂化。
							- 我们应该在以下情况使用TreeMap：
								- 必须考虑到内存限制
								- 我们不知道要在内存中存储多少项
								- 我们希望以自然顺序提取对象
								- 如果需要不断进行添加和删除操作
								- 我们愿意接受O(log n)的搜索时间
					- 相同点
						- 键唯一性
						  collapsed:: true
							- TreeMap和HashMap都不支持重复键。如果添加，它将覆盖前一个元素(没有错误或异常)。
						- 并发访问
						  collapsed:: true
							- 两个Map实现都不是同步的，我们需要自己管理并发访问。
							- 当多个线程并发访问它们并且其中至少有一个线程修改它们时，两者都必须在外部同步。
							- 我们必须显式地使用Collections.synchronizedMap(mapName)来获得所提供映射的同步视图。
						- Fail-Fast Iterators
							- 迭代器创建后，如果Map以任何方式和任何时间被修改，迭代器将抛出ConcurrentModificationException异常。
							- 此外，我们可以使用迭代器的remove方法在迭代过程中更改Map。
					- 如何选择
					  collapsed:: true
						- 如果我们想保持条目的排序，我们应该使用TreeMap。
						- 如果我们优先考虑性能而不是内存消耗，我们应该使用HashMap。
						- HashMap可以使用initialCapacity和loadFactor进行调优，这对于TreeMap是不可能的。
						- 我们可以使用LinkedHashMap，如果我们想保持插入顺序，同时受益于恒定的访问时间。
				- 选择一个正确的Map
					- HashMap是一种提供快速存储和检索操作的通用映射实现。然而，由于条目的排列混乱、无序，它还不够完善。因为受容量（底层数据）和数据条目数量的影响，迭代场景下性能不佳。
					- LinkedHashMap具有哈希映射的良好属性，并为条目增加了顺序。在有大量迭代的情况下，它的性能更好，因为只考虑条目的数量，而不考虑容量。
					- TreeMap通过提供对键应该如何排序的完全控制，将排序提升到下一个层次。另一方面，它提供的总体性能比其他两个备选方案差。
					- LinkedHashMap减少了哈希映射排序中的混乱，而且其性能优于TreeMap。
				- 并发Map
				  collapsed:: true
					- 背景
					  collapsed:: true
						- HashMap不是线程安全的。
						- Hashtable通过同步操作提供线程安全。尽管Hashtable是线程安全的，但它的效率并不高。
						- Collections.synchronizedMap()也没有提供很好的性能。
					- ConcurrentMap
					  collapsed:: true
						- ConcurrentMap是Map接口的扩展。它旨在为解决吞吐量与线程安全之间的协调问题提供一个结构和指导。
						- Map接口的默认实现被覆盖，禁用null键/值支持：
						  collapsed:: true
							- getOrDefault：如果一个键在map中不存在，通过设置他的默认值来获取
							- forEach
							- replaceAll
							- computeIfAbsent：如果键不存在或键对应的值为null，将mappingFunction的执行结果设为value，若执行结果为null，该键值对会被移除
							- computeIfPresent：如果键存在，将remappingFunction的执行结果设为value，如执行结果为null，该键值对会移除
							- compute
							  collapsed:: true
								- 若key对应的键值对是存在的，若value的计算为null，移除该key对应的键值对
								- 若key对应的键值对不存在，若value的计算为null，原有的map保持不变，该key也不会被添加到map中
							- merge
						- Map接口没有默认实现的方法也被覆盖，以支持原子性：
						  collapsed:: true
							- putIfAbsent
							- remove
							- replace(key, oldValue, newValue)
							- replace(key, value)
						- 参考
						  collapsed:: true
							- A Guide to ConcurrentMap
					- ConCurrentHashMap
					- ConcurrentNavigableMap
					  collapsed:: true
						- 特点
						  collapsed:: true
							- 需要对键进行排序的情况，我们可以使用 ConcurrentSkipListMap，它是 TreeMap 的并发版本。
					- ConcurrentSkipListMap
					- Hashtable
				- 不可变Map
				  collapsed:: true
					- Java实现不可变map
					  collapsed:: true
						- `Collections.unmodifiableMap(mutableMap)`，不能直接修改，但是可间接修改
					- Guava实现不可变map
					  collapsed:: true
						- `copyOf()`：直接复制原有可变map
						- `builder()`：即可以直接复制原有可变map，也可以添加新的元素
						- `of()`：可以添加多对键值构造map
						- 特点：生成的不可变map，即不能直接修改也不能间接修改
			- Queue
			- Fail-fast and Fail-safe
			  collapsed:: true
				- Fail-fast
				  collapsed:: true
					- 当我们使用 Fail-fast 迭代器时，如果在线程迭代集合时从集合中添加或删除元素，它会立即抛出 ConcurrentModificationException。
					- 案例
						- HashMap 中的迭代器
						- ArrayList 中的迭代器
				- Fail-safe（Non-Fail-fast）
				  collapsed:: true
					- 如果线程在迭代集合时从集合中不抛出ConcurrentModificationException异常，我们称为Non-Fail-fast或者是Fail-safe。
					- Fail-safe迭代器会创建原始集合或对象数组的副本，并迭代该复制的集合。 在迭代器中所做的任何结构修改都会影响复制的集合，而不是原始集合。 因此，原始集合在结构上保持不变。
					- 案例
						- ConcurrentHashMap 上的迭代器
						- CopyOnWriteArrayList 上的迭代器
				- 具体实践
				  collapsed:: true
					- JavaTrain/src/main/java/cn/bravedawn/collection/failsafe
				- 参考文章
				  collapsed:: true
					- [Fail-fast and Fail-safe in Java](https://www.javatpoint.com/fail-fast-and-fail-safe-in-java)
		- 并发
		- IO
		  collapsed:: true
			- 字节流
			  collapsed:: true
				- 特点
				  collapsed:: true
					- 所有字节流类都继承于 `InputStream` 和 `OutputStream` 。
					- 不同类型字节流的使用方式差别不大，主要是构造方法有区别。
					- 字节流应该用于最原始的I/O，其他流都是建立在字节流之上的。
				- 派生类
				  collapsed:: true
					- 专门用于文件I/O的字节流类：*FileInputStream**和**FileOutputStream*
				- 具体实践
					- JavaTrain/src/main/java/cn/bravedawn/io/bytestreams/CopyBytes.java
				- 参考文章
					- [Byte Streams](https://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html)
			- 字符流
			  collapsed:: true
				- 特点
				  collapsed:: true
					- 所有字符流类都派生自 `Reader` 和 `Writer`。
					- Java 平台使用 Unicode 约定存储字符值。 字符流 I/O 自动将此内部格式与本地字符集相互转换。
					- 使用流类完成的输入和输出自动转换为本地字符集或从本地字符集转换。
					- 使用字符流代替字节流的程序会自动适应本地字符集并为国际化做好准备。
					- 字符流通常是字节流的“包装器”。 字符流使用字节流来执行物理 I/O，而字符流处理字符和字节之间的转换。 例如，FileReader 使用 FileInputStream，而 FileWriter 使用 FileOutputStream。
					- 有两种通用的字节到字符“桥接”流：InputStreamReader 和 OutputStreamWriter。 当没有满足您需要的预打包字符流类时，使用它们来创建字符流。
					- 字符 I/O 通常以比单个字符更大的单元出现。 一个常见的单位是行：一串字符，末尾有行终止符。 行终止符可以是回车/换行序列（“\r\n”）、单个回车（“\r”）或单个换行（“\n”）。具体可以参考`System.lineSeparator()`，他返回特定操作系统的换行符。
				- 派生类
					- 专门用于文件 I/O 的字符流类：*FileReader 和 FileWriter*。
				- 具体实践
					- JavaTrain/src/main/java/cn/bravedawn/io/charaterstreams/CopyCharacters.java
					- JavaTrain/src/main/java/cn/bravedawn/io/charaterstreams/CopyLines.java
			- 缓冲流（buffered streams）          
			  collapsed:: true
				- 背景
					- 使用未缓冲的IO操作每个读或写请求都由底层操作系统直接处理。这会降低程序的效率，因为每个这样的请求通常会触发磁盘访问、网络活动或其他一些相对昂贵的操作。
					- **为了减少这种开销，Java 平台实现了缓冲的 I/O 流**。
				- 实现原理
					- 缓冲的输入流从称为缓冲区的内存区域读取数据; 只有当缓冲区为空时才调用本机输入 API。
					- 缓冲的输出流将数据写入缓冲区，并且只有在缓冲区已满时才调用本机输出 API。
				- 四个缓冲流类用于包装未缓冲流
					- `BufferedInputStream` 和 `BufferedOutputStream` 创建缓冲字节流。
					- `BufferedReader` 和 `BufferedWriter` 创建缓冲字符流。
				- 刷新缓冲区
					- 作用：在临界点写出缓冲区通常是有意义的，而不需要等待它被填满。这就是所谓的冲洗缓冲区。也就是说在开发人员认为需要调用底层API将缓冲区的内容进行写入时调用。
					- 注意点：
						- 一些缓冲输出类支持自动刷新，由可选的构造函数参数指定。
							- 例如，在每次调用`println()`或`format()`时，自动刷新`PrintWriter`对象都会刷新缓冲区。
						- `fluash()`方法任何输出流都可以调用，但是只对缓冲流有效果。
					- 具体实践：cn/bravedawn/io/bufferedstreams/CopyCharacters.java
			- Scanner          
			  collapsed:: true
				- `Scanner` 类型的对象有助于将格式化的输入分解为标记，并根据标记的数据类型转换单个标记。
				- `Scanner`**还支持所有**Java**语言的基本类型**(char**除外**)以及**BigInteger**和**BigDecimal**的令牌。在读取的使用提供了一系列的`nextInt()`、`nextDouble()`...方法
				- 支持读取用户输入
					- 使用next()方法读取用户的键盘输入的字符串
						- next()方法遇到空格就会结束读取
					- 使用nextLine()读取用户的输入的字符串
						- nextLine()方法以Enter为结束符
				- 具体实践：cn/bravedawn/io/scanning
			- Formatting          
			  collapsed:: true
				- 在Java中通过使用java.util.Formatter实现字符串的格式化。
				- 可以通过流对象是PrintWriter(字符流类)或PrintStream(字节流类)的实现格式化操作。
				- `print()`和`println()`以标准方式格式化单个值。
				- `format()`基于格式字符串格式化几乎任何数量的值，有许多精确格式化的选项。
				- format说明符
					- 一般语法：
					  
					    ```
					    %[argument_index$][flags][width][.precision]conversion
					    ```
						- argument_index：参数索引
						- flags：用于修改输出格式的标识
						- width：宽度
						- .precision：精度
				- 对于日期/时间表示
					- 一般语法：`%[argument_index$][flags][width]conversion`
			- 创建文件
			  collapsed:: true
				- 推荐使用Java 7 nio Files.write 来创建和写入文件，因为它有更简洁的代码并自动关闭打开的资源。
				- 实现
					- `Files.newBufferedWriter` (Java 8)
					- `Files.write` (Java 7)
					- `PrintWriter`
					- `File.createNewFile`
					- `Files.writeString`（Java11）
					- `FileOutputStream` 可以将原始字节写入文件，比如图片。
			- 读取文件
			  collapsed:: true
				- 新的 Java 8 `Files.lines` 在读取小型或大型文本文件方面表现良好，返回一个 Stream（灵活类型并支持并行），自动关闭资源，并且有一行干净的代码。
				- 实现
					- `Files.lines`, return a `Stream` (Java 8)
					- `Files.readString`, returns a `String` (Java 11), max file size 2G.
					- `Files.readAllBytes`, returns a `byte[]` (Java 7), max file size 2G.
					- `Files.readAllLines`, returns a `List<String>` (Java 8)
					- `BufferedReader`, a classic old friend (Java 1.1 -> forever)。
					  collapsed:: true
						- Java BufferedReader 类用于从基于字符的输入流中读取文本。 它可以用于通过 readLine() 方法逐行读取数据。 它使性能快速。 它继承了Reader类。
					- `Scanner` (Java 1.5)
					- `BufferedInputStream`
					  collapsed:: true
						- Java BufferedInputStream 类用于从流中读取信息。 它内部使用缓冲机制来提高性能。
			- 构建文件路径
			  collapsed:: true
				- 使用*使用 **File.separator **或 **System.getProperty("file.separator")*
				- 使用新的**File() API**来构造文件路径
				- 检查系统操作系统并手动创建文件路径
			- 文件权限
				- 检查文件的权限
				  collapsed:: true
					- file.canExecute(); – return true, file is executable; false is not.
					- file.canWrite(); – return true, file is writable; false is not.
					- file.canRead(); – return true, file is readable; false is not.
				- 设置文件的权限
				  collapsed:: true
					- file.setExecutable(boolean); – true, allow execute operations; false to disallow it.
					- file.setReadable(boolean); – true, allow read operations; false to disallow it.
					- file.setWritable(boolean); – true, allow write operations; false to disallow it.
			- 追加内容到文件
			  collapsed:: true
				- 下面几种方式的话，比较推荐`Files.writeString`和Apache的`FileUtils`。
				- `Files.write` – Append a single line to a file, Java 7.
				- `Files.write` – Append multiple lines to a file, Java 7, Java 8.
				- `Files.writeString` – Java 11.
				- `FileWriter`
				- `FileOutputStream`
				- `FileUtils` – Apache Commons IO.
			- 检查一个文件或目录是否存在
			- Java读取文件到字符串
			  collapsed:: true
				- Java使用BufferedReader将文件读取为String
				- 使用FileInputStream在Java中将文件读取为String
				- Java使用Files类将文件读取为字符串
				- 使用Scanner类将文件读取到String
				- Java使用Apache Commons IO FileUtils类将文件读取为字符串
				- 参考实现：JavaTrain/src/main/java/cn/bravedawn/io/file/readfiletostring
				- 参考博客：[java读取文件到字符串_Java读取文件到字符串](https://blog.csdn.net/cunchi4221/article/details/107471069)
			- Java读取项目目录下的文件/路径
			  collapsed:: true
				- 方法一：
				  ```Java
				  // 推荐：获取文件路径
				  File file = new File(Thread.currentThread().getContextClassLoader().getResource("doc/test.txt").getPath());
				  ```
				- 方法二：
				  ```Java
				  URL resource = ClassLoader.getSystemClassLoader().getResource(filename);
				  ```
			- Java InputStream to String
				- Converting With Java 9 –  *InputStream.readAllBytes()*
				- 参考文章：[Java InputStream to String](https://www.baeldung.com/convert-input-stream-to-string)
		- JVM
		  collapsed:: true
			- Java的内存区域
				- Java虚拟机定义了在程序执行期间使用的各种运行时数据区域。其中一些数据区域是在Java虚拟机启动时创建的，只有在Java虚拟机退出时才会销毁。其他数据区域是每个线程。每个线程的数据区域在线程创建时创建，在线程退出时销毁。关于运行时数据区可以用以下图形来表示：
				  ![JVM运行时数据区.png](../assets/JVM运行时数据区_1680092970600_0.png)
				- 运行时数据区域
					- 程序计数器
						- 作用
						  collapsed:: true
							- 执行字节码的行号指示器。
							- 通过改变计数器的值，来选取下一条需要执行的字节码指令。
					- Java虚拟机栈
						- 作用
							- Java虚拟机栈描述的是Java方法执行的内存模型。说通俗点就是存储栈帧的。
							- Java中每个方法执行的同时会创建一个栈帧（Stack Frame）用于存储局部变量比表、操作数栈、动态链接、方法返回值等信息。
							- 每一个方法调用直至执行完成的过程，就对应着一个栈帧在虚拟机中入栈和出栈的过程。
					- 本地方法栈
						- 作用：与Java虚拟机栈不同，本地方法栈描述的是native方法执行的内存模型。
					- Java堆
						- 作用：用来存储应用系统创建的对象和数组。
						- 区域划分
							- 区域图
							  ![JVM堆的区域划分.webp](../assets/JVM堆的区域划分_1680093136228_0.webp)
							- 元空间（Metadata Space，JDK1.8之前叫永久代）：像一些方法中的操作临时对象等，JDK1.8之前是占用JVM内存，JDK1.8之后直接使用物理内存
							- 新生代（年轻代）：新对象和没达到一定年龄的对象都在年轻代
								- Eden Space：也叫伊甸区
								- Servivor：两个存活区
							- 老年代：被长时间使用的对象，老年代的内存空间应该要比年轻代更大
					- 方法区
					  collapsed:: true
						- 作用：用来保存加载的类的结构信息，包括类信息、常量、静态变量、及时编译期编译后的代码等数据
						- 运行时常量池
						  collapsed:: true
							- 是方法区的一部分
							- 作用：用于存放Class文件中的常量池信息，即存放编译期生成的各种字面量和符号引用。
					- 直接内存
					  collapsed:: true
						- 作用：支持NIO等功能，可以使用Native函数库直接分配堆外内存，用来提高性能。
				- JVM参数
					- `-Xms`：初始堆大小，默认物理内存的1/64。
					- `-Xmx`：最大堆大小，默认物理内存的1/4。
					- `-Xmn`：堆内新生代的大小。通过这个值也可以得到老生代的大小：-Xmx减去-Xmn。
					- `-XX:SurvivorRatio`：Eden和Survivor区的空间比例
					- `-XX:PermSize=10m`
					  collapsed:: true
						- 配置JVM初始分配的非堆内存，也就是方法区的内存大小
						- 堆内存是开发人员用的，而非堆内存是虚拟机用的
						- 在jdk8被废除
					- `-XX:MaxPermSize=10m`
					  collapsed:: true
						- JVM最大允许分配的非堆内存，按需分配
					- `-verbose:gc`：用于垃圾收集时的信息打印。
					- `-XX:+PrintGCDetails`：打印垃圾回收详细日志。已废弃，建议使用`-Xlog:gc*`。
					- `-Xlog:gc*`：打印GC详细信息。
					- `-XX:+UseSerialGC`：虚拟机运行在Clint模式下的默认值，打开此开关后，使用Serial + Serial Old的收集器组合进行内存回收。
				- 虚拟机对象
					- 对象的创建
						- **类加载检查**：虚拟机遇到一条new指令时，首先将去检查这个指令的参数是否能在常量池中定位到一个类的符号引用，并且检查这个符号引用代表的类是否已被加载、解析和初始化过。如果没有，那必须先执行相应的类加载过程。
						- **创建时机**：在类加载检查通过后，接下来虚拟机将为新生对象分配内存。对象所需内存的大小在类加载完成后便可完全确定，为对象分配空间的任务等同于把一块确定大小的内存从Java堆中划分出来。
						- 内存空间分配的方式
							- 分配方式选择的原则：是由Java堆是否规整决定的。
							- 指针碰撞
								- 适用场景：适用于Java堆的内存是规整的
								- 具体实现：Java堆的内存已经使用过的放一边，还没用的放另一边，中间则是一个指针，若要为新的对象分配内存，则只需要将指针移动相应的位置即可。
							- 空闲列表
								- 适用场景：适用于Java对的内存是不规整的
								- 具体实现：使用一个列表来登记内存的使用情况，如果要为新的内存分配空间，只需要在列表上面找到一块大小合适的内存空间分配给这个对象，并更新列表上的记录。
						- 内存分配的原子性问题
							- 背景：存在一种情况，要给对象A分配内存时，对象B也同时使用了原来要分给对象A的内存
							- 解决方法
								- 方式一：虚拟机采用CAS配上重试机制保证内存分配操作的原子性
								- 方式二：将内存分配的动作按照线程划分到不同的空间去进行，也就是说预先分配内存给线程，让线程自己在自己的内存空间上做分配，与其他线程互不影响。
									- 分配给线程的这块空间我们称之为：本地线程分配缓冲（Thread Local Allocation Buffer，简称TLAB）
						- 对象的内存布局
							- 对象头
							  collapsed:: true
								- 第一部分：存储对象自身的运行时数据
								  collapsed:: true
									- 主要数据（Mark Word）
									  collapsed:: true
										- 哈希码
										- GC分代年龄
										- 锁状态标志
										- 线程持有的锁
								- 第二部分：类型指针，即对象指向它的类元数据的指针
								  collapsed:: true
									- 作用：通过这个指针来确定这个对象是那个类的实例
								- 第三部分：记录数组长度的数据（还部分是**数组对象**特有的）
							- 实例数据
								- 作用：该部分存储的是程序代码中所定义的各种类型的字段内容，也就是这个对象的属性字段数据
							- 对齐填充
								- 作用：因为JVM要求对象的起始地址必须是8字节的整数倍，也就是说对象的大小必须是8字节的整数倍，主要存储的是占位符，用来补全空间。
						- 对象的访问定位
							- 访问和定位堆中对象具体位置的方法
								- 使用句柄
									- 使用句柄，Java堆中会划分出一块内存来作为句柄池，reference中存储句柄的地址，句柄中存储对象的实例数据和类型数据的具体地址信息
									  ![通过句柄访问对象.png](../assets/通过句柄访问对象_1677675705329_0.png)
									- 优点：reference中存储的是稳定的句柄，对象被移动（垃圾回收时会移动对象）时只会改变句柄中的实例数据指针，而reference本身不需要修改。
									- 缺点：访问对象需要经过两次指针定位，速度慢。
								- 使用指针
									- Java堆中会直接存放访问类元数据的地址，reference存储的就直接是对象的地址
									  ![通过指针访问对象.png](../assets/通过指针访问对象_1677675777115_0.png)
									- 优点：速度快，节省了一次指针定位的时间开销。
									- 缺点：对象被移动后，需要修改reference中的指针。
				- OutOfMemoryError异常
				  collapsed:: true
					- Java堆的溢出
					  collapsed:: true
						- 具体的代码演示：jvm-demo/src/main/java/cn/bravedawn/jvm/memory/HeapOutOfMemoryError.java
						- 将Xms和Xmx设置的值相同是为了避免堆自动扩展。
						- 堆内存溢出问题的排查方法
						  collapsed:: true
							- 通过MAT工具查看堆转储快照，分析泄露对象到GC Roots的引用链，定位泄露代码的位置。
							- 检查虚拟机堆参数（-Xmx和-Xms），与机器物理内存比较，看是否能够调大。
							- 从代码上检查是否存在某些对象生命周期较长，持有状态时间过长的情况。
					- 虚拟机栈和和本地方法栈溢出
					  collapsed:: true
						- 虚拟机其实不区分虚拟机栈和本地方法栈。
						- 栈容量只由-Xss参数设置，-Xoss参数（设置本地方法栈）其实是无效的配置。
						- 实验
						  collapsed:: true
							- 单线程内存溢出实验
							  collapsed:: true
								- 具体实践：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/StackOverflowErrorExample.java
								- 结论：在单个线程，无论是由于栈帧太大还是虚拟机栈容量过小，当内存无法分配的时候，都会抛出StackOverflowError异常。
							- 多线程内存溢出实验
							  collapsed:: true
								- 具体实践：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/StackOverflowErrorExample2.java
								- 结论：多线程实验会造成操作系统假死，建议不要尝试。按照书上的说法会出现OutOfMemoryError异常。
					- 方法区和运行时常量区溢出
					  collapsed:: true
						- 这里主要是以String的intern方法展开讨论的，通过不断的将字符串放入常量池，从而增大方法区的大小，来实现溢出。
						- 实验一：方法区和运行时常量区溢出的具体实践：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/RuntimeConstantPoolOOM.java
						- 实验二：这里我们着重的讨论了 ((64043de8-605f-43aa-a7b0-a711a39e4d4a)) 方法在jdk6和jdk7下的不同表现，具体实践参考：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/RuntimeConstantPoolOOM2.java
						- 实验三：借助Cglib生产大量的类，从而实现方法区溢出的效果，具体参考：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/JavaMethodAreaOOM.java
					- 本机直接内存溢出
					  collapsed:: true
						- 实验：通过**Unsafe**实例进行内存分配，使用直接内存导致溢出，具体实践：jvm/jvm-demo/src/main/java/cn/bravedawn/jvm/memory/DirectMemoryOOM.java
			- 垃圾回收器
				- 相关概念
					- 根据对象的存活周期不同将内存分为新生代、老年代
					- 新生代
						- 定义：年轻代用来存放新近创建的对象堆内存空间。
						- 特点
							- 每次垃圾回收都会有大量的对象死去，只有少量存活
							- 有老年代为新生代进行内存分配担保
					- 老年代
					  id:: 640457c7-910c-4bea-bb1d-de5d2dd61ae0
						- 定义：老年代用来存放存活时间久的对象的堆内存空间。
						- 特点
							- 对象存活率高
							- 没有额外的内存为老年代进行内存分配担保
					- 永久代
					  id:: 64045857-a3d0-48e0-b083-94db4c2e7263
					  collapsed:: true
						- 定义：永久代不属于堆内存，是方法区的一种实现，用来存放加载的类的结构信息，包括类信息、常量、静态变量、及时编译期编译后的代码等数据。
					- 吞吐量（Throughput）
					  id:: 6405ef3b-98b6-4356-bc2e-85a1a75e8dc0
					  collapsed:: true
						- 定义：CPU用于运行用户代码的时间与CPU总消耗时间的比值
						- 公式：吞吐量 = 运行用户代码的时间 / (运行用户代码的时间 + 垃圾收集的时间)
					- Ende区
						- **Eden Space**字面意思是伊甸园，对象被创建的时候首先放到这个区域，进行垃圾回收后，不能被回收的对象被放入到空的survivor区域。
					- Survivor区
						- **Survivor Space**幸存者区，用于保存在eden space内存区域中经过垃圾回收后没有被回收的对象。
						- Survivor有两个，分别为To Survivor、 From Survivor，这个两个区域的空间大小是一样的。
					- Full GC/Major GC
						- 是指发生在老年代的GC，出现了Major GC，经常伴随着一次Minor GC，回收速度比较慢。
					- Minor GC
						- 也称为新生代GC，**新生代(新生代分为一个 Eden区和两个Survivor区)的垃圾收集叫做 Minor GC**。Minor GC非常频繁，一般回收速度也很快。
				- 什么是垃圾回收：简单说就是内存中已经不在被使用到的内存空间就是垃圾。
				- 判断对象可回收的方法
				  id:: 640442e6-c01a-4193-a8c4-d43829e17969
				  collapsed:: true
					- 引用计数法
						- 原理：给对象添加一个引用计数器，有访问就加1，引用失效就减1。
						- 优点：实现简单、效率高
						- 缺点：不能解决对象之间循环引用的问题
					- 可达性分析算法（根搜索算法/GC Root Tracing）
					  id:: 64044e66-3742-4a9f-b08c-e25b45d4c214
						- 从根（GC Roots）节点向下搜索对象节点，搜索走过的路径称为引用链（Reference Chain），当一个对象到根之间没有连通的话，则该对象不可用。
						- Java语音中可作为GC Roots的对象包括：
							- 虚拟机栈（栈帧局部变量）中引用的对象
							- 方法区类静态属性引用的对象
							- 本地方法栈中JNI（即一般说的Native方法）引用的对象
					- 引用
						- Java对引用的狭义定义：如果 ((64043de7-b2f9-4db7-b4f3-574c88698635))的数据中存储的数值代表的是另外一块内存的起始地址，就称这块内存代表着一个引用。
						- 引用的扩充，又分为
							- 强引用-Strong Reference
								- 描述在程序代码中是普遍存在的对象。
								- 只要强引用存在，垃圾收集器就永远不会回收掉被引用的对象。
							- 软引用-Soft Reference
								- 描述还有用但并非必需的对象。
								- jdk1.2提供了SoftReference类来实现软引用。
							- 弱引用
								- 描述非必需对象。
								- jdk1.2提供了WeakReference类来实现弱引用。
							- 虚引用
								- 也称为幽灵引用或者幻影引用。
								- 设置虚引用的唯一目的是能在这个对象被收集器回收时收到一个系统通知。
								- jdk1.2之后，提供了PhantomReference类来实现虚引用。
					- 方法区的回收
						- 方法区回收的主要内容
							- 废弃常量
							- 废弃无用的类
						- 要求虚拟机具备类卸载功能的使用场景，来保证 ((64045857-a3d0-48e0-b083-94db4c2e7263)) 不会溢出
							- 在大量使用cglib、反射、动态代理等字节码框架
							- 动态生成JSP以及OSGi等频繁自定义ClassLoader的场景
				- 垃圾回收算法
				  collapsed:: true
					- 垃圾回收算法是内存回收的方法论
					- 标记-清除算法
					  id:: 640454c1-d575-4471-8253-b259cfdfd0d0
						- 算法思想
							- 分为标记和清除两个阶段，这里的标记就是 ((640442e6-c01a-4193-a8c4-d43829e17969))
							- 先标记出所有需要回收的对象
							- 标记完成后统一进行回收
						- 缺点
							- 标记和清除的效率都不高
							- 标记清除之后会产生大量不连续的内存碎片
					- 复制算法
					  collapsed:: true
						- 算法思想
							- 将可用内存分为大小相同AB块
							- 每次只使用其中的一块，比如A，另一块不动
							- 当A块的内存用完了，就将还存活的对象复制到B块上
							- 将A块上已经使用过的内存全部清除掉，只对半块内存进行回收
						- 优点
							- 实现简单，运行效率高
							- 不会产生内存碎片
						- 缺点
							- 将可用内存缩小为原来的一半，内存的使用率低
						- 复制算法在现代商业虚拟机的使用
						  id:: 64045bdf-5eee-44ca-bede-49e6e84d4ed3
							- 将内存分配一块较大的Eden空间和两块较小的Survivor空间
							- 每次使用只使用Eden和一块Survivor空间
							- 当回收时，将Eden区和刚才使用的Survivor区还存活的对象一次性复制到另一个Survivor空间上。若此时另一个Survivor空间内存不足时，将通过**分配担保机制**将这些存活的对象分配到 ((640457c7-910c-4bea-bb1d-de5d2dd61ae0)) 上（也就是说老年代在这里扮演了担保人的角色，当另一个Survivor空间内存不足时，可是使用老年代的内存）
					- 标记-整理算法
						- 背景：复制算法在对象存活率较高时需要进行频繁的复制操作，效率较低。更为关键的是如果采用 ((64045bdf-5eee-44ca-bede-49e6e84d4ed3))这种方式需要额外的空间进行分配担保，以便于应对所有对象都100%存活的极端情况。
						- 算法思想
							- 标记阶段与 ((640454c1-d575-4471-8253-b259cfdfd0d0))的一样
							- 不直接对可回收对象进行清除，而是将所有存活的对象**移动并整理**到另一端内存
							- 清除到原来那一端内存上的可回收对象
					- 分代收集算法
						- 算法思想
							- 针对新生代采用复制算法
							- 针对老年代采用标记-清除或是标记-整理算法
				- HotSpot的算法实现
				  collapsed:: true
					- 枚举根节点
						- GC停顿（Stop the world）
							- 在进行GC时需要执行用户代码的线程暂停工作，由虚拟机进行垃圾回收，这段时间称为GC停顿
						- 枚举根节点（GC Roots）存在的问题
							- 一查找根节点需要消耗很多的时间
								- HotSpot采用一组称为OopMap的数据结构来解决这个问题，在类加载完成时就会将对象的类型和偏移量数据记录下来。
								- JIT在编译过程中也会特定位置记录下栈和寄存器中引用的位置。
							- 二GC停顿
						- OopMap
							- 背景：枚举根节点耗时较长
							- Oop (ordinary object pointer) 普通对象指针
							- Oopmap就是存放这些指针的map
							- OopMap 用于枚举GC Roots，记录栈中引用数据类型的位置。
					- 安全点
						- 背景：
							- 在方法执行的过程中， 可能会导致引用关系发生变化，那么保存的OopMap就要随着变化。如果每次引用关系发生了变化都要去修改OopMap的话，这又是一件成本很高的事情。所以这里就引入了安全点的概念。
						- 定义
							- 程序执行时能停顿下来进行GC的位置，称为安全点。
							- 在OopMap预先选定的一些位置，在这些位置去修改OopMap。这些特定的点就是SafePoint（安全点）
						- 目的：为了高效的修改OoppMap，提高GC的效率。
						- 安全点选取的原则：是否具有让程序长时间执行的特征。满足这种特征的是指令序列复用，比如方法调用、循环跳转、异常跳转等
						- 如何让用户线程（排除执行JNI调用的线程）全部都执行到安全点进行停顿
							- 抢先式中断
								- 在GC发生时，将全部用户线程中断，如果有线程的中断没有在安全点上，则让该线程继续执行，直到到安全点上。
							- 主动式中断
								- 设置一个标志，每个线程执行时会主动的轮训这个标志，如果发现标志为真时就自己中断挂起。轮训标志和安全点事重合的。
					- 安全区
						- 目的：解决在程序执行时，线程因没有分配到CPU时间，从而无法响应JVM的中断请求，导致无法进行GC。
						- 定义：安全区域是指在一段代码片段中，引用关系不会再发生改变，这个区域的任何位置开始GC都是安全的。
				- 垃圾收集器
				  collapsed:: true
					- 垃圾收集器是内存回收的具体实现。
					- 垃圾收集器按照收集内存区域的不同，分为老年代收集器和新生代收集器两种。两种不同的收集器可以组合使用
					- 垃圾收集器的选择
					  collapsed:: true
						- 停顿时间短
						  collapsed:: true
							- 这种收集器适合需要和用户交互的程序使用，良好的响应速度能提升用户的体验
						- 吞吐量大
						  collapsed:: true
							- 这种收集器适合高效利用CPU时间，尽快完成运算任务的虚拟机，适合后台运算但不需要太多交互的任务
					- 新生代收集器
					  collapsed:: true
						- Serial收集器
						  collapsed:: true
							- 是一个单线程收集器
							- 只会使用一个CPU或是一条收集线程去完成垃圾的回收工作
							- 在垃圾回收时，必须暂停其他所有工作线程，直到他收集结束
							- 采用**复制算法**
							- 使用场景：虚拟机运行在Client模式
							- 优点：简单高效
						- ParNew收集器
						  collapsed:: true
							- Serial收集器的多线程版本
							- 是一个并发收集器
							- 采用**复制算法**
							- 除Serial收集器外，只有他能与CMS收集器配合使用
							- 使用场景：虚拟机运行在Server模式
						- Parallel Scavenge 收集器
						  collapsed:: true
							- 该收集器的目标是达到一个可控制的 ((6405ef3b-98b6-4356-bc2e-85a1a75e8dc0))
							- 使用场景：适合后台运算而不需要太多交互的任务
							- 采用**复制算法**
							- 无法与CMS收集器配合使用
							- 配置
							  collapsed:: true
								- 两个精准控制吞吐量的参数
									- -XX:MaxGCPauseMillis
										- 控制最大垃圾收集停顿时间，设置改值后虚拟机垃圾回收的停顿时间都会小于这个值。
										- 该值设置的越小，相应的GC的次数就会增多，吞吐量和新生代的空间就会变小。
									- -X:GCTimeRatio
										- 设置吞吐量的大小
								- -XX:+UseAdaptiveSizePolicy
									- 是一个开关参数
									- 该参数打开之后，就不需要设置新生代大小（-Xmn）、Eden和Survivor区的比例（-XX:SurvivorRatio）、晋升老年代对象大小（-XX:PertenureSizeThreshold）等细节参数
									- 这个参数用于 GC自适应的调节策略
					- 老年代收集器
					  collapsed:: true
						- Serial Old收集器
						  collapsed:: true
							- Serial收集器的老年代版本
							- 一个单线程收集器
							- 给Client模式下的虚拟机使用
							- 采用**标记-整理算法**
							- 两大用途
								- jdk1.5之前版本中与Parallel Scanvenge收集器搭配使用，这种组合无法充分的利用服务器多CPU的处理能力。
								- 作为CMS收集器的后备预案，在发生 Concurrent Mode Failure时使用。
						- Parallel Old收集器
						  collapsed:: true
							- 多线程收集器
							- 是Parallel Scanvenge收集器的老年代版本
							- 采用**标记-整理算法**
							- 在注重吞吐量和CPU资源紧张的场景，优先考虑使用Parallel Scavenge和Parallel Old收集器的组合
						- CMS收集器
							- 以获取最短回收停顿时间为目标的收集器
							- 采用**标记-清除算法**
							- 也称为 高并发，低停顿收集器
							- 运作过程分为4个步骤
								- 初始标记（CMS initial mark）
									- 会出现GC停顿
									- 标记GC Roots能直接关联到的对象
								- 并发标记（CMS concurrent mark）
									- 执行 ((64044e66-3742-4a9f-b08c-e25b45d4c214))的过程
									- 耗时较长
								- 重新标记（CMS remark）
									- 会出现GC停顿
									- 在并发标记期间，因为用户程序继续执行导致标记发生变动的那一部分对象，对他们的标记记录进行修正
								- 并发清除（CMS concurrent sweep）
									- 耗时较长
									- 清除之前标记的可回收对象
							- 缺点
								- **对CPU资源十分敏感**，在并发收集阶段不会导致用户线程停顿，但是会占用一部分CPU资源，导致应用程序变慢，总吞吐量下降。
								- **无法处理浮动垃圾**，在CMS并发清除阶段用户线程还在执行，会导致新的垃圾产生，这个些垃圾出现在标记过之后，CMS无法在当前收集中集中处理掉他们，只能放在下一次GC时再清理，这部分垃圾就称为浮动垃圾。
								- **会产生大量空间碎片**，因为使用的是标记-清除算法。
					- G1收集器
					  collapsed:: true
						- 特点
							- 并行与并发，以获取最短回收停顿时间为目标的收集器
							- 分代收集，分代收集的概念在G1收集器中仍然保留
							- 空间整合，整体上采用**标记-整理**算法，局部使用**复制**算法，意味着G1在运行期间不会产生内存空间碎片
							- 可预测的停顿，与CMS不同，G1收集器可以预测回收停顿的时间
						- Region的划分
							- G1将Java堆划分成了多个大小相等的独立区域Region
							- 会跟踪各个Region里面的垃圾堆积的**价值大小**（回收所获得的空间大小和回收所需时间的经验值），进而方便**优先回收**
						- G1在进行可达性分析的时候，如何避免全堆扫描
							- 使用Remembered Set来避免全堆扫描
							- 每个Region都有自己的Remembered Set，用来统计Reference引用对象与Region之间的关系
						- 运作过程
							- 初始标记
								- 标记GC Roots能直接关联到的对象
								- 会停顿线程，但耗时很短
							- 并发标记
								- 从GC Root开始对堆中的对象进行可达性分析
								- 与用户线程并发执行，耗时较长
							- 最终标记
								- 在并发标记期间，因为用户程序继续执行导致标记发生变动的那一部分对象，对他们的标记记录进行修正
								- 需要停顿线程，也可以并发执行
							- 筛选回收
								- 对各个Region的回收价值和成本进行排序，根据用户期望的停顿时间制定回收计划。
								- 需要停顿线程，也可以并发执行
					- GC日志
					  collapsed:: true
						- 主要内容
							- GC发生的时间
							- 垃圾收集的停顿类型
							- 垃圾收集的区域名称
							- GC前该内存区域已使用容量->GC后内存区域的使用容量（该内存区域总容量）
						- 参考文章
							- [深入理解G1的GC日志](https://juejin.cn/post/6844903893906751501)
					- 垃圾收集器的参数配置
				- 内存分配与回收策略
					- 普遍的内存分配规则
						- 对象优先分配到Eden区
							- 大多数情况下，对象在新生代Eden区中分配。当Eden区没有足够空间进行分配时，虚拟机将会发起一次Minor GC。
						- 大对象直接进入老年代
							-
			- 内存分配策略
				- 每一个栈帧的内存分配大小，基本上在类结构确定下来的时候就是已知的，大体上可以认为是编译期可知的。
			- 类文件结构
			- 虚拟机类的加载机制
				- 类加载的时机
					- 主动使用
						- 主动引用的时机
					- 被动使用
				- 类加载的过程
					- 加载
					- 连接
						- 验证
						- 准备
						- 解析
					- 初始化
				- 类加载器
					- 类和类加载器的关系
					- 自定义类加载器
					- 双亲委派模型
					- 破坏双亲委派模型
					  collapsed:: true
						- 第一次：Java1.2引入双亲委派模型，为兼容Java1.1就存在的ClassLoader抽象类和类加载器，在ClassLoader中新增了findClass()方法。
						- 第二次：因SPI机制，父的类加载器需要获取子的类加载器，去加载厂商实现的类，提出了线程上下文加载器。
						- 第三次：实现热部署，OSGi。
					- 类加载器的应用
						- 获取一个包下面所有的类
							- 具体实现：cn.bravedawn.jvm.classloader.ClassUtil
							- 参考文章：[Java获取指定package下所有类](https://blog.csdn.net/yuhentian/article/details/110007378)
			- 虚拟机字节码执行引擎
			  collapsed:: true
				- 栈帧
					- 定义
					- 作用
					- 结构
					  collapsed:: true
						- 局部变量表
							- 定义：一组变量值存储空间。
							- 作用：用于存放方法参数和方法内部定义的局部变量。
							- Slot
								- 每个Slot占用32位长度的内存空间。
								- Java中占用32位以内的数据类型有：boolean, byte, char, short, int, float, reference和returnAddress。
									- reference类型
									  id:: 64043de7-b2f9-4db7-b4f3-574c88698635
										- 定义：表示对一个对象实例的引用。
										- 虚拟机通过该引用要做到两点：
											- 一是从此引用中能够直接或间接地查找到对象在Java堆中数据存放的其实地址索引
											- 二是此引用中直接或间接地查找到对象所属数据类型在方法区中的存储的类型信息，否则无法实现Java语言规范中定义的语法约束。
								- 对long和double进行分割存储
								- 局部变量表中**slot**的位置分布
									- 静态方法
									- 实例方法
										- 索引为0的Slot默认是用来传递方法所属对象实例的引用，也就是`this`。
								- 对于一个存储64位数据类型的两个相邻Slot，不允许单独访问其中一个。
							- 特点
							  collapsed:: true
								- 局部变量表建立在线程的堆栈上，是线程私有的数据，故对Slot的对写并无原子性的要求，并不会引起数据安全问题。
						- 操作数栈
							- 定义：是一个先进后出的栈，栈的最大深度定义在Code属性的max_stacks数据项中。
							- 作用：用来存放方法运行期间各个指令操作的数据。
							- 特点
							  collapsed:: true
								- 操作数栈中元素的数据类型必须和字节码指令的顺序严格匹配。
								- 虚拟机在实现栈帧的时候可能会做一些优化，让两个栈帧出现部分重叠的区域，以存放公用数据。
						- 动态连接
							- 作用：每个栈帧持有一个指向运行时常量池中的该栈帧所属方法的引用，以支持方法调用过程的动态连接。
							- 内容
								- 静态解析：类加载的时候（连接的解析阶段），符号引用就转化为直接引用。
								- 动态连接：运行期间转换为直接引用。
						- 方法返回地址
							- 定义：方法执行后返回的地址，方法退出的过程实际上就是当前栈帧出栈。
							- 退出方式
								- 正常完成出口
								- 异常完成出口
				- 方法调用
					- 背景
					  collapsed:: true
						- Class文件的编译过程不包含传统编译过程中的连接步骤，一切方法调用在Class文件里面存储的都只是符号引用，而不是方法在实际运行时内存布局中的**入口地址**（相当于之前说的直接引用）。
					- 目的：确定被调用方法的版本（即调用那一个方法）。
					- 方法解析
					  collapsed:: true
						- 定义：方法在程序运行之前就有一个可确定的调用版本，方法的调用版本在运行期是不可改变的，我们称这类方法的调用过程为**解析**（Resolution），解析调用是一个静态的过程。
						- JVM提供的方法调用的字节码指令
							- invokestatic：调用静态方法
							- invokespecial：调用实例构造器<init>方法、私有方法、父类方法
							- invokevirtual
							- invokeinterface
							- invokedynamic
						- 非虚方法
							- 定义：在类加载的时候就会把符号引用解析为直接引用，这些方法称为非虚方法
							- 分类
								- 使用invokestatic调用的方法
								- 使用invokespecial调用的方法
								- 被final修饰的方法
						- 虚方法
					- 分派
					  collapsed:: true
						- 定义：方法的调用版本确认的过程，我们称之为分派。
						- 名称解释
							- 静态类型：在代码`Human man = new Man()`中，Human称为静态类型，即编译期就可以确认，不会被改变的类型。
							- 实际类型：在代码`Human man = new Man()`中，Man称为动态类型，即运行期才可以确认的类型。
							- 宗量：方法的接收者与方法的参数统称为方法的宗量。
						- 静态分派
							- 定义：所有依赖**静态类型**来定位方法执行版本的分派动作称为**静态分派**。
							- 静态分派发生在编译阶段。
							- 典型应用：重载
							- 重载方法匹配优先级（自动类型转换）
								- 在方法重载时，方法参数的类型会按照char->int->long->float->double->Character->....(相关类型实现的接口或父类)->Object->可变长参数，来进行静态分派。
								- 在单方法参数中成立的自动转型，在变长参数中是不成立的。
						- 动态分派
							- 定义：在运行期根据**实际类型**确定方法执行版本的分派过程称为**动态分派**。
							- 典型应用：重写
							- 根据分派基于多少种宗量，分为单分派和多分派
							- 单分派：根据一个宗量对目标方法进行选择
							- 多分派：根据多于一个宗量对目标方法进行选择
							- Java语言的静态分派属于**多分派类型**
								- 一是方法接受者
								- 二是方法参数
							- Java语言的动态分派属于**单分派类型**，只看方法的接受者。
						- 虚方法表
							- 背景：动态分派比较消耗性能，大部分的代码实现不会有很多的动态分派
							- 具体内容：使用虚方法表来代替元数据查找，提高性能
							- 特点
								- 某个方法如果在子类中没有被重写，方法的入口地址与父类方法的是一致的。
								- 若子类重写了父类方法，那么子类方法表中的地址会替换为子类实现版本的入口地址。
						- 动态类型语言支持
							- 背景
							  collapsed:: true
								- Java是在编译期就会做类型检查。
								- 在JDK7，Java为了实现”动态类型语言“而做的改进。
							- 定义：动态语言的关键特征是他的类型检查的主体过程是在运行期而不是编译期。
							- 动态类型语言
								- 变量无类型，变量值有类型
								- 开发效率高
								- 对开发人员更灵活
							- 静态类型语言
							  collapsed:: true
								- 与类型相关的问题在编译期就能及时发现，利于代码稳定性，进行大规模代码的开发
							- MethodHandle机制
								- 背景：Java没有办法单独的把一个函数作为参数进行传递。
								- 功能：类似于方法指针或者委托的方法别名，从而实现将一个函数作为参数进行传递。
								- 与Reflection的区别
									- 两者都是在模拟方法调用，Reflection是模拟Java代码层次的方法调用，而MethodHandle是模拟字节码层次的方法调用
									- Reflection是重量级的，包含了Java对象的全面映像，也就是说能够获取多全量的对象信息；而MethodHandle只包含执行该方法的相关信息
									- MethodHandle是针对字节码方法执行调用的模拟，可以利用虚拟机实现相关优化
									- Reflection是站在Java语言角度来看的，而MethodHandle是服务于所有运行在Java虚拟机之上的语言的
							- invokedynamic指令
								- 动态调用点：包含invokedynamic指令的位置
								- 功能：该指令的作用与MethodHandle的作用类似。为了解决如何将查找目标方法的决定权从虚拟机转嫁到具体的用户代码之中
								- invikedynamic与之前四种invoke*方法不同支出在于分派逻辑不是虚拟机决定，而是由程序员决定
								- INDY工具：将字节码转换为使用invokedynamic的简单工具
						- 基于栈的字节码解释执行引擎
							- 解释执行：通过解释器执行
							- 编译执行：通过即时编译器生成本地代码，然后执行
							- Java是一个半独立的编译器
								- Javac编译期完成了词法分析，语法分析到抽象语法树，接着遍历语法数生成字节码指令是在虚拟机之外进行的。
								- Java的解释器却在虚拟机内部。
							- 基于栈的指令集
								- 特点
									- 大部分指令是零地址指令
								- 优点
									- 可移植性强
									- 代码紧凑，编译器实现简单
								- 缺点
									- 运行较慢
									- 指令数量多于寄存器指令集
							- 基于寄存器的指令集
								- 缺点
									- 收到硬件的约束
								- 优点
									- 运行快
		- 三方类库
		  collapsed:: true
			- Guava
			- Apache Commons
			- Jackson JSON
			- reflectasm
				- 空笔记
	- 新特性
	  collapsed:: true
		- Java8
			- 我不会的函数
			  collapsed:: true
				- java.util.Map#compute
				- java.util.Map#merge
				- java.util.function.BiFunction
				- java.util.stream.Collectors#toMap()
				- Collectors.groupingBy()
				- Collectors.counting()
				- java.util.function.BiConsumer
				- 空笔记
			- stream操作
				- Stream生命周期
				  collapsed:: true
					- 流由三部分构成：数据源，一个或多个中间操作，一个或多个终止操作。
					- **数据源**：为流提供数据。
					- **中间操作**：依次获取数据并处理数据。所有的中间操作都是“懒操作”，也就是说在流开始工作之前，中间操作对流中的数据没有任何影响。
					- **终止操作**：流生命周期的结束，它可以触发流开始工作，中间操作也就会影响流中的数据。
				- peek操作
				  collapsed:: true
					- 使用场景
						- **peek()**方法存在的主要目的是用调试，通过**peek()**方法可以看到流中的数据经过每个处理点时的状态。
						- **peek()**在需要修改元素内部状态的场景也非常有用，比如我们想将所有**Person**的名字修改为大写，当然也可以使用**map()**和**flatMap**实现，但是相比来说**peek()**更加方便，因为我们并不想替代流中的数据，我们想保留原有的数据。
					- 特点
						- peek()是一个中间操作，不是终止操作。
					- 具体实践
						- JavaTrain：cn/bravedawn/java8/stream/peek
	- 命令行工具
		- java
			- `-cp`：`java -cp`和`-classpath`一样，是指定类运行所依赖其他类的路径，通常是类库，jar包之类。用于启动JVM时设置`classpath`。
		- javap
			- 介绍
				- javap是jdk自带的反解析工具。它的作用就是根据class字节码文件，反解析出当前类对应的code区（汇编指令）、本地变量表、异常表和代码行偏移量映射表、常量池等等信息。
			- 常用选项
				- `javap -v`：不仅会输出行号、本地变量表信息、反编译汇编代码，还会输出当前类用到的常量池等信息。
		- javac
			- `-source`：指定使用什么版本的JDK语法编译源代码
			- `-target`：指定生成特定于某个JDK版本的class文件
- 设计模式
  collapsed:: true
	- 装饰器模式
		- 使用场景：指能够在一个类的基础上增加一个装饰类（也可以叫包装类），并在装饰类中增加一些新的特性和功能。这样，通过对原有类的包装，就可以在不改变原有类的情况下为原有类增加更多的功能。
		- 类型：结构性
		- 实现接口
			- 接口+接口实现类+装饰器类
			- 抽象类+抽象类子类+装饰器类
	- 单例模式
	  collapsed:: true
		- 使用场景：想确保任何情况下都绝对只有一个实例。
		- 类型：创建型
	- 代理模式
	  collapsed:: true
		- 使用场景
		  collapsed:: true
			- 类似于中介，不会将被代理类直接暴露出来，可以通过代理类间接的使用被代理类的功能。
			- 通过代理类可以对被代理类的方法进行增强，比如统计方法调用耗时、方法调用前后添加日志等功能
		- 类型：结构型
		- 分类
		  collapsed:: true
			- 静态代理
			- 动态代理
			  collapsed:: true
				- 对于基于反射的动态代理而言，有一个必需的条件：被代理的对象必须有一个父接口。
	- 模板模式
	  collapsed:: true
		- 使用场景：通过抽象类定义方法调用的顺序和规则，具体的方法实现则交给子类去实现。
		- 类型：行为型
	- 适配器模式
	  collapsed:: true
		- 使用场景
			- 将多个类的不同功能的方法，整合到统一的方法中，能够使得原本不兼容的类可以一起工作。
			- 如果被适配的类可以修改，就直接修改被适配的类；如果不能修改，可以通过适配器模式进行适配。
		- 构成
		  collapsed:: true
			- 被适配的类
			- 适配器类，需要实现目标类的方法
			- 目标类（接口），规定了适配器类需要实现的方法
		- 分类
		  collapsed:: true
			- 类适配器模式
			  collapsed:: true
				- **适配器类**通过继承**被适配的类**并实现**目标类**，实现适配。
			- 对象适配器模式
			  collapsed:: true
				- **适配器类**实现了**目标类**，并实例化**被适配的类对象**，实现适配。
			- 方法适配器
			  collapsed:: true
				- 通常是指相同功能但由于输入参数的不同被划分为几个方法，其中有一个是核心方法，其余几个方法通过补全输入参数的做法调用核心方法。
				- 这种方式在框架代码中比较常见。
		- 类型：结构型
- Java EE
  collapsed:: true
	- Servlet
	  collapsed:: true
		- Java web application介绍
		  collapsed:: true
			- 静态和动态网站的区别
			  collapsed:: true
				- 图片
				- 静态网站
				  collapsed:: true
					- 每次加载页面时，预生成的内容都是相同的
					- 使用 HTML 代码来开发网站
					- 对每个请求发送完全相同的响应
					- 只有当有人发布和更新文件(将其发送到 Web 服务器)时，内容才会更改
					- 灵活性是静态网站的主要优势
				- 动态网站
				  collapsed:: true
					- 内容快速生成并定期更改
					- 使用 PHP、 SERVLET、 JSP 和 ASP.NET 等服务器端语言来开发网站
					- 可以为每个请求生成不同的 HTML
					- 页面包含“服务器端”代码，该代码允许服务器在加载页面时生成唯一的内容
					- 内容管理系统(CMS)是动态网站的主要优势
			- 服务器和客户端
			  collapsed:: true
				- 服务器：负责处理客户端请求，并返回响应
				- 客户端：与服务器沟通交互的软件
			- Html和Http
			  collapsed:: true
				- html：超文本标记语言，客户端和服务器之间通用的交互语言
				- http：http是客户端和服务器之间通用的通信协议，http运行在TCP/IP协议之上
				  collapsed:: true
					- 三个基本特性
					  collapsed:: true
						- HTTP与媒体无关：它指定只要服务器和客户端都能处理数据内容，任何类型的媒体内容都可以通过 HTTP 发送。
						- HTTP 是无连接的：它是一种无连接的方法，其中 HTTP 客户端，即浏览器发起 HTTP 请求，并在请求被发送后，客户端从服务器断开连接并等待响应。
						- HTTP 是无状态的：客户端和服务器只在当前请求期间知道彼此。后来，他们两个都忘记了对方。由于协议的无状态特性，无论是客户端还是服务器端都不能跨网页保留不同请求的信息。
					- http请求的重要部分
					  collapsed:: true
						- Http Method
						  collapsed:: true
							- GET：请求指定的资源。使用 GET 的请求应该只用于获取数据。
							- POST：发送数据给服务器。请求主体的类型由 Content-Type 首部指定
							- HEAD：请求资源的头部信息，并且这些头部与 HTTP GET 方法请求时返回的一致。该请求方法的一个使用场景是在下载一个大文件前先获取其大小再决定是否要下载，以此可以节约带宽资源。
							- TRACE：实现沿通向目标资源的路径的消息环回（loop-back）测试 ，提供了一种实用的 debug 机制。
							- PUT
							  collapsed:: true
								- 使用请求中的负载创建或者替换目标资源
								- PUT 与 POST 方法的区别在于，PUT 方法是幂等的：调用一次与连续调用多次是等价的（即没有副作用），而连续调用多次 POST 方法可能会有副作用，比如将一个订单重复提交多次。
							- DELETE：用于删除指定的资源
							- OPTIONS：用于获取目的资源所支持的通信选项。客户端可以对特定的 URL 使用 OPTIONS 方法，也可以对整站（通过将 URL 设置为“*”）使用该方法
						- URL(Uniform Resource Identifier)
						- Form Parameters
						- source IP address, proxy and port
						- destination IP address, protocol, port and host
						- Request method and Content
						- User-Agent header
						- Connection control header
						- Cache control header
					- http响应的重要部分
					  collapsed:: true
						- Status Code
						- Content Type（MIME type）：告诉客户端给用户呈现的数据类型
						- Content
					- GET vs. POST
					  collapsed:: true
						- GET
						  collapsed:: true
							- 只能发送有限数量的数据，因为数据是在URL中发送的，不同的浏览器和Web服务器限制了URL的长度
							- GET请求不安全，因为数据暴露在 URL 栏中
							- 获取请求可以加入书签
							- GET请求是等幂的。这意味着第二个请求将被忽略，直到第一个请求的响应被传递
							- GET请求比 Post 更高效，使用更多
						- POST
						  collapsed:: true
							- 由于数据是在主体中发送的，因此可以发送大量的数据
							- POST请求是安全的，因为数据没有暴露在 URL 栏中
							- 请求无法加入书签
							- POST请求的非幂等的
							- Post请求是低效率的，使用较少
			- URL
			  collapsed:: true
				- 定义：URL 是通用资源定位器的首字母缩写，用于定位服务器和资源。
				- https://localhost:8080/FirstServletProject/jsps/hello.jsp解析
				  collapsed:: true
					- https://：指定了客户端和服务器的通信协议
					- localhost：服务器主机名（ip）或是域名
					- 8080：服务器监听的端口
					- FirstServletProject/jsps/hello.jsp：请求服务器的资源，可能是静态网页，pdf
			- Servlet和JSP的用途
			  collapsed:: true
				- 提供对动态响应和数据持久性的支持来扩展web服务器的功能
			- Servlet容器
			  collapsed:: true
				- Servlet容器是web服务器的一部分
				- 作用：将客户端请求交给正确的资源（servlet和JSP）来处理，然后使用资源中的响应来生成Http响应并提供给web容器，web容器将响应发送给客户端
				- 原理：web容器接收到请求，对于Servlet来说会创建两个对象，分别是HttpServletRequest和HttpServletResponse。然后去找到正确的Servlet，接着为请求创建线程，接着会调用Servlet的service()方法，根据http请求方式调用doGet()或是doPost()方法，servlet会生产动态页面并写到响应中，一旦线程完成，web容器就会将响应转换为http响应返回给客户端
				- Servlet容器的状态
				  collapsed:: true
					- Standalone
					- In-process
					- Out-of-process
				- Servlet容器的重要工作
				  collapsed:: true
					- 通信的支持
					  collapsed:: true
						- 提供了web服务器与Servlet/JSP之间的通信支持
						- 不需要构建一个服务器套接字来监听来自 webserver 的任何请求，解析请求并生成响应
						- 只需关注自己的业务逻辑
					- 生命周期与资源管理
					  collapsed:: true
						- 负责管理Servlet的生命周期
						- 提供诸如 JNDI 之类的实用工具，用于资源池和管理
					- 多线程支持
					  collapsed:: true
						- 为每一个请求创建一个线程
						- 不会为每个请求初始化 servlet，从而节省时间和内存
					- JSP支持
					  collapsed:: true
						- 应用程序中的每个 JSP 都由容器编译并转换为 Servlet，然后容器像其他 Servlet 一样管理它们
					- 杂项
					  collapsed:: true
						- Web 容器管理资源池、进行内存优化、运行垃圾收集器、提供安全配置、对多个应用程序的支持、热部署以及其他一些幕后任务
			- Server：Web vs. Application
			  collapsed:: true
				- 定义
				  collapsed:: true
					- 服务器是接受并响应其他程序（称为客户端）发出的请求的设备或计算机程序。 它用于管理网络资源和运行提供服务的程序或软件。
				- 分类
				  collapsed:: true
					- Web Server
					  collapsed:: true
						- 图片
						- Web 服务器只包含 web 或 servlet 容器。 可用于servlet、jsp、struts、jsf等。不能用于EJB。
						- 它是一台可以存储网络内容的计算机。 一般来说，网络服务器可用于托管网站，但也使用其他一些网络服务器，如 FTP、电子邮件、存储、游戏等。
						- web server的例子
						  collapsed:: true
							- Apache Tomcat
							- Resin
						- 有两种方式为客户端提供响应
						  collapsed:: true
							- 通过脚本和数据库通信生成响应
							- 发送与url相关联的文件给客户端
						- Web Server与Application Server之间的区别
						  collapsed:: true
							- Application Server是Web Server的一部分
							- Web Server可以直接向客户端提供静态资源的响应
							- 除静态数据等资源外，Web Server可以通过与Application Server连接去处理相应的请求
					- Application Server
					  collapsed:: true
						- 图片
						- 定义
						  collapsed:: true
							- Application Server包括web和EJB容器，只要是使用Servlet、JSP、EJB、JSF等组件实现，它是一个基于组件的产品，位于以服务器为中心的体系结构的中间层。
							- 提供了会话状态维护、安全、数据访问和持久化等功能
						- Application Server的例子
						  collapsed:: true
							- JBoss: Open-source server from JBoss community.
							- Glassfish: Provided by Sun Microsystem. Now acquired by Oracle.
							- Weblogic: Provided by Oracle. It more secured.
							- Websphere: Provided by IBM.
			- Content Type
			  collapsed:: true
				- 定义
				  collapsed:: true
					- Content Type也被称为MIME(多用途互联网邮件扩展)类型。它是一个HTTP报头，提供关于您要向浏览器发送什么内容的描述。
					- MIME是一种互联网标准，用于通过允许在消息中插入声音、图像和文本来扩展电子邮件的有限功能。
				- Content Type的清单
				  collapsed:: true
					- text/html
					- text/plain
					- application/json
			- web应用程序文件结构
			  collapsed:: true
				- 目录结构这里可以参考：https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html
			- Deployment Descriptor
			  collapsed:: true
				- web.xml文件是 web 应用程序的部署描述符，包含 servlet (3.0之前)、欢迎页面、安全配置、会话超时设置等的映射。
		- Servlet简介
			- 开头
			  collapsed:: true
				- Servlet中的主要api是由javax.servlet-api提供的，主要的接口和类在javax.servlet和javax.servlet.http下面
				- Servlet接口定义了Servlet的生命周期
				- 我们通过实现GenericServlet和HttpServlet来定义我们自己的Servlet，因为我们通常使用http协议访问我们的服务，所以一般实现HttpServlet
			- Common Gateway Interface (CGI)
			  collapsed:: true
				- 使用CGI技术创建动态web应用程序。
				- CGI的缺点
				  collapsed:: true
					- 随着请求数量的增加，服务器响应需要更多的时间
					- 对于每一个请求，CGI都会启动一个进程，web服务器受限于启动进程
					- 使用的平台语言是C，C++，Perl
				- Servlet与CGI之间的比较
				  collapsed:: true
					- 在处理时间和内存利用率方面，servlet提供了比CGI更好的性能
					- Servlet与平台和系统无关，使用Servlet开发的web应用程序可以运行在任何标准的web容器上
					- servlet是健壮的，因为容器负责servlet的生命周期，我们不需要担心内存泄漏、安全性、垃圾收集等问题
					- servlet是可维护的，而且学习曲线很小，因为我们只需要注意应用程序的业务逻辑
			- Servlet API
			  collapsed:: true
				- Javax.Servlet.Servlet是Servlet API的基本接口
			- Servlet Interface
			  collapsed:: true
				- 方法
				  collapsed:: true
					- init(ServletConfig paramServletConfig)
					  collapsed:: true
						- Servlet生命周期方法
						- 用于初始化servlet和ServletConfig参数
						- init()方法执行完成，Servlet才能处理客户端请求
						- 在servlet生命周期中只被调用一次
						- 可以在servlet类中扩展这个方法来初始化资源，比如DB Connection、Socket Connection等
					- getServletConfig()
					  collapsed:: true
						- 返回一个Servlet配置对象，它包含了Servlet的初始化参数和启动配置
						- 返回的 ServletConfig 对象是传递给 init 方法的那个
					- service(ServletRequest req, ServletResponse res)
					  collapsed:: true
						- Servlet生命周期方法
						- 该方法负责处理客户端请求
						- 当Servlet容器收到任何请求时，它都会创建一个新线程并通过将请求和响应作为参数传递和响应来执行Service()方法
						- servlet通常在多线程环境中运行，因此开发人员有责任使用同步保持共享资源线程安全
					- getServletInfo()
					  collapsed:: true
						- 这个方法返回包含servlet信息的字符串，比如作者、版本和版权。
						- 返回的字符串应该是纯文本，不能有标记。
					- destroy()
					  collapsed:: true
						- Servlet生命周期方法
						- 该方法在servlet生命周期中只能调用一次，并用于关闭任何开放资源。这类似于java类的finalize方法。
			- ServletConfig Interface
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- 用于将配置信息传递给 Servlet
					- 每个 servlet 都有自己的 ServletConfig 对象，servlet 容器负责实例化该对象
					- 可以在 web.xml 文件中<context-name>、<param-name>、<param-value>或通过使用 @WebInitParam注释提供 servlet init 参数。
					- 我们可以使用getServletConfig ()方法来获取 servlet 的 ServletConfig 对象。
				- 方法
				  collapsed:: true
					- getServletContext()
					  collapsed:: true
						- 此方法返回 servlet 的 ServletContext 对象。
					- getInitParameterNames()
					  collapsed:: true
						- 这个方法返回为 servlet 定义的 init 参数的名称的枚举 < String > 。如果没有定义 init 参数，则此方法返回空枚举。
					- getInitParameter(String paramString)
					  collapsed:: true
						- 此方法可用于按名称获取特定的 init 参数值。如果名称中没有参数，则返回 null。
					- getServletName()
					  collapsed:: true
						- 返回这个servlet实例的名称
			- ServletContext interface
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- ServletContext接口提供了对 servlet 的 Web 应用程序变量的访问。
					- ServletContext是唯一的对象，Web应用程序中的所有Servlet都可用
					- 当我们希望某些初始化参数对web应用程序中的多个或所有servlet可用时，我们可以使用ServletContext对象，并使用<context-param>元素在web.xml中定义参数
					- 可以通过ServletConfig的getServletContext()方法获取ServletContext对象
					- Servlet引擎还可以提供上下文对象，这些对象对于一组Servlet是唯一的，并且与主机的URL路径名称空间的特定部分绑定在一起。
				- 方法
					- getContext(String uripath)
					  collapsed:: true
						- 该方法返回特定uri路径的ServletContext对象，如果对servlet不可用或不可见，则返回null。
					- getResource(String path)
					  collapsed:: true
						- 此方法返回URL对象，允许访问任何请求的内容资源。我们可以访问项目，无论它们是否驻留在本地文件系统，远程文件系统，数据库或远程网络站点上，而无需了解如何获得资源的具体详细信息。
					- getResourceAsStream(String path)
					  collapsed:: true
						- 此方法返回给定资源路径的输入流，如果没有找到，则返回null。
					- getRequestDispatcher(String urlpath)
					  collapsed:: true
						- 此方法主要用于获取对另一个servlet的引用。在获得RequestDispatcher之后，servlet程序员将请求转发给目标组件（forward方法）或包含来自该组件的内容（include方法）。
					- log(String msg)
					  collapsed:: true
						- 此方法用于将给定的消息字符串写入Servlet日志文件。
					- getAttribute(String name)
					  collapsed:: true
						- 返回给定名称的对象属性。我们可以使用公共抽象enumeration <String> getAttributeNames()方法获取所有属性的枚举。
					- setAttribute(String paramString, Object paramObject)
						- 此方法用于设置具有应用程序范围的属性。所有其他访问这个ServletContext的servlet都可以访问这个属性。我们可以使用公共抽象方法void removeAttribute(String paramString)删除属性
					- getInitParameter(String name)
					  collapsed:: true
						- 这个方法返回在web.xml中用name定义的init参数的String值，如果参数名不存在则返回null。我们可以使用Enumeration<String> getInitParameterNames()来获取所有init参数名的枚举。
					- setInitParameter(String paramString1, String paramString2)
					  collapsed:: true
						- 可以使用这个方法来设置应用程序的初始化参数。
				- 注意
				  collapsed:: true
					- 理想情况下，这个接口的名称应该是ApplicationContext，因为它用于应用程序，而不是特定于任何servlet。另外，不要将它与URL中传递的访问web应用程序的servlet上下文混淆。
			- ServletRequest interface
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- ServletRequest接口用于向servlet提供客户端请求信息。如内容类型、内容长度、参数名称和值、头信息、属性等。
					- Servlet容器根据客户端请求创建ServletRequest对象，并将其传递给Servlet service()方法进行处理。
					- ServletRequest的子接口是HttpServletRequest，它包含一些用于会话管理、cookie和请求授权的其他方法。
				- 方法
					- Object getAttribute(String name)
					  collapsed:: true
						- 此方法将指定属性的值返回为Object，如果不存在则返回null。
						- 我们可以使用getAttributeNames()方法来获取请求属性名称的枚举。此接口还提供设置和删除属性的方法
					- getServerName()
					  collapsed:: true
						- 返回服务器的主机名。
					- getServerPort()
					  collapsed:: true
						- 返回它正在监听的服务器的端口号。
					- getParameter(String name)
					  collapsed:: true
						- 这个方法以String的形式返回请求参数。
						- 我们可以使用getParameterNames()方法来获取请求参数名称的枚举。
						- 返回url中拼接参数的value值，若请求地址为http://www.abc.com/def?a=1&a=2&a=3，此时使用getPatameter("a")，返回的值是getParameterValues("a")的数组的第一个值。
					- getParameterValues(String name)
					  collapsed:: true
						- 若你的请求参数会有多个值时，调用这个方法会返回一个数组。
			- ServletResponse interface
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- servlet使用ServletResponse接口向客户端发送响应。
					- Servlet容器创建ServletResponse对象，并将其传递给Servlet service()方法，然后使用响应对象为客户机生成HTML响应。
					- ServletResponse的子接口是HttpServletResponse
				- 方法
				  collapsed:: true
					- addCookie(Cookie cookie)
					  collapsed:: true
						- 用于在响应中添加cookie。
					- addHeader(String name, String value)
					  collapsed:: true
						- 用于添加具有给定名称和值的响应头
					- encodeURL(String url)
					  collapsed:: true
						- 通过将会话ID包含在其中对指定的URL进行编码，或者，如果不需要编码，则不加更改地返回URL。
					- getHeader(String name)
					  collapsed:: true
						- 返回指定报头的值，如果没有设置此报头，则返回null。
					- sendRedirect(String location)
					  collapsed:: true
						- 用于使用指定的重定向位置URL向客户端发送临时重定向响应。
					- setStatus(int sc)
					  collapsed:: true
						- 用于设置响应的状态码。
			- RequestDispatcher interface
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- RequestDispatcher接口用于将请求转发到另一个资源，该资源可以是相同上下文中的HTML、JSP或其他servlet。
					- 我们还可以使用它将另一个资源的内容包含到响应中。
					- 此接口用于同一上下文中的servlet通信协作
					- 我们可以使用ServletContext.getRequestDisPatcher(String Path)方法在Servlet中获得RequestDisPatcher。该路径必须以一个/开头，并将其解释为相对于当前上下文的根。
				- 方法
				  collapsed:: true
					- forward(ServletRequest request, ServletResponse response)
					  collapsed:: true
						- 将请求从servlet转发到服务器上的另一个资源(servlet、JSP文件或HTML文件)
					- include(ServletRequest request, ServletResponse response)
					  collapsed:: true
						- 在响应中包含资源(servlet、JSP页面、HTML文件)的内容
			- HttpServletRequest interface
			  collapsed:: true
				- 关于httpServletRequest path API的讨论
				  collapsed:: true
					- 附一张图
					  ![httpservlethelper-768x391.png](../assets/httpservlethelper-768x391_1672322215374_0.png)
					- 参考文章：[HttpServletRequest Path Decoding](https://agiletribe.purplehillsbooks.com/2016/02/23/httpservletrequest-path-decoding/)
			- sendRediret
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- HttpServletResponse 接口的 sendRedirect() 方法可用于将响应重定向到另一个资源，它可以是 servlet、jsp 或 html 文件。
					- 它接受相对和绝对 URL。
					- 它在客户端工作，因为它使用浏览器的 url 栏发出另一个请求。 因此，它可以在服务器内部和外部工作，也就是说我们可以通过这个方法在服务器内部控制客户端的行为。
				- forward()和sendRedirect()的区别
				  collapsed:: true
					- 实验结论，可以参考mall/Servlet/forward-sendRedirect-example项目
					  collapsed:: true
						- forward()配置的转发不会进行页面的跳转（或者说浏览器地址栏的地址是不会改变的，因为request和response对象本身就没有变）
						- sendRedirect()配置的跳转会进行页面的跳转，会跳向一个新的地址，浏览器地址栏的地址会变，浏览器控制台http请求的状态码会变为302
					- 参考区别：
			- GenericServlet class
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- GenericServlet是一个抽象类，实现了Servlet，ServletConfig和Serializable接口。
					- GenericServlet提供了所有Servlet生命周期方法和ServletConfig方法的默认实现，使我们在扩展这个类时更加容易，我们只需要覆盖我们想要的方法，其余的方法我们可以使用默认实现。
					- 这个类中定义的大多数方法只是为了方便地访问Servlet和ServletConfig接口中定义的常用方法
					- GenericServlet类中一个重要的方法是无参数的init()方法，如果我们必须在处理servlet请求之前初始化一些资源，那么我们应该在servlet程序中重写这个方法。
				- 除了对Servlet和ServletConfig方法的实现外，单独提供的方法
				  collapsed:: true
					- init()
					  collapsed:: true
						- 一个方便的方法，可以被重写，这样就不需要调用super.init(config)。
						- 不用重写init(ServletConfig)，只需重写这个方法，它就会被GenericServlet的init (ServletConfig config)方法调用。ServletConfig对象仍然可以通过getServletConfig()获取。
					- log(String msg)
					  collapsed:: true
						- 将指定的消息写入servlet日志文件，并以servlet名称作为前缀。
					- log(String message, Throwable t)
					  collapsed:: true
						- 将给定Throwable异常的解释性消息和堆栈跟踪写入servlet日志文件，前面加上servlet名称。
			- HttpServlet class
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- HTTPServlet是一个抽象类，它扩展了GenericServlet，并为创建基于HTTP的web应用程序提供了基础。
					- 为不同的HTTP方法定义了一些可以被子类重写的方法。
				- 方法
				  collapsed:: true
					- service(ServletRequest req,ServletResponse res)
					  collapsed:: true
						- 通过将请求和响应对象转换为 http 类型，将请求分派到protected service()方法。
					- service(HttpServletRequest req, HttpServletResponse resp)
					  collapsed:: true
						- 从服务方法接收请求，并根据传入的 http 请求类型将请求分派到 doXXX ()方法。
					- doGet(HttpServletRequest req, HttpServletResponse resp), for HTTP GET requests
					- doPost(HttpServletRequest req, HttpServletResponse resp), for HTTP POST requests
					- doPut(HttpServletRequest req, HttpServletResponse resp), for HTTP PUT requests
					- doDelete(HttpServletRequest req, HttpServletResponse resp), for HTTP DELETE requests
					- doHead(HttpServletRequest req, HttpServletResponse resp), for HTTP HEAD requests
					- doOptions(HttpServletRequest req, HttpServletResponse resp), for HTTP OPTIONS requests
					- doTrace(HttpServletRequest req, HttpServletResponse resp), for HTTP TRACE requests
					- getLastModified(HttpServletRequest req)
					  collapsed:: true
						- 返回自1970GMT 1月1日午夜以来最后一次修改 HttpServletRequest 的时间
			- Servlet Attributes
			  collapsed:: true
				- 介绍
				  collapsed:: true
					- Servlet属性（Servlet Attributes）用于Servlet之间的通信，可以在web应用程序中设置、获取和删除属性。
					- servlet属性有三种作用域：请求作用域（request scope）、会话作用域（session scope）和应用程序作用域（application scope）。
					- ServletRequest，httpsession和ServletContext 接口提供分别从请求，会话和应用程序范围中获取/设置/删除属性的方法。
					- Servlet属性与ServletConfig或ServletContext的web.xml中定义的初始化参数是不同。
			- Annotations in Servlet 3
			  collapsed:: true
				- 背景
				  collapsed:: true
					- 在Servlet 3之前，所有的Servlet映射和它的init参数都是在web.xml中定义的，当应用程序中Servlet的数量很大时，这样做很不方便，而且更容易出错。
					- Servlet 3引入了Java Annotations来定义servlet，filter和listener和初始参数
				- 注解
				  collapsed:: true
					- @WebServlet
					  collapsed:: true
						- 我们可以在Servlet类中使用这个注解来定义init参数、loadOnStartup值、描述和url模式等。
						- 必须在该注解的value或urlPattern属性中声明至少一个URL模式，但不能同时声明两者。
						- 声明此注解的类必须扩展HttpServlet。
						- 值得注意的是value和urlPatterns必须以/开头
					- @WebInitParam
					  collapsed:: true
						- 该注解用于定义servlet或过滤器的初始化参数，它包含名称、值对，我们还可以提供描述。
						- 这个注解可以在@WebFilter或@WebServlet注解中使用
					- @WebFilter
					  collapsed:: true
						- 这个注解用于声明一个servlet过滤器。
						- 该注解在部署期间由容器处理，将根据配置创建它所在的Filter类，并应用于URL模式、servlet和DispatcherTypes。
						- 带注解的类必须实现javax.servlet.Filter接口。
					- @WebListener
					  collapsed:: true
						- 在给定的web应用程序上下文中，用于声明各种事件类型的监听器的注解
				- 空笔记
			- Servlet Life Cycle
			  collapsed:: true
				- web容器维护这Servlet实例的生命周期
				  collapsed:: true
					- 如下图所示，Servlet有三个状态：new，ready和end
					  ![cbc8abf3-7d2e-44db-b610-01166c10a0c8-4632647.jpg](../assets/cbc8abf3-7d2e-44db-b610-01166c10a0c8-4632647_1671973498704_0.jpg)
					- 当Servlet被创建，则Servle就处于new状态
					- 当web容器调用init()方法之后，Servlet进入ready状态，Servlet去执行它的所有任务
					- 当web容器调用destory()方法之后，Servlet进入end状态
				- 生命周期的五个阶段
					- Servlet class is loaded
					  collapsed:: true
						- 类加载器负责加载 servlet 类。当 Web 容器接收到对 servlet 的第一个请求时，将加载 servlet 类。
					- Servlet instance is created
					  collapsed:: true
						- Web 容器在加载 servlet 类之后创建 servlet 的实例。Servlet 实例在 servlet 生命周期中只创建一次。
					- init method is invoked
					  collapsed:: true
						- Web 容器在创建 servlet 实例之后只调用一次 init()方法。init()方法用于初始化 servlet。它是 javax.servlet.Servlet 接口的生命周期方法。init()方法的语法如下：public void init(ServletConfig config) throws ServletException
					- service method is invoked
					  collapsed:: true
						- 每次接收到对 servlet 的请求时，Web 容器都会调用service()方法。如果没有初始化 servlet，它将从头按照前三个步骤去执行，再去调用service()方法。如果初始化了 servlet，它将调用service()方法。请注意，servlet 只初始化一次。Servlet 接口的service()方法的语法如下：public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException
					- destroy method is invoked
					  collapsed:: true
						- Web 容器在从服务中删除 servlet 实例之前调用destory()方法。它让 servlet 有机会清理任何资源，例如内存、线程等。Servlet 接口的destory()方法的语法如下：public void destroy()
				- 生命周期的三个核心方法
					- init()
					  collapsed:: true
						- 这个方法有两个实现
						  collapsed:: true
							- init()
							- init(ServletConfig config)
						- 特点
						  collapsed:: true
							- 在web容器初始化的时候会调用这个方法
							- 这个方法在Servlet的生命周期中只会被调用一次
							- 实现了ServletConfig接口的对象，可以访问web.xml中定义的键值参数
					- service()
					  collapsed:: true
						- 根据请求类型将请求分发到合适的方法上去处理，开发者必须提供相应的实现方法
						- 该方法不需要复写
					- destory()
					  collapsed:: true
						- web容器调用该方法会使Servlet退出服务
						- 想在servlet超出范围之前关闭或销毁一些文件系统或网络资源，您应该调用这个方法
						- 这个方法在Servlet的生命周期中只会被调用一次
			- 创建一个Servlet程序
			  collapsed:: true
				- 实现一个Servlet的三个途径
				  collapsed:: true
					- 实现Servlet接口
					- 继承GenericServlet类
					- 继承HttpServelet类
				- 创建一个Servlet程序的六个步骤
				  collapsed:: true
					- 1.创建目录结构
					  collapsed:: true
						- 目录结构定义了不同类型文件的放置位置，以便 web 容器可以获取信息并响应客户端。这里你可能联想到了Maven的目录结构，如下图：
					- 2.创建一个Servlet
					  collapsed:: true
						- 实现Servlet接口
						- 继承GenericServlet类
						- 继承HttpServelet类
						  collapsed:: true
							- HttpServlet 类被广泛用于创建 servlet，因为它提供了处理 http 请求的方法，例如 doGet()、doPost、doHead() 等。
					- 3.编译Servlet
					  collapsed:: true
						- 为了编译Servlet需要引用服务器厂商提供的Servlet标准实现的jar包：
						- 加载jar文件的两种方式
						  collapsed:: true
							- 1.设置类路径
							- 2.将jar文件粘贴到JRE/lib/ext 文件下
						- 接着编译java文件后，将servlet的类文件粘贴到WEB-INF/classes目录下
					- 4.创建一个部署描述文件
					  collapsed:: true
						- 部署描述符是一个 xml 文件，Web 容器从中获取有关要调用的服务的信息。Web 容器使用解析器从 web.xml 文件中获取信息。 有许多 xml 解析器，例如 SAX、DOM 和 Pull。
					- 5.部署项目，启动服务
					  collapsed:: true
						- Tomcat的配置
						  collapsed:: true
							- 设置JAVAHOME或JREHOME在环境变量中
							- 在conf目录下修改server.xml文件，修改tomcat的默认端口号（默认是8080）
						- 部署servlet项目方法
						  collapsed:: true
							- 将war文件复制到Tomcat的webapps目录下
							- 使用命令创建war文件：jar cvf myproject.war *，在与WEB-INF同级的目录中
						- 运行bin目录下的startup.bat
					- 6.访问Servlet
			- Servlet是如何工作的
			  collapsed:: true
				- Servlet是如何工作的，详情参见下图：
				- web容器如何处理servlet请求
				  collapsed:: true
					- 1.将请求与 web.xml 文件中的 servlet 进行映射
					- 2.为此请求创建请求和响应对象
					- 3.调用线程上的service（javax.servlet.http.HttpServlet#service(javax.servlet.ServletRequest, javax.servlet.ServletResponse)）方法
					- 4.先调用public的service方法，后调用protected的service方法
					- 5.protected的service方法根据http请求方法调用doxxx()方法
					- 6.doxxx()方法生成响应并将响应传递给客户端
					- 7.发送响应之后，web容器会删除Request和Response对象
			- war文件
			  collapsed:: true
				- 定义：war(web archive)文件 包含一个web项目的文件。它可能有 servlet、xml、jsp、image、html、css、js 等文件。
				- 优势
					- 节省时间：war 文件将所有文件组合成一个单元。因此，将文件从客户端传输到服务器所需的时间更少。
				- 创建war文件
					- 进入项目目录（WEB-INF同级目录）执行命令：jar -cvf projectname.war *
					- 其中配置参数：-c 用于创建文件，-v 用于生成详细输出，-f 用于指定 archive 文件名，*（星号）符号表示该目录（包括子目录）的所有文件
				- 部署war文件的两种方式
					- 通过服务器的控制面板
					- 收单将war包放到Tomcat服务器的webapps目录，将war文件粘贴到这里
				- 提取war包中的文件
					- 使用命令：jar -xvf projectname.war
					- 其中配置参数：-x从档案中提取指定的 (或所有) 文件，-v 用于生成详细输出，-f 用于指定 archive 文件名
			- web.xml中的welcome-file-list标签
			  collapsed:: true
				- web-app 的welcome-file-list元素，用于定义欢迎文件列表。 它的子元素是welcome-file，用于定义欢迎文件。
				- 欢迎文件是服务器自动调用的文件，如果您未指定任何文件名。
				- 默认情况下，服务器按以下顺序查找欢迎文件（如果没有找到这些文件，服务器将呈现 404 错误）：
					- welcome-file-list in web.xml
					- index.html
					- index.htm
					- index.jsp
			- web.xml中的load-on-startup标签
			  collapsed:: true
				- 作用
					- 如果值为正，web-app 的 load-on-startup 元素会在部署或服务器启动时加载 servlet。也称为 servlet 的预初始化。
				- 优势
					- Servlet会在第一次请求时被加载，这意味着第一次请求会花费更多的时间
					- 如果在web.xml中指定load-on-startup，则Servlet将会在项目部署时或是服务器启动时加载。因此，第一个请求会花费更少的时间
				- 传递正值
					- 若传递正值，数字越小的Servlet会优先被加载
				- 传递负值
				  collapsed:: true
					- 若传递负值，Servlet将会在第一次请求时才会加载
			- Servlet组件注册的三种方式
			  collapsed:: true
				- 传统web.xml注册方式
				- 注解注册方式（Servlet 3.0+）
				- 编码注册方式（Servlet 3.0+）
				  collapsed:: true
					- 我们可以在ServletContentListener的初始化方法中，使用ServletContext.addServlet()方法去注册一个Servlet
		- Servlet中Session的管理
		  collapsed:: true
			- 会话的定义
			  collapsed:: true
				- 背景
				  collapsed:: true
					- HTTP协议和Web服务器是无状态的，这意味着对Web服务器来说，每个请求都是一个新的请求，他们不能识别它是否来自之前发送请求的客户端。
				- 定义
				  collapsed:: true
					- Session是web服务器和客户端之间的一种状态标识。由于HTTP和Web Server都是无状态的，所以维护Session的唯一方法是在每个请求和响应中在服务器和客户机之间传递一些关于会话的惟一信息(会话id)。
				- 有几种方法可以在请求和响应中提供唯一标识符
				  collapsed:: true
					- 1.用户认证
					  collapsed:: true
						- 用户可以从登录页面提供身份验证凭据，然后我们可以在服务器和客户机之间传递身份验证信息以维护会话。
						- 优点：实现简单
						- 缺点：如果同一用户使用不同的浏览器登录，此时系统内有两个相同的用户在操作，无法保证用户操作的唯一性
					- 2.HTML隐藏字段
					  collapsed:: true
						- 我们可以在HTML中创建一个唯一的隐藏字段，当用户开始导航时，我们可以设置它的值为用户唯一，并跟踪会话。
						- 优点：实现简单
						- 缺点
						  collapsed:: true
							- 这种办法不能用于链接，客户端每次发送带有隐藏字段的请求时，都需要提交表单
							- 不安全，黑客可以从HTML源中获取隐藏字段的值并使用它们攻击会话
					- 3.URL重写
					  collapsed:: true
						- 在每个请求和响应中附加一个会话标识符参数，以跟踪会话。这是非常麻烦的，因为我们需要在每个响应中跟踪此参数，并确保它与其他参数没有冲突。
					- 4.Cookie
					  collapsed:: true
						- cookie是由web服务器在响应头中发送的一小段信息，并存储在浏览器的cookie中。当客户端发出进一步的请求时，它将cookie添加到请求头，我们可以利用它来跟踪会话。我们可以用cookie维护一个会话，但如果客户端禁用cookie，那么它就无法工作。
					- 5.Session Management API
					  collapsed:: true
						- 是在以上方法的基础上构建的，用于会话跟踪。
						- 上面所有方法的主要缺点
						  collapsed:: true
							- 大多数时候，我们不希望只跟踪会话，我们必须将一些数据存储到会话中，以便在未来的请求中使用。如果我们试图实现这一点，这将需要大量的努力。
							- 上述所有方法本身都不完整，它们都不能在特定的场景中工作。因此，我们需要一种能够利用这些会话跟踪方法在所有情况下都能提供会话管理的解决方案。
						- J2EE Servlet技术附带了我们可以使用的Session Management API。
			- 方法一：Cookies
			  collapsed:: true
				- 这里可以参考mall项目下的子项目Servlet/servlet-demo
				  collapsed:: true
					- cn.bravedawn.servlet.session.cookies.LoginSessionServlet
					- cn.bravedawn.servlet.session.cookies.LogoutSessionServlet
			- 方法二：HttpSession
			  collapsed:: true
				- Servlet API通过HttpSession接口提供会话管理。我们可以使用以下方法从HttpServletRequest对象获取会话。HttpSession允许我们将对象设置为可以在未来请求中检索的属性。
				- 方法
				  collapsed:: true
					- HttpSession getSession()
					- HttpSession getSession(boolean flag)
					- String getId()
					- Object getAttribute(String name)
					- long getCreationTime()
					- setMaxInactiveInterval(int interval)，设置会话超时时间
					- ServletContext getServletContext()
					- boolean isNew()
					- void invalidate()
				- Understanding JSESSIONID Cookie
				  collapsed:: true
					- 什么是JSESSIONID
					  collapsed:: true
						- 当我们第一次访问服务器的时候，在请求的响应头中就会有Set-Cookie:JSESSIONID=382503A133C933FCA016B7DB84C7199F;Path=/;信息。
						- 浏览器会根据响应头的set-cookie信息设置浏览器的cookie并保存。注意此cookie由于没有设置cookie有效日期，所以在关闭浏览器（这里的关闭浏览器就是把浏览器窗口关闭，不是只关闭tab）的情况下会丢失掉这个cookie。
						- 当我们再次请求的时候，浏览器会在请求头中携带JSESSIONID发送给服务器（每次请求都是这样）。
						- JSESSIONID用于服务器处理客户端请求时识别Httpsession对象，换句话说服务器识别session的方法是通过jsessionid来告诉服务器该客户端的session在内存的什么地方。说白了HttpSession是通过JSESSIONID来实现的。
					- 当一个JSP页面被访问时，web容器会自动创建一个HttpSession，因此我们无法通过判断HttpSession是否为null来决定用户是否已经登录。所以我们需要使用HttpSession Attribute来判断用户是否已经登录。
				- HttpSession与Cookie的区别
				  collapsed:: true
					- 相同点
					  collapsed:: true
						- HttpSession是通过cookie实现的，需要将JSessionId的值存储在浏览器cookie中
						- 其目的都是为了实现客户端和服务器之间的会话保持
					- 不同点
					  collapsed:: true
						- HttpSession如果关闭浏览器就会丢弃会话信息，而cookie不会
						- HttpSession将数据存储在服务器上，cookie将数据存储的浏览器上
				- 这里可以参考mall项目下的子项目Servlet/servlet-demo
				  collapsed:: true
					- cn.bravedawn.servlet.session.httpsession.LoginHttpSessionServlet
					- cn.bravedawn.servlet.session.httpsession.LogoutHttpSessionServlet
			- 方法三：URL Rewriting
			  collapsed:: true
				- 背景：在禁用浏览器cookie的情况下，服务器端就无法从客户端获取JSESSIONID cookie。Servlet API提供了url复写的方法来解决这个问题，实现会话管理。
				- JSESSIONID
				  collapsed:: true
					- 定义：JSESSIONID是一个Cookie，Servlet容器（tomcat，jetty）用来记录用户会话信息。
					- 简单说明
					  collapsed:: true
						- 1.第一次访问服务器的时候，会在响应头里面看到Set-Cookie信息（只有在首次访问服务器的时候才会在响应头中出现该信息）。例如：
						- 2.当再次请求的时候（非首次请求），浏览器会在请求头里将cookie发送给服务器(每次请求都是这样)
						- 3.当每一个用户访问服务器的时候，服务器都会为用户开启一个session，生成一个JSESSIONID，JSESSIONID就是用来判断当前用户对应于那个session。换句话说服务器识别session时，就是通过JSESSIONID来判断用户的session保存在内存的什么地方
					- 生成时机
					  collapsed:: true
						- 1.创建会话时，即调用request.getSession()的时候
						- 2.当访问JSP资源时，容器会自动为请求创建会话
				- 定义：通过在URL后面加上;jsessionid=xxx来传递session id，这样即使Cookie不可用时，也可以保证session的可用性，但是session暴露在URL里，本身是不安全的
				- 优点
				  collapsed:: true
					- 编码简单
					- 是一种后备方法，只有在浏览器cookie被禁用时才会发挥作用
				- 实现
				  collapsed:: true
					- 通过HttpServletResponse的encodeURL()方法
					- 如果我们必须将请求重定向到另一个资源，并且要提供会话信息，则可以使用encodeRedirecturl()方法。
				- 这里可以参考mall项目下的子项目Servlet/servlet-demo
				  collapsed:: true
					- cn.bravedawn.servlet.session.urlrewriting.LoginServlet
					- cn.bravedawn.servlet.session.urlrewriting.LogoutServlet
		- Servlet中的过滤器
		  collapsed:: true
			- 背景
				- 在上一节中我们通过HttpSession实现会话管理时，我们通过判断session属性来判断用户是否登录（或者说会话是否有效），这个方式实现简单但是如果我们有大量的Servlet和jsp页面那该怎么办，如果在将来我们修改这个session属性，那我们的工作量就更大了。
			- Servelt常见的使用场景
				- 将请求参数记录到日志文件
				- 资源请求的认证和授权
				- 在将请求正文（body）或报头（header）发送到servlet之前进行格式化
				- 压缩发送给客户端的响应数据
				- 通过添加一些cookie，标题信息等来更改响应
				- 设置请求或响应的报文编码
			- 实现
				- 1.实现javax.servlet.Filter接口
				- 2.在web.xml中声明或是使用@WebFilter注解
			- Servlet Filter interface
				- init(FilterConfig filterConfig)，web应用程序启动时创建Filter对象实例并调用该方法，Filter对象只会创建一次，init方法只会执行一次。可通过FilterConfig对象获取配置信息
				- doFilter()，执行实际的拦截工作
				- destory()，Servlet容器在销毁过滤器实例前调用该方法，在该方法中释放Servlet过滤器占用的资源
			- 具体实现参考mall项目下的子项目Servlet/servlet-demo
			  collapsed:: true
				- cn.bravedawn.filter.AuthenticationFilter
				- cn.bravedawn.filter.RequestLoggingFilter
			- 过滤器的执行顺序：web.xml 中的filter-mapping 元素的顺序决定了 Web 容器应用过滤器到 Servlet 的顺序
			- web.xml配置节点说明
				- <dispatcher>子元素可以设置的值及其意义
					- REQUEST：当用户直接访问页面时，Web容器将会调用过滤器。如果目标资源是通过RequestDispatcher的include()或forward()方法访问时，那么该过滤器就不会被调用。
					- INCLUDE
					- FORWARD
					- ERROR
			- 参考教程
				- https://www.journaldev.com/1933/java-servlet-filter-example-tutorial
				- https://www.runoob.com/servlet/servlet-writing-filters.html
		- Servlet中的监听器
		  collapsed:: true
			- 背景
			  collapsed:: true
				- 如果我们想在用户登录入口为数据库连接设置一个属性，如果只有一个入口我们可以直接在Servlet中进行实现，若我们有多个登录入口，就会造成大量的冗余代码。这是一个登录的请求事件，类似的事件还有程序的初始化，客户端请求，程序的销毁，创建和销毁一个会话，会话属性的修改等事件。我们都可以通过监听器去实现。
			- Servlet提供的监听器和事件
			  collapsed:: true
				- 监听器和事件的关系：Servlet为不同的事件提供了不同的监听器，监听器的每一个方法都以事件作为入参，进而根据事件的状态去做不同的处理
				- Servlet中的事件
					- javax.servlet.AsyncEvent
					- javax.servlet.http.HttpSessionBindingEvent
					- javax.servlet.http.HttpSessionEvent
					- javax.servlet.ServletContextAttributeEvent
					- javax.servlet.ServletContextEvent
					- javax.servlet.ServletRequestEvent
					- javax.servlet.ServletRequestAttributeEvent
				- Servlet中的监听器
					- javax.servlet.AsyncListener：监听ServletRequest发起的异步操作
					- javax.servlet.ServletContextListener：接收关于ServletContext生命周期更改的通知事件
					- javax.servlet.ServletContextAttributeListener：接收ServletContext属性更改的通知事件
					- javax.servlet.ServletRequestListener：接收关于请求进入和离开web应用程序范围的通知事件
					- javax.servlet.ServletRequestAttributeListener：接收ServletRequest属性变更通知事件
					- javax.servlet.http.HttpSessionListener：接收关于HttpSession生命周期更改的通知事件
					- javax.servlet.http.HttpSessionBindingListener：在对象在与会话绑定或取消绑定时得到通知
					- javax.servlet.http.HttpSessionAttributeListener：接收关于HttpSession属性更改的通知事件
					- javax.servlet.http.HttpSessionActivationListener
			- Servlet监听器的配置
				- 注解@WebListener
				- 在web.xml中配置
			- Servlet 监听器Listener 的执行顺序
				- 在 `ServletContext` 创建之前，Listener监听器（包括其他类型监听器）会先按配置顺序初始化；
				- 然后 `ServletContext` 初始化完成后会按照监听器配置的顺序回调相应的方法，比如 `ServletContextListener` 的 `contextInitialized()` 方法。
			- 具体实现参考mall项目下的子项目Servlet/servlet-demo
				- 包：cn.bravedawn.listener
		- Servlet Cookies Example
		  collapsed:: true
			- Cookie的定义
			  collapsed:: true
				- cookie是服务器发送给客户端的文本数据，并保存在客户端本地机器上。当客户端向服务器发送请求时，它会在请求头中将cookie信息传递给服务器。
			- Cookie的附加信息
			  collapsed:: true
				- 名称，NAME
				- 值，value
				- 所在的域，Domain：在涉及到多个二级域名共享cookie的时候，就需要配置这个值。存取cookie的只能在本域名下或者子域名下才能生效
				- 请求路径，Path：根据当前客户端的访问路径，若访问路径包含cookie的请求路径，客户端请求就会将这些cookie发送到服务器上
				- 有效期（以秒为单位），Max-Age：默认值是-1，表示永久有效
				- 备注，Comment
				- 版本，version：默认值是0
			- API（javax.servlet.http.Cookie）
			  collapsed:: true
				- HttpServletRequest通过getCookies()获取请求中携带的cookie数组
				- HttpServletResponse 通过addCookie(Cookie c)添加cookie信息到响应头里
			- 具体实现参考mall项目下的子项目Servlet/servlet-demo
			  collapsed:: true
				- cn/bravedawn/servlet/cookie
			- 参考文章
			  collapsed:: true
				- 关于cookie的附加信息
				  collapsed:: true
					- https://www.cnblogs.com/xiangkejin/p/8952801.html
		- Servlet上传和下载文件（通过使用commons-fileupload实现）
		  collapsed:: true
			- 实现步骤
			  collapsed:: true
				- 引入依赖：commons-fileupload和commons-io
				- 1.编写上传文件的html
				- 2.在web.xml中上下文参数中配置上传文件的路径
				- 3.在上下文监听器中获取上下文参数，创建上传文件路径
				- 4.编写上传文件和下载文件的Servlet
			- 注意点
			  collapsed:: true
				- 上传文件
				  collapsed:: true
					- request.setCharacterEncoding("utf-8");
					  collapsed:: true
						- 设置客户端请求进行重新编码的编码
					- response.setContentType("text/html;charset=utf-8");
					  collapsed:: true
						- 设置响应文件的编码
				- 下载文件
				  collapsed:: true
					- response.setHeader("Content-Disposition", "attachment;filename*=utf-8''" + URLEncoder.encode(fileName, "utf-8"));
					  collapsed:: true
						- 保证下载文件的编码正确
				- 下面这两句代码一定要在进入doxxx方法的第一句代码上写
				  collapsed:: true
					- request.setCharacterEncoding("utf-8");
					- response.setCharacterEncoding("utf-8");
			- 具体实现参考mall项目下的子项目Servlet/servlet-demo
			  collapsed:: true
				- cn.bravedawn.servlet.uploadfile.UploadDownloadFileServlet
		- Servlet异常处理
		  collapsed:: true
			- 异常处理关键点
			  collapsed:: true
				- servlet容器在调用servlet去处理异常之前，会将异常信息放到request和response中
			- 部署描述文件
			  collapsed:: true
				- 捕获
				  collapsed:: true
					- 配置http错误码
					- 配置异常
				- 处理
				  collapsed:: true
					- 跳转至jsp
					- 跳转至Servlet
		- Servlet、JDBC和Log4j整合
		  collapsed:: true
			- 设计要点
			  collapsed:: true
				- 1.通过上下文监听器初始化数据库连接和Log4j配置
				- 2.全局异常处理器，这里可以参考上面的Servlet异常处理
				- 3.用户认证的过滤器
				- 4.注册，登录，登出接口
			- 实现参考：mall\Servlet\ServletDBLog4jExample项目
		- Servlet3 文件上传
		  collapsed:: true
			- 注解@MultipartConfig，有三个参数
			  collapsed:: true
				- fileSizeThreshold：这是临时保存上传文件时的大小阈值。如果上传的文件大小超过该阈值，将被保存到磁盘上。否则，文件存储在内存中(大小以字节为单位)
				- maxFileSize：这是上传文件的最大大小(大小以字节为单位)
				- maxRequestSize：这是请求的最大大小，包括上传的文件和其他表单数据(大小以字节为单位)
				- location：上传文件的存储目录
			- 参考实现：mall\Servlet\servlet-demo项目的cn.bravedawn.servlet.uploadfile.FileUploadServlet
			- 参考文章：
			  collapsed:: true
				- A Guide to Java EE Web-Related Annotations
				- Uploading Files with Servlets and JSP
				- Servlet 3 File Upload – @MultipartConfig, Part
		- Tomcat Datasource JNDI
		  collapsed:: true
			- App范围，直接在MATE-INF文件下的context.xml文件中配置
				- 优点
					- 实现简单
				- 缺点
					- 由于context与 WAR 文件绑定在一起，因此我们需要为每个小的配置更改构建和部署新的 WAR。
					- 数据源是由容器创建的，只用于应用程序，因此不能在全局范围内使用。我们不能跨多个应用程序共享数据源。
					- 如果有一个定义为相同名称的全局数据源(Tomcat中的server.xml) ，则忽略应用程序数据源。
				- 参考实现
					- 参考mall项目/Servlet/ServletJNDI
			- Server范围，通过配置Server的context.xml文件，实现多个应用程序共享一个数据源
				- 实现
					- 编辑tamcat/conf/context.xml文件。添加如下代码
					  ![941d956d-5aac-4d5f-b6f5-2b97a6971812-4632647.jpg](../assets/941d956d-5aac-4d5f-b6f5-2b97a6971812-4632647_1671973348990_0.jpg)
					- 在项目的web.xml文件中定义
					  ![4ec6e670-597a-408b-9001-cff77c584a8d-4632647.jpg](../assets/4ec6e670-597a-408b-9001-cff77c584a8d-4632647_1671973363350_0.jpg)
				- 优点
					- 可以让多个应用程序共享一个数据源
				- 缺点
					- 导致数据库资源耗尽。如果您定义了100个连接的DataSource连接池，并且有20个应用程序，则将为每个应用程序创建数据源。这将导致2000年连接，显然会消耗所有数据库服务器资源并损害应用程序性能。
				- 参考实现
					- 参考mall项目/Servlet/ServletJNDIByServerContext
			- Server范围，通过配置Server的server.xml，在Server或是应用程序配置context.xml文件，是实现多个应用程序共享一个数据源的首要选择
				- 实现
				- 优点
			- 参考资料
				- https://tomcat.apache.org/tomcat-8.0-doc/config/context.html#Resource_Definitions
				- https://blog.csdn.net/wn084/article/details/80736253
			- 注意
				- 关于</welcome-file>不能指定Servlet的解决办法：https://www.cnblogs.com/taoweiji/p/3248847.html，我这里采用的是<meta http-equiv="refresh" content="0;URL=/ServletJNDIByServer">
	- JDBC
	  collapsed:: true
		- JDBC核心API
		  collapsed:: true
			- 驱动管理器接口：java.sql.DriverManager
			  collapsed:: true
				- 获取Driver的实现
				  collapsed:: true
					- collapsed:: true
					  1. 通过Class.forName("com.mysql.jdbc.Driver")，这种方式需要我们显示的在代码中体现
						- 类加载过程会触发一个静态初始化逻辑，实例化com.mysql.jdbc.Driver类，数据库驱动就会调用java.sql.DriverManager#registerDriver(java.sql.Driver)方法进行驱动注册。
						- 显示调用Class.forName()方法的背景：在 JDBC 版本 4 和 Java SE 1.6 之前，JVM 中没有可以自动发现和注册服务的通用机制。 因此，需要一个手动步骤来按名称加载 JDBC 驱动程序类。
					- 2. 通过 “jdbc.drivers” 系统属性，DriverManager会帮我们处理
						- 使用命令：`java -Djdbc.drivers=oracle.jdbc.driver.OracleDriver`，设置系统属性。在java.sql.DriverManager了的静态代码块中会调用loadInitialDrivers()方法将系统属性中携带的驱动程序参数进行驱动注册。
						- 或者在代码中设置系统属性：
						- ```java
						  System.setProperty("jdbc.drivers", "oracle.jdbc.driver.OracleDriver")
						  ```
					- 3. 通过 Java SPI ServiceLoader 获取 Driver实现，DriverManager会帮我们处理
					- 上面的这三种方法其实都在DriverManager的加载逻辑中覆盖了。
				- 问题：java.sql.DriverManager#loadInitialDrivers 方法中 JavaSPI 迭代器的空遍历的意义（Java8的逻辑）
				  collapsed:: true
					- driversIterator.next()方法会执行ServiceLoader#next()方法，这个方法会主动触发 ClassLoader 加载，将SPI获取的驱动类进行实例化，将驱动注册到JDBC。
					- 看这个方法：java.util.ServiceLoader.LazyIterator#nextService。
			- 建立连接 - java.sql.Connection
				- 建立连接的方式
					- `Connection DriverManager.getContection(String url, String user, String password);`：建立一个数据库连接，返回一个Connection对象
					- **推荐**：使用DataSource对象获取数据源
			- SQL 命令接口 - java.sql.Statement
				- 普通 SQL 命令 - java.sql.Statement
					- 功能：用于实现简单的没有参数的SQL语句
					- DDL语句和DML语句
						- DML 语句 ：CRUD
							- R（读操作）：ResultSet java.sql.Statement#executeQuery
							- CUD（增删改）：int java.sql.Statement#executeUpdate(java.lang.String)
						- DDL 语句
							- 使用boolean java.sql.Statement#execute(java.lang.String)
								- 成功的话：不需要返回值（返回值 false）
								- 失败的话：SQLException
					- 关闭操作
					  collapsed:: true
						- 使用statement.close()去关闭
						- 或者使用Try With Resources进行关闭
				- 预编译 SQL 命令 - java.sql.PreparedStatement
					- 功能：用于预编译可能包含输入参数的SQL语句。
					- 继承了`java.sql.Statement`
					- PreparedStatement 可以将参数插入到 SQL 语句中，因此 PreparedStatement 可以通过不同的参数值一次又一次地重复使用。
				- 存储过程 SQL 命令 - java.sql.CallableStatement
					- 功能：用于执行可能包含输入和输出参数的存储过程。
					- 继承了` java.sql.PreparedStatement`
				-
			- 执行SQL
			  collapsed:: true
				- 核心方法
					- **execute**：如果查询返回的第一个对象是 ResultSet 对象，则返回 true。 如果查询可以返回一个或多个 ResultSet 对象，请使用此方法。 通过重复调用Statement.getResultSet 来检索从查询返回的 ResultSet 对象。
					- **executeQuery**：返回一个ResultSet对象。
					- **executeUpdate**：返回一个整数，表示受 SQL 语句影响的行数。 如果您正在使用 INSERT、DELETE 或 UPDATE SQL 语句，请使用此方法
			- 处理结果，结果集接口 - java.sql.ResultSet
			  collapsed:: true
				- 可以通过游标访问 ResultSet 对象中的数据。
				- 调用 ResultSet 对象中定义的各种方法来移动光标。
			- 关闭连接
			  collapsed:: true
				- 在使用完一个`Connection`，`Statement`，或者`ResultSet`对象之后，应该使用他们的close方法释放资源。
				- 或者，使用 **try-with-resources** 语句自动关闭 Connection、Statement 和 ResultSet 对象，无论是否抛出 SQLException。
		- 使用DataSource对象获取数据源
		  collapsed:: true
			- 特点
				- DataSource接口是由驱动程序供应商实现的。
			- 优点
				- 可维护性：如果有DataSource的属性需要更改，系统管理员可以更新数据源属性，而不必担心更改每个与数据源建立连接的应用程序。
				- 可移植性：如果数据源被移动到不同的服务器，那么系统管理员只需将serverName属性设置为新的服务器名。
				- 当DataSource接口被实现为与ConnectionPoolDataSource实现一起工作时，该DataSource类的实例产生的所有连接将自动成为池连接。类似地，当DataSource实现被实现为与XADataSource类一起工作时，它产生的所有连接都将自动成为可以在分布式事务中使用的连接。
			- 使用DataSource接口的基本实现
				- 部署一个Datasource对象的步骤
					- 创建一个DataSource实例
					- 为DataSource实例设置属性
					- 注册该实例到JNDI命名服务，并使用它
			- 连接池
				- 背景
					- 打开和关闭连接涉及大量开销，使用连接池，可以反复使用连接，从而避免了为每次数据库访问创建新连接的开销。
				- 部署和使用连接池
					- 实例化一个ConnectionPoolDataSource的类的实例，并注册到JNDI命名服务
					- 实例化一个DataSource的类的实例，其其dataSourceName属性的值是绑定到先前部署的ConnectionPoolDataSource对象的逻辑名。
					- 使用DataSource对象来获取数据库连接。
					- 使用finally块来确保连接是关闭的
			- 分布式事务
			- 参考文章：[Connecting with DataSource Objects](https://docs.oracle.com/javase/tutorial/jdbc/basics/sqldatasources.html)
		- 参考教程
			- [JDBC Database Access](https://docs.oracle.com/javase/tutorial/jdbc/index.html)
	- JSP
	  collapsed:: true
		- 参考文章
			- [JSP tutorial](https://www.javatpoint.com/jsp-tutorial)
	- JPA
	  collapsed:: true
		-
	- 规范
	  collapsed:: true
		- JAX-RS(Java API for RESTful Web Services)
			- JAX-RS提供了一些注解将一个资源类，一个POJO Java类，封装为Web资源。
- 开发工具
  collapsed:: true
	- vmware
	  collapsed:: true
		- 许可证：NH001-8HJ06-18LJ3-0L926-98RP4
	- IDEA
	  collapsed:: true
		- 快捷键
			- MAC
				- 全局查找：`command`+`shift`+`F`
				- 删除整行：`command`+`delete`
				- 字母大小写转换：`command+shift+U`
				- 文件结构：`fn` + `command` + `F12`
				- 去除无效import：`control` + `option` + `o`
				- 跳转到指定行数：`command` + `L`
				- 返回到上一处代码：`command` + `[`
				- 前进到下一处代码：`command` + `]`
				- 显示隐藏文件：`Shift`+`Command`+`.`
				- 复制一行：`command` + `D`
	- VS Code
- 构建工具
  collapsed:: true
	- Maven
	  collapsed:: true
		- 基础知识
			- DependencyManagement标签的使用
			  collapsed:: true
				- 作用
					- 使用`DependencyManagement`可以统一管理项目的版本号，确保应用的各个项目的依赖和版本一致，不用每个模块项目都弄一个版本号，不利于管理，当需要变更版本号的时候只需要在父类容器里更新，不需要任何一个子项目的修改；
					- 如果某个子项目需要另外一个特殊的版本号时，只需要在自己的模块`Dependencies`中声明一个版本号即可。子类就会使用子类声明的版本号，不继承于父类版本号。
				- 与Dependencies的区别
					- `Dependencies`相对于`DependencyManagement`，所有生命在`Dependencies`里的依赖都会自动引入，并默认被所有的子项目继承。
					- `DependencyManagement`里只是声明依赖，并不自动实现引入，因此子项目需要显式的声明需要用的依赖。如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中写了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且`version`和`scope`都读取自父pom；另外如果子项目中指定了版本号，那么会使用子项目中指定的jar版本。
			- scope的值为`import`
			  collapsed:: true
				- `<scope>import</scope>` 只能用在 `DependencyManagement` 块中
				- ```
				  <dependencyManagement>
				  	<dependencies>
				  		<dependency>
				  			<!-- Import dependency management from Spring Boot -->
				  			<groupId>org.springframework.boot</groupId>
				  			<artifactId>spring-boot-dependencies</artifactId>
				  			<version>2.1.12.RELEASE</version>
				  			<type>pom</type>
				  			<scope>import</scope>
				  		</dependency>
				  	</dependencies>
				  </dependencyManagement>
				  ```
				- 以上面这段配置来做说明，它将 `spring-boot-dependencies`  中 `DependencyManagement` 下的 `Dependencies` 插入到当前工程的 `DependencyManagement` 中，所以不存在依赖传递。
				- 当没有 `<scope>import</scope>` 时，意思是将 `spring-boot-dependencies`  的 `Dependencies` 全部插入到当前工程的 `Dependencies` 中，并且会依赖传递。
			- 指定jdk编译版本号
				- 参见如下代码
				  ```xml
				  <build>
				    <plugins>
				      <plugin>
				        <groupId>org.apache.maven.plugins</groupId>
				        <artifactId>maven-compiler-plugin</artifactId>
				        <version>3.10.1</version>
				        <configuration>
				          <source>11</source>
				          <target>11</target>
				        </configuration>
				      </plugin>
				    </plugins>
				  </build>
				  ```
		- 插件
		  collapsed:: true
			- spring-boot-maven-plugin
				- 作用
					- maven项目的pom.xml中，添加了*org.springframework.boot:spring-boot-maven-plugin*插件，当运行`mvn package`进行打包时，会打包成一个可以直接运行的 JAR 文件，使用“Java -jar”命令就可以直接运行。
					- spring-boot-maven-plugin插件，在很大程度上简化了应用的部署，只需要安装了 JRE 就可以运行。
				- 参考文章
					- [spring-boot-maven-plugin插件的作用](https://www.cnblogs.com/acm-bingzi/p/mavenspringbootplugin.html)
			- maven-compiler-plugin
			  collapsed:: true
				- 背景
				  collapsed:: true
					- `maven`是个项目管理工具，如果我们不告诉它我们的代码要使用什么样的`jdk`版本编译的话，它就会用`maven-compiler-plugin`默认的`jdk`版本来进行处理，这样就容易出现版本不匹配，以至于可能导致编译不通过的问题。
				- 作用
				  collapsed:: true
					- 使用`maven-compiler-plugin`插件可以指定项目源码的`jdk`版本，编译后的`jdk`版本，以及`编码`。
			- flatten-maven-plugin
			  collapsed:: true
				- 使用场景：适合父子项目时使用
				- 配置
				  collapsed:: true
					- **FlattenMode=resolveCiFriendliesOnly**，设置该属性表示flatten只`${revision}`, `${sha1}` and/or `${changelist}`这个几个占位符。
					- **updatePomFile=true**，插件默认只会处理`packaging`属性为非`pom`的，如果要处理`packaging`为`pom`的，可将本属性值设置为`true`。
				- 使用
				  collapsed:: true
					- [单一项目](https://www.mojohaus.org/flatten-maven-plugin/examples/example-simple-project.html)
					  collapsed:: true
						- 使用场景：单一项目（不建议使用该插件）
						- 在pom文件的properties属性中声明依赖项的版本值，然后执行install或是deploy进行打包。然后项目中会生成.flattened-pom.xml文件，在这个文件中可以看到，flatten将properties属性值替换到原本版本依赖项版本的属性占位符。
					- [中心项目](https://www.mojohaus.org/flatten-maven-plugin/examples/example-central-version.html)
					  collapsed:: true
						- 使用场景：子父级项目，子项目会使用其他子项目作为依赖性
						- 在父级项目的properties属性中声明依赖版本值
						- 在子项目中可以使用父级项目properties属性声明的版本值去替换自己pom文件中依赖项版本的属性占位符。
					- [多个项目](https://www.mojohaus.org/flatten-maven-plugin/examples/example-multiple-versions.html)
					  collapsed:: true
						- 使用场景：子父级项目，子项目会使用其他子项目作为依赖项
						- 在父级项目的父级项目中声明依赖版本的属性值，然后在dependencyManagement中声明依赖项，并在依赖项的version中使用属性值的占位符进行声明。
						- 在子项目中，子项目可以直接使用其他子项目作为依赖项且不需要声明依赖版本。
					- 针对浦惠到家这种项目
					  collapsed:: true
						- esm-parent，设置一个版本号revision，打包的时候他的子module也设置这个占位符进行版本控制
						- 像支付服务这种
				- 官网： [flatten-maven-plugin](https://www.mojohaus.org/flatten-maven-plugin)
				- 参考文章
				  collapsed:: true
					- https://zhuanlan.zhihu.com/p/270574226
					- https://www.cnblogs.com/jonath/p/7729903.html
- ORM框架
  collapsed:: true
	- Mybatis
	  collapsed:: true
		- tinyint类型
		  collapsed:: true
			- 在mybatis generator项目中，tinyint类型字段的实体映射逻辑：
				- 若数据库定义字段为`tinyint(1)` ，映射之后的Java类型为`Boolean`
				- 若数据库定义字段为`tinyint(2)`，映射之后的Java类型为`Byte`
				- 若数据库定义字段为`tinyint(4)`，映射之后的Java类型也为`Byte`
		- sum()函数
		  collapsed:: true
			- `sum()`函数可能会返回null值，故在MyBatis查询中应该设置resultType为integer类型，不能是int。查询完成之后，还需要判断该值是否为null，从而避免代码出现空指针。
- 消息队列
  collapsed:: true
	- Pulsar
	  collapsed:: true
		- 官网
		- 架构介绍
		  collapsed:: true
			- [Apache Pulsar简介](https://www.cnblogs.com/hzmark/p/pulsar.html)
			- [Apache源码分析](http://aloyszhang.cn/tags?tag=pulsar)
			- [Pulsar 入门及介绍](https://crossoverjie.top/2021/04/18/pulsar/pulsar-start/)
			- [Pulsar VS. Kafka（1）: 统一的消息消费模型（Queue + Stream）](https://juejin.cn/post/7032939738814562334)
		- 教程
		  collapsed:: true
			- 单机安装
				- [Linux MacBook单机部署Pulsar并开启认证功能](https://blog.51cto.com/u_15454062/4924217)
			- [Apahe Pulsar 从入门到精通](https://blog.51cto.com/u_15278282/2933568)
		- 问题
		  collapsed:: true
			- 为什么要在@PulsarConsumer中写subscriptionName？
				- pulsar支持同一个topic可以有多个不同订阅模式的订阅，每个订阅下面可以有多个消费者。这里的订阅类似于Kafka中消费者组的概念。
- 日志框架
	- Java.util.logging
	- Log4j2
		- 参考文章
			- [Java Logging Tutorials](https://www.javacodegeeks.com/java-logging-tutorials)
			- [How Log4J2 Works: 10 Ways to Get the Most Out Of It](https://stackify.com/log4j2-java/)
			- [Apache Log4j 2 Tutorials](https://mkyong.com/logging/apache-log4j-2-tutorials/)
			- [Log4j2实现不同线程不同级别日志输出到不同的文件中](http://codepub.cn/2016/12/18/Log4j2-to-achieve-different-levels-of-different-threads-log-output-to-a-different-file/)
		- 主要的三个组件
			- Logger：用于记录消息。
			- Appender：用于将日志信息发布到目标，如文件、数据库、控制台等。
			- Layout：用于以不同的风格格式化日志信息。
		- Log4j2的最佳实践
		  collapsed:: true
			- 为LogManager对象使用静态修饰符：当开发人员在代码中声明任何变量时，都会带来开销。开发人员可以通过如下所示声明静态Logger引用来克服这种开销。
			  ```java
			  private static final Logger log = Logger.getLogger(YourClassName.class);
			  ```
			- 使用`isDebugEnabled()`将调试日志放在Java中，因为它将节省大量的字符串连接活动。下面是Java中调试模式的示例。在Java8中我们可以不用做日志登记的判断，具体可以参考 [Java8不需要校验日志等级](https://logging.apache.org/log4j/2.0/manual/api.html#Java_8_lambda_support_for_lazy_logging) 
			  ```java
			  if(logger.isDebugEnabled()) { 
			       logger.debug("java logging level is DEBUG Enabled"); 
			  }
			  ```
			- 通过使用log4j2.xml，开发人员可以为不同的Java类提供不同的Logger配置。开发人员可以让一些类处于INFO模式，一些类处于WARN模式或ERROR模式。
			- 制作定制的Log4j2 Appenders。如果开发人员想做一些标准Appenders不支持的事情，他们可以在线搜索或编写自己的定制Appenders。例如，开发人员可以通过扩展`AppenderSkeleton`类来制作他们自己的自定义Log4j2 Appender。
			- 如果给定的记录器没有分配级别，那么它将从最接近的祖先继承一个级别。这就是为什么开发人员总是将日志级别分配给配置文件中的根日志记录器，即log4j2.rootLogger=DEBUG。
			- 参考文章： [Log4j 2 Best Practices Example](https://examples.javacodegeeks.com/java-development/enterprise-java/log4j/log4j-2-best-practices-example/)
		- 简单自定义Log4j2的配置
		  collapsed:: true
			- 简单配置
			  ```xml
			  <?xml version="1.0" encoding="UTF-8"?>
			  <Configuration status="WARN">
			      <Appenders>
			          <Console name="Console" target="SYSTEM_OUT">
			              <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
			          </Console>
			      </Appenders>
			      <Loggers>
			          <Root level="INFO">
			              <AppenderRef ref="Console"/>
			          </Root>
			      </Loggers>
			  </Configuration>
			  ```
			- Configuration
			  collapsed:: true
				- Log4j2配置文件的根元素; **status** 属性表示应该记录内部 log4j 事件的级别。
			- Appdenders
				- 这个元素包含一个追加器列表; 在上面的示例中，定义了一个对应于系统控制台的追加器。
			- Loggers
			  collapsed:: true
				- 这个元素包含一个 Logger 实例列表。 **Root** 元素是一个输出所有消息的标准日志记录器。
			- **注意**：如果您没有提供一个，那么默认情况下将自动配置一个 Console appender 和 ERROR 日志级别。
		- Log4j2 Appenders
		  collapsed:: true
			- ConsoleAppender
			  collapsed:: true
				- 功能：将日志输出到系统控制台。
			- FileAppender
			  collapsed:: true
				- 功能：将日志写入文件。
			- RollingFileAppender
			  collapsed:: true
				- 功能：将日志写入滚动日志文件。
				- 解决的问题：将所有内容都记录到一个文件中并不理想。定期滚动活动日志文件通常要好得多。也就是说他会在某个条件被触发的时候将现有的日志文件存档，新起一个文件进行日志记录。
				- 配置滚动策略
				  collapsed:: true
					- 配置滚动策略意味着确认如何滚动日志，或者说是何时创建一个新的文件。
					- `OnStartupTriggeringPolicy`：每次 JVM 启动时都会创建一个新的日志文件
					  `TimeBasedTriggeringPolicy`：日志文件根据日期/时间模式滚动
					  `SizeBasedTriggeringPolicy`：当文件达到一定大小时滚动
				- 参考配置
				  :LOGBOOK:
				  CLOCK: [2023-03-24 Fri 21:35:46]
				  :END:
				  下面的滚动策略是每天滚动日志或是文件大于10MB时滚动。
				  ```xml
				  <Configuration status="DEBUG">
				      <Appenders>
				          <Console name="LogToConsole" target="SYSTEM_OUT">
				              <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
				          </Console>
				          <RollingFile name="LogToRollingFile" fileName="logs/app.log"
				                      filePattern="logs/$${date:yyyy-MM}/app-%d{MM-dd-yyyy}-%i.log.gz">
				  			<PatternLayout>
				  				<Pattern>%d %p %c{1.} [%t] %m%n</Pattern>
				  			</PatternLayout>
				  			<Policies>
				  				<TimeBasedTriggeringPolicy />
				  				<SizeBasedTriggeringPolicy size="10 MB"/>
				  			</Policies>
				  		</RollingFile>
				      </Appenders>
				  	
				      <Loggers>
				          <!-- avoid duplicated logs with additivity=false -->
				          <Logger name="com.mkyong" level="debug" additivity="false">
				              <AppenderRef ref="LogToRollingFile"/>
				          </Logger>
				          <Root level="error">
				              <AppenderRef ref="LogToConsole"/>
				          </Root>
				      </Loggers>
				  </Configuration>
				  ```
				- DefaultRolloverStrategy
			- RollingRandomAccessFileAppender
			  collapsed:: true
				- RollingFileAppender相似，但速度更快。
			- AsyncAppender
			  collapsed:: true
				- 功能：异步记录日志，提高性能。
			- SMTPAppender
			- JDBCAppender
			  collapsed:: true
				- 功能：将日志记录到数据库
			- FailoverAppender
			  collapsed:: true
				- 功能：配置一个故障转移策略Appender，在配置的主Appender失败时，就可以使用这个故障转移Appender做备份。
				- 例如，可以配置一个主 JDBCAppender，如果无法建立数据库连接，可以配置一个辅助的 RollingFile 和 Console appender：
				  ```xml
				  <Failover name="FailoverAppender" primary="JDBCAppender">
				      <Failovers>
				          <AppenderRef ref="RollingFileAppender" />
				          <AppenderRef ref="Console" />
				      </Failovers>
				  </Failover>
				  ```
			- RoutingAppender
				-
		- 配置布局
		  collapsed:: true
			- 通过使用布局来定义日志消息的格式。
			- Log4j2提供的常用布局：
			  collapsed:: true
				- *PatternLayout*：根据字符串规则配置消息格式
					- 该机制主要由包含转换说明符的转换模式驱动。每个说明符以% 符号开始，后面跟着控制消息的宽度和颜色等内容的修饰符，以及表示内容的转换字符，如日期或线程名称。
					- 关于说明符的含义的解释参考： [PatternLayout](https://logging.apache.org/log4j/2.x/manual/layouts.html#PatternLayout)
				- *JsonLayout*：为日志消息定义JSON格式
				- *CsvLayout*：可用于创建CSV格式的消息
		- 配置过滤器
		  collapsed:: true
			- Log4j2中的筛选器用于确定是否应处理或跳过日志消息。
			- 可以为**整个配置**或在**日志记录器**或**追加器**三个级别上配置筛选器。
			- 过滤器类型
				- `BurstFilter`：控制允许的日志事件数。
				  collapsed:: true
					- 例如控制日志输出的速率
					  下面的配置中level="info"说明将有选择地忽略 INFO 级别及以下级别消息的流量控制，同时确保您不会丢失任何高于 INFO 的更重要的消息。
					  rate 定义每秒应处理的平均日志消息数。
					  maxBurst 控制过滤器开始消除日志条目之前流量突发的总体大小。
					  ```xml
					  <Filters>
					      <BurstFilter level="INFO" rate="10" maxBurst="100"/>
					  </Filters>
					  ```
				- `DynamicThresholdFilter`：基于特定属性的过滤器日志行
				- `RegexFilter`：根据消息是否与正则表达式匹配来筛选消息
		- 配置Loggers
			- 属性
				- `name`：记录器名称
				- `level`：记录器记录的日志级别，默认为ERROR
				- `additivity`：是否支持与Root记录器叠加使用，默认为true
				- `AppenderRef`：一个记录器（Logger）可以配置多个追加器（Appender），如果配置了多个追加器，在处理日志记录事件的时候将分别调用每一个追加器。
				- includeLocation：
			- 必须配置一个Root记录器
			- Root记录器与其他记录器的区别
				- 根记录器没有名称属性。
				- 根记录器不支持additivity属性，因为它没有父记录器。
		- 使用MDC增强日志
			- 参考文章
				- [Improved Java Logging with Mapped Diagnostic Context (MDC)](https://www.baeldung.com/mdc-in-log4j-2-logback)
		- 异步日志
			-
		- Pattern Layouts format配置
		  collapsed:: true
			- 以下面这段配置为例，更多具体的配置参考： [Pattern Layout](https://logging.apache.org/log4j/2.x/manual/layouts.html#PatternLayout) 
			  collapsed:: true
			  ```
			  %date{yyyy-MM-dd HH:mm:ss.SSS} [%thread] [%level{length=5}] %logger{36}.%M(%line) - %msg %n
			  ```
				- `%date{yyyy-MM-dd HH:mm:ss.SSS}`：它以给定的日期-时间格式写入日期。
				- `%thread`：它在日志中写入线程名称。
				- `%level{length=5}`：它在日志中写入级别。`length=5`中的5将字段的宽度设置为5个字符。
				- `%logger{36}`：它在日志中写入日志记录器的名称(例如com.jcg.log4j2.demo)，36是指记录日记记录器的精度，先固定写成36。
				- `%M`：记录日志输出所在的方法。
				- `%line`：记录日志输出所在的代码行号。
				- `%line`：它在日志中写入行号。
				- `%msg`：将消息写入日志。
				- `%n`：换行，输出与平台相关的行分隔符字符。
		- 实践
		  collapsed:: true
			- Log4j2的简单实战
			  collapsed:: true
				- 项目：Log4j2Example
				- 参考文章：https://examples.javacodegeeks.com/java-development/enterprise-java/log4j/log4j-2-getting-started-example/
	- commons-logging
	- Slf4j
	  collapsed:: true
		- 是一个门面框架，只定义接口，没有具体的实现。在日常使用时调用Slf4j的接口就行，底层的日志实现有具体的日志实现框架去做。
		- 背景
		  collapsed:: true
			- 市面上出现多种日志实现工具，场面十分混乱，因为这些日志系统互相没有关联，替换和统一也就变成了比较棘手的一件事。
	- Logback
	- 日志级别（以下等级由高到低，等级越低输出的日志信息越多）
	  collapsed:: true
		- Fatal：致命等级的日志，指发生了严重的会导致应用程序退出的事件
		- Error：错误等级的日志，指发生了错误，但是不影响系统运行；
		- Warn：警告等级的日志，指发生了异常，可能是潜在的错误；
		- Info：信息等级的日志，指一些在粗粒度级别上需要强调的应用程序运行信息；
		- Debug：调试等级的日志，指一些细粒度的对于程序调试有帮助的信息；
		- Trace：跟踪等级的日志，指一些包含程序运行详细过程的信息。
	- 日志记录主要分为三部分
	  collapsed:: true
		- Logger：Logger负责捕获要记录的消息以及某些元数据，并将其传递给日志框架。
		- Formatter：在接收到消息后，框架使用该消息调用Formatter。Formatter为输出格式化它。
		- Appender：框架将格式化的消息交给适当的Appender处理。可能包括控制台显示、写入磁盘、追加到数据库或电子邮件。
	- `System.out.println()`的局限性
	  collapsed:: true
		- 任何日志框架都允许开发人员将调试信息记录到可以用作过滤标准的日志级别，即可以禁用属于特定日志级别的消息。例如，在生产环境中，开发人员更关心WARN消息而不是DEBUG消息。
		- 日志框架可以产生更好的输出和元数据，这有助于故障排除和调试。例如，Log4j2允许通过指定格式化模式来打印格式化输出，即使用PatternLayout可以包括时间戳、类名等。
- 测试框架
  collapsed:: true
	- Junit
	  collapsed:: true
		- 参考文章
			- [Spring Boot 基于 JUnit 5 实现单元测试](https://www.jianshu.com/p/4648fd55830e)
- 开发框架
  collapsed:: true
	- Spring
	  collapsed:: true
		- Spring Test
		  collapsed:: true
			- 在单元测试中如果依赖Spring的RequestContext，怎么办
				- 先看代码：
				  ```Java
				  // Spring-test 有一个灵活的请求模拟，称为 MockHttpServletRequest。
				  MockHttpServletRequest request = new MockHttpServletRequest();
				  RequestContextHolder.setRequestAttributes(new ServletRequestAttributes(request));
				  ```
				- 参考文章
					- [How to Mock HttpServletRequest](https://www.baeldung.com/java-httpservletrequest-mock)
		- Spring core
			- IOC的实现
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
					- [Using @Autowired in Abstract Classes](https://www.baeldung.com/spring-autowired-abstract-class)
			- 注解@Scope
			  collapsed:: true
				- 作用
					- Scope，也称作用域，在 Spring IoC 容器是指其创建的 Bean 对象相对于其他 Bean 对象的请求可见范围。
				- Spring IoC容器的作用域
					- 基本作用域
						- `singleton`：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例。
						- `prototype`：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例。
					- Web 作用域
						- `reqeust`：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效。
						- `session`：对于每次HTTP Session，使用session定义的Bean都将产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效。
						- `globalsession`：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效。
					- 自定义作用域。
		- Spring Web
		  collapsed:: true
			- @RequestBody中的required默认是true，这个接口必须要传输json格式的数据，假如没有数据，就会报错：`Required request body is missing`。如果我们要自己做数据校验的话，可以将required设置为false。
		- Spring Boot
		  collapsed:: true
			- 依赖管理
			  collapsed:: true
				- Spring Boot 的每个版本都提供了它支持的依赖项列表，因此，我们在引入其他的依赖时不需要在配置中指定依赖项的版本，Spring Boot会自行管理。具体可以参考文章：[springboot依赖的一些配置：spring-boot-dependencies、spring-boot-starter-parent、io.spring.platform](https://www.cnblogs.com/leeego-123/p/12665279.html)
			- 上传文件
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
				- Spring Boot 默认使用 SLF4J+Logback 记录日志，其中SLF4J提供了日志接口，Logback提供的日志实现。
				- 日志配置的级别
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
					- [使用SLF4J和Logback-廖雪峰](https://www.liaoxuefeng.com/wiki/1252599548343744/1264739155914176)
					- [Spring Boot日志配置及输出](http://c.biancheng.net/spring_boot/log-config.html)
		- Spring Cloud
		  collapsed:: true
			- [spring-cloud-release](https://github.com/spring-cloud/spring-cloud-release)
			  collapsed:: true
				- 该项目的作用就是管理SpringCloud版本的发布，主要做了二件事，一个是分布版本的规则，二是管理各个发布版本的子项目的版本的映射关系。
				- 参考文章： https://www.cnblogs.com/hzhuxin/p/12393456.html
			- Open Feign
				- 配置规则
					- 第一种：自定义配置类
						- 自定义FeignClientsConfiguration配置类
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