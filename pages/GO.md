- 语言基础
	- 运行go语言文件：`go run <xxx.go>`
	- 编译go语言文件为二进制文件，编译后的二进制文件可以直接执行：`go build <xxx.go>`
	- 数据类型
	  collapsed:: true
		- 字符串
		- 整数
		- 浮点数
		- 布尔值
	- 变量声明
	  collapsed:: true
		- 字符串声明：`var a = "apple"`，或者`var s string = "apple"`，或者`a := "apple"`
		- 整数声明：`var b int = 1`，或者`var b = 1`
		- 布尔值声明：`var c = true`，或者`var c bool = true`
		- 声明并初始化：`f := "apple"`，就等同于：`var f string = "apple"`
		- 声明多个变量：`var a, b int = 1, 2`
		- go可以默认自动推测数据类型。
	- 声明常量
	- For循环
	- IF/Else语句
	- Switch语句
	- 数组
	  collapsed:: true
		- 在 Go 语言中，数组是一组固定长度的元素的集合。数组的长度是在创建数组时指定的，且不能更改。数组中的元素类型必须相同，可以是任何基本类型或结构体类型。
	- 切片
	  collapsed:: true
		- 感觉使用上和数组是类似的。
		- 在 Go 语言中，切片是一个动态长度的序列，可以通过对底层数组的引用来实现。切片中的元素类型必须相同，可以用于存储任何类型的元素，且可以动态扩展和收缩。
		- [Go 数组与切片的区别](https://blog.csdn.net/GeeCode/article/details/131465820)
			- 内部结构
			  collapsed:: true
				- 数组在内存中是一段连续的内存空间，元素的类型和长度都是固定的。切片在内存中由一个指向底层数组的指针、长度和容量组成，长度表示切片当前包含的元素个数，容量表示切片可以扩展的最大元素个数。
			- 长度
			  collapsed:: true
				- 数组的长度在创建时指定，不能更改。切片的长度可以动态扩展或收缩，可以根据需要自由调整。
			- 使用方式
			  collapsed:: true
				- 数组在使用时需要明确指定下标访问元素，不能动态生成。切片可以使用 append 函数向其末尾添加元素，可以使用 copy 函数复制切片，也可以使用 make 函数创建指定长度和容量的切片。
	- map
	- range
	- 函数声明
	- 函数可以返回多个返回值
	- 可变参数函数
	- 闭包
	  collapsed:: true
		- 定义：闭包是由函数及其相关的上下文组成的实体。
		- 闭包的特点包括：
			- 1.	函数和其外部状态的组合：闭包包含了函数以及函数执行所需的外部变量或状态。
			- 2.	持久性：即使在函数执行结束后，闭包仍然可以保留对外部状态的访问。
			- 3.	隔离性：不同的闭包可以独立地操作和修改其外部状态。
		- JavaScript实现的闭包：
		  ```JavaScript
		  function createCounter() {
		    let count = 0;
		    return function() {
		      return count++;
		    };
		  }
		  
		  let counter = createCounter();
		  console.log(counter()); 
		  console.log(counter()); 
		  console.log(counter());
		  ```
	- 递归
	- 指针
	- 字符串和字符
	  collapsed:: true
		- Go 字符串是只读的字节切片。该语言和标准库将字符串作为以 UTF-8 编码的**文本的容器**。
		- 在其他语言中，字符串是由“字符”组成的。在 Go 中，字符的概念称为 `rune` - 它是表示 Unicode 代码点的整数。
	- 结构体
	- 结构体方法
		- 指针接收器
		- 值接收器
		- 区别
			- 修改接收者的值：使用指针接收器可以通过指针修改接收者的字段值，而值接收器不能直接修改接收者的字段。
			- 效率：在某些情况下，指针接收器可能具有更高的效率。
			- 共享和拷贝：指针接收器共享指向的内存，而值接收器会拷贝整个结构体。
-