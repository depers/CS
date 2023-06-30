- 《Kubernetes实战》
	- 第一章 Kubernetes介绍
		- 单体应用部署遇到的问题
		- 微服务应用部署遇到的问题
		- 容器技术
			- Linux的Namespace技术
				- `Namespace`的作用是环境隔离，它让应用程序只看到该`Namespace`内的世界，诸如文件系统、用户ID、网络接口等。
			- Linux的Cgroups技术
				- Cgroups 的作用是限制分配给进程的宿主机资源，诸如CPU、内存和网络带宽等。
		- Kubernetes的作用
			- 为应用的开发和部署提供一致的系统环境，包括网络，依赖，系统配置等。
			- 让开发人员专注应用开发，让运维人员专注系统基础设施的维护。
		- 容器技术的介绍
			- Kubernetes使用Linux容器技术来提供应用的隔离，现有的容器技术有docker和rkt。
	- 第二章 开始使用Kubernetes和docker
	  collapsed:: true
		- 3.在Kubernetes上运行第一个应用
			- Pod的介绍
				- 一个工作节点上可以运行多个Pod，一个Pod上面可以运行多个容器，每个容器是一个进程。
				- kubernetes的基本构件是Pod。
			- ReplicationController
				- ReplicationController用于复制Pod，即创建Pod的多个副本，并让他们保持运行。
	- 第三章 pod：运行于kubernetes中的容器
		- 1.介绍Pod
		  collapsed:: true
			- 一个Pod总是运行在一个工作节点上，他不会跨越多个工作节点。
			- 一个Pod中应该包含一个容器还是多个容器
			- 问题
			  background-color:: red
				- 为什么容器被设计成一个容器中只能运行一个进程？
				  collapsed:: true
					- 每个容器中只运行一个应用程序，则水平伸缩将变得十分容易。例如，当你需要一个Tomcat容器，可以从现有的容器再扩展出一个，但如果你的这个容器中不仅有Tomcat，还有MySQL等其他应用程序，事情就会变得复杂起来。
					- 2、每个容器中只运行一个应用程序，可以轻松地将其重新用于其他项目或目的，极大增加复用度。
					- 3、每个容器中只运行一个应用程序，出现故障时开发人员能方便地对该故障容器进行问题排查，而不必对整个系统的各个部分进行排查，这也使得其更具有可移植性和可预测性。
					- 4、每个容器中只运行一个应用程序，升级程序时能够将影响范围控制在更小的粒度，极大增加应用程序生命周期管理的灵活性，避免在升级某个服务时中断相同容器中的其他进程。
					- 5、每个容器中只运行一个应用程序，从安全性和隔离性角度来看，能够提供更安全的服务和应用程序间的隔离，以保持强大的安全状态或遵守PCI之类的规定。
					- 话说回来，容器本身的设计，就是希望容器和服务/应用能够具备相同的生命周期。即：一个容器对应一个进程。这样，才能够最好地应用容器编排来管理好容器和服务。
		- 2.通过yaml或是json描述文件创建Pod
			- Pod描述文件的主要部分
			  collapsed:: true
				- *metadata*：包括名称、命名空间、标签和关于该容器的其他信息。
				- *spec*：包含 Pod 内容的实际说明，例如Pod的容器、卷和其他数据。
				- *status*：包含运行中pod的当前信息。在创建新的Pod时，这部分信息不需要定义。
			- 通过`kubectl explain pods`或是`kubectl explain pods.spec`来查看pod的描述信息。
			- 为pod创建一个简单的yaml描述文件
			  collapsed:: true
				- 代码
				  ```yaml
				  apiVersion: v1
				  kind: Pod
				  metadata:
				  	name: kubia-biz
				  spec:
				      containers:
				      - images: luksa/kubia
				        name: kubia
				        ports:
				        - containerPort: 8080
				          protocol: TCP
				  ```
			- 创建一个Pod
			- 查看Pod中的应用日志
			- 向Pod发送请求
	- kubectl的命令
		- `kubectl get pods`
		- `kubectl get services`
		- `kubectl get ReplicationControllers`
		- `kubectl get po <pod名称> -o yaml`
		  collapsed:: true
			- 获取pod完整的YAML定义。
		- `kubectl create -f <pod描述文件.yaml>`
		  collapsed:: true
			- 用于从yaml或是json文件中创建pod。
		- `kubectl log <pod名称>`
		  collapsed:: true
			- 容器化的应用程序会将日志记录到标准输出和标准错误流，而不是写入文件。
			- 我们可以通过上述命令查看pod的日志。
		- `kubectl log <pod名称> -c <容器名称>`
		  collapsed:: true
			- 获取多容器pod的日志时指定容器名称。
			- 值得注意的是这个命令只能获取仍然存在于pod中的日志。
		- `kubectl port-forward <pod名称> 8888:8080`
		  collapsed:: true
			- 将请求本地8888端口的请求转发到Pod的8080端口上。
		-