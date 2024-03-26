- CAP理论
- BASE理论
- ZAB协议
	- ZAB（ZooKeeper Atomic Broadcast）协议是 Zookeeper 用于保证数据一致性的一种分布式协议。它基于一种类似于两阶段提交（2PC）的算法，用于在分布式系统中实现原子广播。
	- ZAB 协议的主要目标是确保所有节点对数据的变更达成一致，并保证数据的顺序性和一致性。协议分为三个阶段：
	  	1.	领导者选举：在 ZooKeeper 集群中，通过选举产生一个领导者节点。只有领导者节点可以接受客户端的写请求。
	  	2.	提案阶段：当领导者接收到一个写请求时，它会生成一个提案（Proposal），并将其发送给所有的追随者节点。提案包含了要更新的数据、事务 ID 以及纪元号。
	  	3.	原子广播阶段：领导者等待大多数（超过半数）的追随者节点响应提案。如果收到足够的响应，领导者会将提案标记为已提交（Committed），并将结果广播给所有的追随者节点。如果在等待过程中领导者发生故障或失去连接，其他节点会重新进行领导者选举。
	- ZAB 协议通过使用领导者选举和原子广播机制，确保了数据的一致性和顺序性。同时，它还提供了崩溃恢复机制，以应对领导者节点的故障。
- 功能
  collapsed:: true
	- 1.数据一致性：Zookeeper 保证了分布式系统中数据的一致性。通过使用 ZAB 协议（Zookeeper Atomic Broadcast），Zookeeper 可以确保所有节点上的数据都是最新的、一致的。
	- 2.	服务发现：Zookeeper 可以帮助应用程序发现其他服务或节点的存在。应用程序可以在 Zookeeper 中注册服务，并通过监听 Zookeeper 节点的变化来获取服务的信息。
	- 3.	命名服务：Zookeeper 提供了一个全局的命名空间，用于给分布式系统中的资源或服务分配唯一的标识符。
	- 4.	配置管理：应用程序可以将配置信息存储在 Zookeeper 中，并且可以通过监听 Zookeeper 节点的变化来实时获取配置的更新。
	- 5.	领导者选举：Zookeeper 可以用于在分布式系统中选举领导者。各个节点可以在 Zookeeper 中创建一个临时节点，拥有该临时节点的节点即为领导者。
	- 6.	分布式锁：Zookeeper 可以用于实现分布式锁。通过在 Zookeeper 中创建一个临时节点，当且仅当一个客户端持有该临时节点时，才能获取锁。
	- 7.	队列管理：Zookeeper 可以用于实现简单的队列管理。客户端可以在 Zookeeper 中创建一个顺序节点，从而形成一个队列。
- Zookeeper客户端curator的使用
	- [Zookeeper客户端框架curator使用详解](https://juejin.cn/post/6984742386744164388?searchId=2024032015450699D3B90A54B0C6279D3A)
	- [Apache Curator Framework教程（一）](https://zhuanlan.zhihu.com/p/603185454)
- Zookeeper常用命令
	- `ls -s /path`和`stat /path`：都是用来查看节点状态的。
		- 数据项说明：
		    collapsed:: true
			- `czxid` 创建该节点的事物ID
			- `ctime` 创建该节点的时间
			- `mZxid` 更新该节点的事物ID
			- `mtime` 更新该节点的时间
			- `pZxid` 操作当前节点的子节点列表的事物ID(这种操作包含增加子节点，删除子节点)
			- `cversion` 当前节点的子节点版本号
			- `dataVersion` 当前节点的数据版本号
			- `aclVersion` 当前节点的acl权限版本号
			- `ephemeralowner` 当前节点的如果是临时节点，该属性是临时节点的事物ID
			- `dataLength` 节点存储的数据长度
			- `numchildren` 当前节点的子节点个数
	- `ls /path`：用于查看某个路径下目录列表。
	- 具体的命令参考官方文档：https://zookeeper.apache.org/doc/r3.9.2/zookeeperCLI.html
- 数据节点
	- 节点的创建模式
		- PERSISTENT：持久化节点
		- PERSISTENT_SEQUENTIAL：持久化顺序节点
		- EPHEMERAL：临时节点
		- EPHEMERAL_SEQUENTIAL：临时顺序节点
	- 顺序节点：创建顺序节点后，节点名称会拼接一个递增的十位序列号，比如我创建的路径是`/order`，得到的节点名称就是`order0000000001`。
- Zookeeper官网：https://zookeeper.apache.org/
- 教程
	- [ZooKeeper 入门教程](https://luyuhuang.tech/2021/05/02/zookeeper.html#%E6%95%B0%E6%8D%AE%E5%AD%98%E5%82%A8)