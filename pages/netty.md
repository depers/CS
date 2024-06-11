- 跟闪电侠学Netty：Netty即时聊天实战与底层原理
  collapsed:: true
	- 第四章 服务端启动流程
	  collapsed:: true
		- Netty服务端启动的流程，一句话总结就是：首先创建一个引导类，然后给它指定线程模型、IO模型、连接读写处理逻辑，绑定端口之后，服务端就启动起来了
		- 端口动态绑定
		- 其他参数配置
	- 第五章 客户端启动流程
	  collapsed:: true
		- Netty客户端启动流程，首先创建一个引导类，然后为它指定线程模型、IO模型、连接读写处理逻辑，连接上特定主机和端口后，客户端就启动起来了。
		- 设置重连次数
		- 其他参数配置
		-
	- 第十二章
	  collapsed:: true
		- 基于`ByteToMessageDecoder`，可以实现自定义解码，而不用关心`ByteBuf`的强转和解码结果的传递。
		- 基于`SimpleChannelInboundHandler`，可以实现每一种指令的处理，不再需要强转，不再有冗长乏味的`if else`逻辑，不再需要手动传递对象。
		- 基于`MessageToByteEncoder`，可以实现自定义编码，不用关心`ByteBuf`的创建，不用每次向对端写Java对象都进行一次编码。
	- 第十四章 ChannelHandler的生命周期
	  collapsed:: true
		- 这一章主要讲了ChannelHandler的生命周期方法
			- handlerAdded()：当检测到新连接之后。
			- channelRegistered()：当前channel的处理逻辑已和NIO线程建立了绑定关系。
			- `channelActive()`：channel被激活。
			- channelRead()：客户端向服务端发送数据，服务端每次都会回调此方法，表示有数据可读。
			- channelReadComplete()：服务端每读完一次完整的数据，都回调该方法，表示数据读取完毕。
			- channelInactive()：连接已经被关闭了，这个连接在TCP层面已经不再是ESTABLISH状态。
			- channelUnregistered()：连接对应的NIO线程移除了对这个连接的处理。
			- handlerRemoved()：连接添加的所有业务逻辑处理器都被移除。
		-
	- 第十五章 使用ChannelHandler的热插拔实现客户端身份校验
	  collapsed:: true
		- 如果有多个业务逻辑的handler要进行相同的操作，我们可以将这部分逻辑单独抽到一个逻辑中进行实现。例如在server端的校验用户是否登录。
		- 如果某一个独立的逻辑在执行几次之后（这里是一次）不需要再执行，则可以通过`ChannelHandler`的热插拔机制来实现动态删除逻辑，使应用程序的性能处理更为高效。
	- 第十六章 客户端互聊的原理与实现
	  collapsed:: true
		- 使用`SessionUtil`来管理用户`Session`和`Channel`之间的映射关系。
		- 在服务端处理消息的时候，通过用户id获取到用户的`Channel`，从而实现两个客户端信息的交互。
	- 第十七章 群聊的发起和通知
	  collapsed:: true
		- 重新整合了登录，一对一，群聊，登出控制台操作的逻辑。
		- 通过`ChannelGroup`，可以很方便地对一组`Channel`进行批量操作。
	- 第十八章 群聊的成员管理
	  collapsed:: true
		- 这里实现了建群，进群，查看群成员，退群的操作。
	- 第十九章 群聊消息的收发及Netty的性能优化
	  collapsed:: true
		- 群聊消息的收发。
		- 共享Handler
		- 压缩Handler-合并编解码器
		- 压缩Handler-合并平行Handler
		- 更改事假传播源
		  collapsed:: true
			- `ctx.channel().writeAndFlush();`：对象会从最后一个Outbound类型的Handler开始，逐个往前传播，路径要比ctx.writeAndFlush()方法长。
			- `ctx.writeAndFlush()`：可以直接一口气把对象送到codec中编码，然后写出去。
		- 减少主线程的阻塞
		  collapsed:: true
			- 在服务器端的`channelRead0()`方法中如果涉及耗时操作，应放到线程池中进行处理。
		- 如何准确的统计时长
		  collapsed:: true
			- `writeAndFlush()`方法会返回一个`ChannelFuture`对象，我们给这个对象添加一个监听器，然后在回调方法里，可以监听这个方法执行的结果，进而执行其他逻辑，最后统计耗时，这样统计出来的耗时才是最准确的。
- RPC（ Remote Procedure Call ）框架和 HTTP 服务的区别
	- 1.	通信协议：RPC 框架通常使用自定义的协议来进行远程调用，而 HTTP 服务使用的是 HTTP 协议。RPC 框架可以更高效地进行远程方法调用，因为它可以直接传递方法参数和返回值，而不需要进行协议解析和序列化。
	  	2.	数据格式：RPC 框架通常使用自定义的数据格式来序列化和反序列化参数和返回值，而 HTTP 服务通常使用 JSON 、XML 或其他通用的数据格式。RPC 框架的数据格式可以更高效地进行传输，因为它可以针对特定的编程语言和数据类型进行优化。
	  	3.	调用方式：RPC 框架通常采用同步调用方式，即客户端发起调用后会阻塞直到服务器返回结果。而 HTTP 服务可以支持同步和异步调用方式，客户端可以通过发送请求后立即返回，然后通过轮询或回调的方式获取结果。
	  	4.	性能：RPC 框架通常设计为在局域网或高速网络环境下进行高效的远程调用，因此在性能上可能比 HTTP 服务更优。RPC 框架可以通过减少网络开销和数据传输量来提高性能。
	- 对于调用的客户端来说，使用 RPC 框架和 HTTP 服务的主要区别在于调用方式和数据格式。如果你需要高效地进行远程方法调用，并且客户端和服务器使用相同的编程语言和数据类型，那么使用 RPC 框架可能更适合。如果你需要支持多种编程语言和数据格式，或者需要通过 HTTP 协议进行通信，那么使用 HTTP 服务可能更合适。
- 参考文章
	- [Netty入门看这一篇就够了](https://juejin.cn/post/6924528182313893896)