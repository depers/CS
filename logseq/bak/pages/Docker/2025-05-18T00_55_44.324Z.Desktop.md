- 解决了什么问题
	- **Docker解决了开发、测试和生产环境不一致的问题**。在传统的软件开发过程中，开发环境和生产环境往往存在较大的差异，导致在开发环境中运行良好的应用程序在生产环境中却无法正常运行。而Docker通过统一的容器化封装，使得应用程序在不同的环境中具有一致的运行环境，从而保证了应用程序在各个环境中的稳定性和可靠性。
	- **Docker降低了环境迁移的成本**。在传统的软件开发过程中，环境迁移往往需要耗费大量的时间和人力，而且容易出错。而Docker将应用程序及其依赖项打包成一个独立的容器，使得环境迁移变得简单快捷。只需要将Docker容器一键式拷贝到新的环境中，就可以快速搭建起完整的开发、测试和生产环境。
	- **Docker还简化了软件部署的过程**。在传统的软件部署过程中，需要手动安装和配置应用程序及其依赖项，步骤繁琐且容易出错。而Docker通过自动化的镜像构建和容器管理，简化了部署过程，提高了部署的效率和准确性。同时，Docker还支持快速回滚和版本控制，使得软件部署更加可靠和可控。
- docker与虚拟机的区别
	-
- docker的三个概念
	- 镜像（image）：镜像中包含了应用软件运行的基础设施和应用软件本身。镜像的名称一般由`镜像名:TAG`组成。
	- 容器（container）：容器是镜像创建的运行实例。
	- 仓库（Repository）：存放镜像的仓库，类似与Maven的仓库。
- 构建镜像的两种方式
	- 一基于现有镜像启动一个容器，然后利用容器创建一个新的镜像
	  collapsed:: true
		- 启动现有镜像：`docker run -it $image_name /bin/bash`
		  logseq.order-list-type:: number
		- 对现有镜像进行修改，例如安装一个新的软件到镜像中。
		  logseq.order-list-type:: number
		- 根据容器的更改创建新映像：`docker commit -m "$commit messages" -a "$作者的用户名" $容器id $新的镜像名`
		  logseq.order-list-type:: number
	- 二利用Dockerfile创建镜像
	  collapsed:: true
		- 构建命令：`docker build -t $image_name -f $Dockerfile_path`
- 容器的基本操作
	- 基于镜像启动容器：`docker run -it 镜像名称/镜像tag /bin/bash`
	  collapsed:: true
		- `-i`：表示打开并保持标准输出。
		- `-t`：分配一个终端。
		- `-p`
		- `-v`
		- `-u`
		- `-e`
	- 后台启动容器：`docker run -dit 镜像名称/镜像tag /bin/bash`
		- `-d`：使这个容器处于后台运行的状态，不会对当前终端产生任何输出，所有的stdout都输出到log，可以使用`docker logs container_name或container_id`查看。
	- 启动容器命令：`docker start container_name或container_id`
	- 停止容器命令：`docker stop container_name或container_id`
	- 重启容器命令：`docker restart container_name或container_id`
	- 启动容器之后想进入容器，输入命令：`docker attach container_name或container_id`
	- 删除容器：`docker rm container_name或container_id`
	- 删除镜像：`docker rmi image_name:tag/image_id`
	- 为镜像image修改tag：`docker tag [IMAGE ID] [REPOSITORY名]:[TAG标识]`
	- `docker images`
		- 功能：列出本地镜像。
		- `-a`：列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；
	- 查看运行中的镜像：`docker ps`
- 仓库的基本操作
	- 注册[docker hub](https://hub.docker.com/)公共仓库
	- 登录，命令`docker login $address -u$username $password`
	- 推送本地仓库镜像到远程仓库：`docker push $image_name`
	- 拉取远程仓库镜像到本地：`docker pull $image_name`
	- 更新镜像的两种方式，与创建镜像的两种方式一样
		- 创建容器之后做更改，之后commit生成镜像，然后push到仓库中。
		- 更新Dockerfile。在工作时一般建议这种方式，更简洁明了。
- 容器中的数据管理
  collapsed:: true
	- 数据卷
	  collapsed:: true
		-
	- 数据卷容器
	  collapsed:: true
		-
- Dockerfile
	- 命令参数
		- `FROM`：构建镜像基于哪个镜像。
		  collapsed:: true
			- 作用：定制的镜像都是基于 FROM 的镜像，通过这个命令指定基础镜像。
			- 命令格式：`FROM 基础镜像`
		- `RUN`：构建镜像时运行的指令。
		  collapsed:: true
			- 作用：用于执行后面跟着的命令行命令。
			- **值得注意**的是docker每运行一次`RUN`命令都会在镜像文件上新建一层，使用多条RUN命令会造成镜像文件过大。建议多条`RUN`命令使用`&&`连接为一条指令，这样只会创建一层镜像。
			- 命令格式
			  collapsed:: true
				- shell命令：`RUN <shell命令>`
				  logseq.order-list-type:: number
				- 可执行文件：`RUN ["可执行文件", "参数1", "参数2"]`
				  logseq.order-list-type:: number
		- `CMD`：运行容器时执行的shell环境。
			- 作用：为启动的容器指定默认要运行的程序，程序运行结束，容器也就结束。`CMD`指令指定的程序可被`docker run`命令行参数中指定要运行的程序所覆盖。
			- 类似于 RUN 指令，用于运行程序，但二者运行的时间点不同。
				- CMD 是在`docker run`时运行。
				- RUN 是在`docker build`时运行。
			- **注意**：如果 Dockerfile 中如果存在多个`CMD`指令，仅最后一个生效。
			- 命令格式
				- `CMD <shell 命令>`
				  logseq.order-list-type:: number
				- `CMD ["<可执行文件或命令>","<param1>","<param2>",...]`
				  logseq.order-list-type:: number
				- `CMD ["<param1>","<param2>",...]  # 该写法是为 ENTRYPOINT 指令指定的程序提供默认参数`
				  logseq.order-list-type:: number
		- `ENTRYPOINT`：运行容器时执行的shell命令。
		  collapsed:: true
			- 作用
			  collapsed:: true
				- 类似`CMD`指令，但其参数不会被`docker run`的命令行参数指定的指令所覆盖，其命令行参数会被当作参数送给 `ENTRYPOINT` 指令指定的程序。
				- 如果运行`docker run`时使用了`--entrypoint`选项，将覆盖`ENTRYPOINT`指令指定的程序。
			- **优点**：在执行`docker run`的时候可以指定`ENTRYPOINT`运行所需的参数。
			- **注意**：如果 Dockerfile 中如果存在多个`ENTRYPOINT`指令，仅最后一个生效。
			- 命令格式：`ENTRYPOINT ["<executeable>","<param1>","<param2>",...]`
		- `COPY`：拷贝文件或目录到容器中，跟ADD类似，但不具备自动下载或解压的功能。
			- 作用：复制指令，将主机上的资源复制或加入到容器镜像中，都是在构建镜像的过程中完成的。
			- 命令格式：`COPY <源路径1>...  <目标路径>`
			- 这个命令执行文件复制时，**复制的文件目录是以Dockerfile为根目录进行复制的**，切记。
			- `COPY ./floder1 /var/`：这句命令的意思是将floder1文件夹下的文件全部复制到容器的/var目录下。
			- `COPY ./floder1 /var/floder1/`：这句命令的意思是将floder1文件夹复制到/var目录下。
		- `ADD`：拷贝文件或目录到容器中，如果是URL或压缩包便会自动下载或自动解压。
		  collapsed:: true
			- 作用：ADD 指令和 COPY 的使用格类似（同样需求下，官方推荐使用 COPY），功能也类似。
			- 命令格式：`ADD <源路径1>...  <目标路径>`
			- COPY指令和ADD指令的唯一区别：**是否支持从远程URL获取资源。**
			  collapsed:: true
				- `COPY`指令只能从执行docker build所在的主机上读取资源并复制到镜像中。
				- `ADD`指令还支持通过URL从远程服务器读取资源并复制到镜像中。
				- Docker开发者推荐：满足同等功能的情况下，推荐使用`COPY`指令。`ADD`指令更擅长读取本地tar文件并解压缩。
		- `ARG`：构建时指定的一些参数。
			- 作用：用于定义构建参数。它允许在构建镜像时从外部传递参数。
			- 当我们使用`docker build`命令构建映像时，可以使用`--build-arg`选项来传递该参数的值。例如：`docker build --build-arg VERSION=2.0 .`这里将`VERSION`参数的值设置成了2.0。
			- 如果要在dockerfile文件中使用`ARG`命令配置的参数，需要使用`$`符号，如下：
			   ```docker
			   AGR APP_NAME=my-app
			   WORKDIR $APP_NAME
			  ```
		- `ENV`：设置容器环境变量。
			- 作用：用于定义环境变量。这些变量在容器运行时是可用的，并且可以在容器内部的任何进程中使用。
			- `ENV`与`ARG`的区别
			  collapsed:: true
				- `ARG`和`ENV`指令的最大区别在于它们的**作用域**。`ARG`指令定义的参数**仅在构建映像期间可用**，而`ENV`指令定义的环境变量**在容器运行时可用**。因此，你可以使用`ARG`指令来**传递构建参数**，而使用`ENV`指令来**设置容器的环境变量**。
				  ![arg和env的区别.webp](../assets/arg和env的区别_1689575028581_0.webp)
		- `EXPOSE`：声明容器的服务端口（仅仅是声明）。
		  collapsed:: true
			- 作用
			  collapsed:: true
				- 声明端口，帮助镜像使用者理解这个镜像服务的守护端口，以方便配置映射。
				- 在运行时使用随机端口映射时，也就是`docker run -P`时，会自动随机映射`EXPOSE`的端口。
			- 命令格式：`EXPOSE <端口1> [<端口2>...]`
		- `WORKDIR`：为 `RUN`、`CMD`、`ENTRYPOINT`、`COPY` 和 `ADD` 设置工作目录，就是切换目录。
		  collapsed:: true
			- 作用
			  collapsed:: true
				- 指定工作目录。
				- 用`WORKDIR`指定的工作目录，会在构建镜像的每一层中都存在。`docker build`构建镜像过程中的，每一个`RUN`命令都是新建的一层。只有通过`WORKDIR`创建的目录才会一直存在。
			- 命令格式：`WORKDIR <工作目录路径>`
		- `MAINTAINER`： 镜像维护者信息。
		- `VOLUME`：定义数据卷，如果没有定义则使用默认。
		- `USER`：指定后续执行的用户组和用户。
		- `HEALTHCHECH`：健康检测指令。
	- 上下文路径
	  collapsed:: true
		- 定义：是指 docker 在构建镜像，有时候想要使用到本机的文件（比如复制），`docker build`命令得知这个路径后，会将路径下的所有内容打包。
		- 如果未说明最后一个参数，那么默认上下文路径就是 Dockerfile 所在的位置。这个参数一般在最后，比如下面的`.`
		  ```shell
		  $ docker build -t nginx:v3 .
		  ```
		- **注意**：上下文路径下不要放无用的文件，因为会一起打包发送给 docker 引擎，如果文件过多会造成过程缓慢。
- 参考文章
  collapsed:: true
	- [只要一小时，零基础入门Docker](https://zhuanlan.zhihu.com/p/23599229)
	- [Docker进阶：容器中的数据管理](https://zhuanlan.zhihu.com/p/23630443)