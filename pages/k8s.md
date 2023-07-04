- 《Kubernetes实战》
  collapsed:: true
	- 第一章 Kubernetes介绍
	  collapsed:: true
		- 单体应用部署遇到的问题
		- 微服务应用部署遇到的问题
		- 容器技术
		  collapsed:: true
			- Linux的Namespace技术
			  collapsed:: true
				- `Namespace`的作用是环境隔离，它让应用程序只看到该`Namespace`内的世界，诸如文件系统、用户ID、网络接口等。
			- Linux的Cgroups技术
			  collapsed:: true
				- Cgroups 的作用是限制分配给进程的宿主机资源，诸如CPU、内存和网络带宽等。
		- Kubernetes的作用
		  collapsed:: true
			- 为应用的开发和部署提供一致的系统环境，包括网络，依赖，系统配置等。
			- 让开发人员专注应用开发，让运维人员专注系统基础设施的维护。
		- 容器技术的介绍
		  collapsed:: true
			- Kubernetes使用Linux容器技术来提供应用的隔离，现有的容器技术有docker和rkt。
	- 第二章 开始使用Kubernetes和docker
	  collapsed:: true
		- 3.在Kubernetes上运行第一个应用
		  collapsed:: true
			- Pod的介绍
			  collapsed:: true
				- 一个工作节点上可以运行多个Pod，一个Pod上面可以运行多个容器，每个容器是一个进程。
				- kubernetes的基本构件是Pod。
			- ReplicationController
			  collapsed:: true
				- ReplicationController用于复制Pod，即创建Pod的多个副本，并让他们保持运行。
	- 第三章 pod：运行于kubernetes中的容器
	  collapsed:: true
		- 1.介绍Pod
		  collapsed:: true
			- 一个Pod总是运行在一个工作节点上，他不会跨越多个工作节点。
			- 一个Pod中应该包含一个容器还是多个容器
			- 问题
			  background-color:: red
			  collapsed:: true
				- 为什么容器被设计成一个容器中只能运行一个进程？
				  collapsed:: true
					- 每个容器中只运行一个应用程序，则水平伸缩将变得十分容易。例如，当你需要一个Tomcat容器，可以从现有的容器再扩展出一个，但如果你的这个容器中不仅有Tomcat，还有MySQL等其他应用程序，事情就会变得复杂起来。
					- 2、每个容器中只运行一个应用程序，可以轻松地将其重新用于其他项目或目的，极大增加复用度。
					- 3、每个容器中只运行一个应用程序，出现故障时开发人员能方便地对该故障容器进行问题排查，而不必对整个系统的各个部分进行排查，这也使得其更具有可移植性和可预测性。
					- 4、每个容器中只运行一个应用程序，升级程序时能够将影响范围控制在更小的粒度，极大增加应用程序生命周期管理的灵活性，避免在升级某个服务时中断相同容器中的其他进程。
					- 5、每个容器中只运行一个应用程序，从安全性和隔离性角度来看，能够提供更安全的服务和应用程序间的隔离，以保持强大的安全状态或遵守PCI之类的规定。
					- 话说回来，容器本身的设计，就是希望容器和服务/应用能够具备相同的生命周期。即：一个容器对应一个进程。这样，才能够最好地应用容器编排来管理好容器和服务。
		- 2.通过yaml或是json描述文件创建Pod
		  collapsed:: true
			- Pod描述文件的主要部分
				- *metadata*：包括名称、命名空间、标签和关于该容器的其他信息。
				- *spec*：包含 Pod 内容的实际说明，例如Pod的容器、卷和其他数据。
				- *status*：包含运行中pod的当前信息。在创建新的Pod时，这部分信息不需要定义。
			- 通过`kubectl explain pods`或是`kubectl explain pods.spec`来查看pod的描述信息。
			- 为pod创建一个简单的yaml描述文件
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
	  collapsed:: true
		- kubectl
		  collapsed:: true
			- kubectl是在进行Kubernetes管理的过程中使用的主要命令行工具。
			- kubectl的作用是将对用户友好的命令转换成API Server所能理解的JSON格式。它基于一个配置文件来决定将其POST到哪个集群的API Server。
		- `kubectl get pods`
		  collapsed:: true
			- 查看Pod信息。
			- 拓展命令
				- `-o wide`：能够多输出几列信息。
				- `-o yaml`：能够返回集群存储中的一份完整的关于Pod的清单。
		- `kubectl get services`
		- `kubectl get ReplicationControllers`
		- `kubectl get Pods <pod名称> -o yaml`
		  collapsed:: true
			- 获取pod完整的YAML定义。
		- `kubectl create -f <pod描述文件.yaml>`
		  collapsed:: true
			- 用于从yaml或是json文件中创建pod。
		- `kubectl log <pod名称>`
		  collapsed:: true
			- 容器化的应用程序会将日志记录到标准输出和标准错误流，而不是写入文件。
			- 我们可以通过上述命令查看Pod的日志。
		- `kubectl log <pod名称> -c <容器名称>`
		  collapsed:: true
			- 获取多容器Pod的日志时指定容器名称。
			- 值得注意的是这个命令只能获取仍然存在于pod中的日志。
		- `kubectl port-forward <pod名称> 8888:8080`
		  collapsed:: true
			- 将请求本地8888端口的请求转发到Pod的8080端口上。
		- `kubectl apply -f Pod.yml`
		  collapsed:: true
			- 将清单文件发送到API Server。
		- `kubectl describe Pods <pod名称>`
		  collapsed:: true
			- 该命令会打印出所查看对象的总览信息，其多行格式易于阅读。内容中还包含对象的重要的生命周期事件。
		- `kubectl exec`
		  collapsed:: true
			- 功能：在Pod中执行命令。
			- `-it`
				- 参数`-it`的作用在于使exec的会话成为交互式（interactive）的，并且把当前终端的STDIN和STDOUT与Pod中第一个容器的STDIN和STDOUT连接起来。
- 《Kubernetes修炼手册》
  collapsed:: true
	- 第二章 Kubernetes
	  collapsed:: true
		- Kubernetes
			- 功能：负责应用的部署和管理。
			- 组成
				- 主节点
					- Kubernetes的主节点（master）是组成集群的控制平面的系统服务的集合。
					- 组成
						- API Server
						  collapsed:: true
							- API Server（API服务）是Kubernetes的中央车站。所有组件之间的通信，都需要通过API Server来完成。
						- 集群存储
						  collapsed:: true
							- 在整个控制层中，只有集群存储是有状态（stateful）的部分，它持久化地存储了整个集群的配置与状态。
							  id:: 64a3de66-2124-4341-ad45-112ae95baf5c
							- 通常集群存储底层会选用一种常见的分布式数据库etcd。
						- controller管理器
						  collapsed:: true
							- controller管理器实现了全部的后台控制循环，完成对集群的监控并对事件作出响应。
							- controller管理器是controller的管理者（controller of controller），负责创建controller，并监控它们的执行。
						- 调度器
						  collapsed:: true
							- 调度器的职责就是通过监听API Server来启动新的工作任务，并将其分配到适合的且处于正常运行状态的节点中。
						- 云controller管理器
						  collapsed:: true
							- 云controller管理器负责集成底层的公有云服务
				- 工作节点
					- 功能
						- 监听API Server分派的新任务。
						- 执行新分派的任务。
						- 向控制平面回复任务执行的结果（通过API Server）。
					- 组成
						- Kubelet
							- 功能：负责监听API Server新分配的任务。每当其监听到一个任务时，Kubelet就会负责执行该任务，并维护与控制平面之间的一个通信频道，准备将执行结果反馈回去。
						- 容器运行时
							- 功能：执行依赖容器才能执行的任务，例如拉取镜像并启动或停止容器。
						- kube-proxy
							- 功能：kube-proxy运行在集群中的每个工作节点，负责本地集群网络。
		- Pod
		  collapsed:: true
			- Pod是Kubernetes调度的原子单位。
			- Pod是一种包含了一个或多个容器的结构。
			- Pod是一个用于运行容器的有限制的环境。
			- Kubernetes中最小的调度单元也是Pod。
			- 一个Pod只会被唯一的工作节点调度。这一点对于多容器Pod来说也是一样的，一个多容器Pod中的全部容器都会运行在相同的工作节点上。
			- 对于存在强绑定关系的多个容器，比如需要共享内存与存储，多容器Pod就是一个非常完美的选择。否则尽量在一个Pod上只部署一个容器。
			- 更确切地说，一个Pod就是由一个或多个容器共享的运行环境。
		- Development
		  collapsed:: true
			- 是Pod的更高一层封装。
			- 提供了如扩缩容管理、不停机更新以及版本控制等其他特性。
		- Service
		  collapsed:: true
			- 一个稳定的网络终端，提供了基组动态Pod集合的TCP以及UDP负载均衡能力。
			- Service使用标签（label）与一个标签选择器（label selector）来决定应当将流量负载均衡到哪一个Pod集合。
	- 第四章 Pod的使用
		- Pod的清单文件分析
			- 4个顶级资源
			  collapsed:: true
				- *apiVersion*
					- 用于创建部署对象的API组和API版本，其中API组可以忽略，版本默认是v1。
				- *kind*
					- 指定Kubernetes要部署的对象类型。
					- 这里的值可能是`Pod`，`Deployment`，`Service`
				- *metadata*
					- 用于定义名称、命名空间、标签和关于该容器的其他信息。其中标签就是简单的键值对。
				- *spec*
					- 用于定义Pod所运行的容器。
	- 第五章 Kubernetes Deployment
		-