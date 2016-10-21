# Docker

### Docker 常用命令
一. Docker操作：

1. 查看目前系统中安装的Docker版本：
	
		MacBook-Pro-6:apk belinda$ docker version

   返回：
   
		Client:
 		Version:      1.12.1
 		API version:  1.24
 		Go version:   go1.7.1
 		Git commit:   6f9534c
 		Built:        Thu Sep  8 10:31:18 2016
 		OS/Arch:      darwin/amd64
		
		Server:
 		Version:      1.12.1
 		API version:  1.24
 		Go version:   go1.6.3
 		Git commit:   23cf638
 		Built:        Thu Aug 18 17:52:38 2016
 		OS/Arch:      linux/amd64
 		
2. 查看系统中安装的docker信息：
		
		MacBook-Pro-6:apk belinda$ docker info
   返回：
    	
    	`Containers` : 4
 		Running: 0
 		Paused: 0
 		Stopped: 4
		`Images`: 5
		Server Version: 1.12.1
		Storage Driver: aufs
 		Root Dir: /var/lib/docker/aufs
 		Backing Filesystem: extfs
 		Dirs: 81
 		Dirperm1 Supported: true
		Logging Driver: json-file
		Cgroup Driver: cgroupfs
		Plugins:
 		Volume: local
 		Network: host bridge null overlay
		Swarm: inactive
		Runtimes: runc
		Default Runtime: runc
		Security Options: seccomp
		Kernel Version: 4.4.20-moby
		Operating System: Alpine Linux v3.4
		OSType: linux
		Architecture: x86_64
		CPUs: 2
		Total Memory: 1.953 GiB
		Name: moby
		ID: H3QW:I2CM:HNTN:D4OL:6HMI:RNU3:CJMB:LP2K:AIL6:GTRI:QYUR:6DXN
		Docker Root Dir: /var/lib/docker
		Debug Mode (client): false
		Debug Mode (server): true
 		File Descriptors: 16
 		Goroutines: 27
 		System Time: 2016-10-21T07:13:20.198647414Z
 		EventsListeners: 1
		No Proxy: *.local, 169.254/16
		Registry: https://index.docker.io/v1/
		Insecure Registries:127.0.0.0/8


    容器和镜像的区别：
    
      	`Containers` : 4
 		Running: 0
 		Paused: 0
 		Stopped: 4
		`Images`: 5
		
	`Image`: 镜像。 假设Linux内核是第0层，那么无论怎么运行Docker，它都是运行于内核层之上的。这个Docker镜像，是一个只读的镜像，位于第1层，它不能被修改或不能保存状态。
    `Containers`:容器。在所有的镜像层之上增加一个可写层。这个可写层有运行在CPU上的进程，而且有两个不同的状态：运行态（Running）和退出态（Exited）。这就是Docker容器。
    
 类型     |创建命令          |启动命令 |状态           |支持的操作           |注意事项 |
---------|-----------------|-------|---------------|-----------------|--------|
Image    | pull            | 无     |无               | 参见二 Image   |镜像是只读的，不能修改，也不能保存状态 |
Container|Docker Run IMG|Docker run| Running/exited|  参见三 Container | 运行态->停止态:我们对容器所做的一切变更都会永久地写到容器的文件系统,对容器的变更是写入到容器的文件系统的，而不是写入到Docker镜像中的|

3. 登录registry server（Login）	
		
		docker login

二. Image（镜像）操作 (search$pull, images,rmi,history)

假设Linux内核是第0层，那么无论怎么运行Docker，它都是运行于内核层之上的。这个Docker镜像，是一个只读的镜像，位于第1层，它不能被修改或不能保存状态。

一个Docker镜像可以构建于另一个Docker镜像之上，这种层叠关系可以是多层的。第1层的镜像层我们称之为基础镜像（Base Image），其他层的镜像（除了最顶层）我们称之为父层镜像（Parent Image）。这些镜像继承了他们的父层镜像的所有属性和设置，并在Dockerfile中添加了自己的配置。

Docker镜像通过镜像ID进行识别。镜像ID是一个64字符的十六进制的字符串。但是当我们运行镜像时，通常我们不会使用镜像ID来引用镜像，而是使用镜像名来引用。

1. 列出系统当前所有镜像：

    命令：
	
		docker images

  	返回：
    	
    	REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
		bitnami/redmine               latest              7182adb23bf7        8 weeks ago         408.9 MB
		gitlab/gitlab-ce              latest              6502a773769a        8 weeks ago         1.205 GB
		jenkins                       latest              753c2e1bdef7        10 weeks ago        715.4 MB
		hello-world                   latest              c54a2cc56cbb        3 months ago        1.848 kB
		kitematic/hello-world-nginx   latest              03b4557ad7b9        16 months ago       7.913 MB
		
  	标签tag：镜像可以发布不同版本，这种机制我们称之为标签。
  
2. 删除 Image镜像
        
   		docker rmi image_name
3. 查找并下载镜像：
		
		docker search image_name
		docker pull image_name
4. 查看Images的历史信息

	命令：
		
		docker history image_name	
5. 保存&加载镜像（Save，load）

	当需要把一台机器上的镜像迁移到另一台机器的时候，需要保存镜像与加载镜像

	本地操作：
 	
 	－ 保存镜像到一个tar包：
 		
 		docker save image_name -o file_path
 － 加载一个tar包格式的镜像
        
    	docker load －i file_path
 － 从机器A——机器B
 		
 		机器A：docker save image_name > /home/save_img.tar
 		机器B：docker load < /home/save_img.tar
 		
6. 发布Image
	
		docker push new_image_name

	 
三. Container（容器）操作

docker run imagename，会在所有的镜像层之上增加一个可写层。这个可写层有运行在CPU上的进程，而且有两个不同的状态：
	
	- 运行态（Running）
	- 退出态（Exited）
这就是Docker容器。当我们使用docker run启动容器，Docker容器就进入运行态，当我们停止Docker容器时，它就进入退出态。

当我们有一个正在运行的Docker容器时，从运行态到停止态，我们对它所做的一切变更都会永久地写到容器的文件系统中。要切记，对容器的变更是写入到容器的文件系统的，而不是写入到Docker镜像中的。

我们可以用同一个镜像启动多个Docker容器，这些容器启动后都是活动的，彼此还是相互隔离的。我们对其中一个容器所做的变更只会局限于那个容器本身。

如果对容器的底层镜像进行修改，那么当前正在运行的容器是不受影响的，不会发生自动更新现象。

如果想更新容器到其镜像的新版本，那么必须当心，确保我们是以正确的方式构建了数据结构，否则我们可能会导致损失容器中所有数据的后果。

64字符的十六进制的字符串来定义容器ID，它是容器的唯一标识符。容器之间的交互是依靠容器ID识别的，由于容器ID的字符太长，我们通常只需键入容器ID的前4个字符即可。当然，我们还可以使用容器名，但显然用4字符的容器ID更为简便。


1. 创建：
  
Docker容器可以使用命令创建：
     
     docker run imagename 
2. 列出，删除容器：

   － 列出系统中的正在运行的容器：
   			
     		docker ps
   － 列出系统中所有状态的容器：
        	
        	docker ps －a
   － 列出最近一次启动的容器
        	
        	docker ps －l
   － 删除一个容器
   			
   			docker rm container_name/ID
   － 删除所有容器
    		
    		docker rm ‘docker ps －a －q’
3. 启动容器（run）
	
		docker run －it 容器id
		eg: docker run -it gitlab/gitlab-ce
	－ 以交互方式进入容器：
	     	
	     	docker run -i -t image_name /bin/bash
	     	
	－ 在容器中安装新应用
	        
	        docker run image_name apt-ge install  -y app_name
	        
	  备注：在执行apt-get 命令的时候，要带上-y参数。如果不指定-y参数的话，apt-get命令会进入交互模式，需要用户输入命令来进行确认，但在docker环境中是无法响应这种交互的。apt-get 命令执行完毕之后，容器就会停止，但对容器的改动不会丢失。
	     	 
4. 运行已有的容器
	
		docker start 容器id
	
5. 启动，停止，kill一个容器
    
    － 启动 
      		
      		docker start  container_name/ID
    － 停止
    		
    		docker stop container_name/ID
    － 杀死
       		
       		docker kill container_name/ID
    － 重启一个正在运行的容器
            
            docker restart container_name.ID
    	
6. 保存对容器的修改：
		
		docker commit ID new_image_name
	Note：  image相当于类，container相当于实例，不过可以动态给实例安装新软件，然后把这个container用commit命令固化成一个image。
	
7. 从一个容器中取日志
		
		docker logs Name/ID  
8. 附加到一个运行的容器上面
        
        docker attach ID 
9. 从容器里面拷贝文件/目录到本地一个路径
		docker cp ID:/container_path to_local_path
10. 附加到一个运行的容器上面:
		
		docker attach ID
		attach命令允许你查看或者影响一个运行的容器。你可以在同一时间attach同一个容器。你也可以从一个容器中脱离出来，是从CTRL-C。
11. 根据docker file构建出一个container

		docker build -t image_name dockerfile_path


# docker设置
Docker可以作为创建者读取Dockerfile文件中的指令，自动执行步骤并且创建一个新的镜像。执行docker build命令，它会按照文档执行并最终创建一个镜像。

参考文章：http://blog.chinaunix.net/uid-10915175-id-4442826.html

1. 使用
2. 格式
3. 指令

	- 3.1  FROM
	- 3.2  MAINTAINER
	- 3.3  RUN
	- 3.4  CMD
	- 3.5  EXPOSE
	- 3.6  ENV
	- 3.7  ADD
	- 3.8  ENTRYPOINT
	- 3.9  VOLUME
	- 3.10  USER
	- 3.11  WORKDIR
4. Dockerfile举例


1.使用 

－ 从镜像资源中创建一个镜像，在你的跟目录下创建一个描述文件叫做Dockerfile，这个将描述你创建镜像的步骤.

docker build要用路径的资源库来作为参数(如：.)

	sudo docker build . 

先从存储源查找要本地创建的环境，build会在docker后台运行的，而不是用命令行界面，所以所有的本地环境都会被后台进程多调度。当环境被发送到后台进程时，Docker命令行会报告"Uploading context"

－ 也可以指定存储卡和标记，来保存构建成功的镜像:

	sudo docker build -t shykes/myapp . 
Docker进程会按照步骤步骤一步操作，必要时会输出必要的结果, 创建完成之后会输出你的镜像id,Docker会自动清楚你发送的环境。

当你构建成功之后，你就要考虑把镜像推送到库中。
2. Format

Dockerfile格式很简单的:

	# Comment
	指令 参数 
指令是不区分大小写的, 然而约定是大写的以便区分其他的参数

Docker会读测试Dockerfile中的指令，第一条命令必须是'FROM',来指定你正在构建的基本镜像

docker以#开头为一个注释，一个#在的地方会被认为是一个注释，例如

	# Comment
	RUN echo 'we are running some # of cool things' 
	
3.指令
	可以使用Dockerfile中的指令来构建镜像

3.1 FROM
	
	FROM  
或者
	
	FROM : 
FROM指令来构建基础镜像。因此，一个有效的Dockerfile必须是用FROM做第一个指令。镜像可以是任何有效的镜像，它会很容易从公共存储卡中获取。

FROM在Dockerfile必须是第一个没有意见性（RUN之类的）指令

FROM命令可以在Dockerfile中出现多次创建多个镜像，在用新的FROM之前简单的记录下镜像的id

如果FROM指令没有tag，就假设tag是latest.如果tag不存在，就会发挥一个错误信息。

3.2 MAINTAINER
	
	MAINTAINER  
这个指令是允许你设置镜像生成的作者信息

3.3 RUN
	
	RUN  
RUN指令将会在当前镜像执行任何命令并提交结果，提交的镜像的结果将用户Dockerfile的下一步操作

分层RUN指令和生成提交是docker的核心概念，提交是廉价的从任何点创建一个镜像历史，就行代码控制一样。

已知问题

- 问题783 关于文件权限的问题，可能会发生在使用AUFS文件系统。你要注意她视图使用rm文件，例如，描述一个解决方案

- 问题2424 本地将不会自动被设置

3.4 CMD
CMD有三种形式：

	CMD "executable","param1","param2"

	CMD ["param1","param2"] (作为ENTRYPOINT默认参数)

	CMD command param1 param2 (像shell一样)

Dockerfile只能有一个CMD，如果你写了多个CMD，最后那个CMD会生效。

CMD主要给一个容器执行提供默认参数，这些默认值可以是一个热可执行的，或者他们可以省略可执行文件，在这种情况下，你必须指定一个ENTRYPOINT你交号

当shell中使用执行格式，CMD命令会设置镜像运行的指令，这个功能相当于docker 提交 -run 将会执行在/bin/sh -c

	FROM ubuntu
	CMD echo "This is a test." | wc - 
如果你希望你的容器每次都执行相同的可执行文件，那么你应该考虑使用ENTRYPOINT结合CMD，可以查看3.8 ENTRYPOINT.

注意

- 不要混淆运行CMD。RUN CMD，RUN必须提交结果，CMD在构建镜像是并不执行，但在镜像构建成功后会执行

3.5 EXPOSE
	
	EXPOSE  [...] 
EXPOSE指令会对连接着开放端口使用，这个功能相当于运行docker提交 -run '{"PortSpecs": ["", ""]}',相当于	
	
	docker run -p

3.6 ENV
	
	ENV   
ENV指令设置环境变量key对应值value,这个值将会被传递给后边使用的指令，这个功能相当于在命令前面加了=

注意：

		环境变量会持续到一个镜像的生成
3.7 ADD
	
	ADD   
ADD指令是将复制新文件，并将它们添加到容器的文件系统。

必须是一个文件或者目录相对于源目录（也就是构建的环境）或者一个远程文件的URL。

是容器将被复制的目录地址。

所有新创建的文件和目录都是0755权限，uid和gid 0。

注意

－ 如果你有stdin标准输入流创建(docker build - < somefile),没有建立环境，所以Dockerfile只能包含一个基于URL添加语句。

注意

－ 如果你的URL文件需要身份认证，你将需要使用运行wget，运行curl或者其他工具添加到容器是不支持身份验证的

副本必须遵循一下规则：

－ 路径必须是声称到环境中，你不能添加../something/someting,因为docker build第一步会发送环境目录（和子目录）到dicker后台进程

－ 如果是URl，并将不已斜线结尾，然后将从URl中下载并复制到

－ 如果是URL，并且以斜线结尾，则文件名是从URL推断然后文件会下载到/,例如，ADD http://example.com/foobar/将会创建file/foobar，这个URL必须是一个平常的路径，使用合适的文件名，一下情况下是无法工作的(http://example.com)

－ 如果是目录，将整个目录复制，包含文件的原始数据

－ 如果是压缩文件个事(譬如,gzip、bzip2或者xz)，那么它会解压到目录，从URL资源不解压

－ 如果一个目录被复制或者解压，他们都会执行相同的行为tar -x 作为结果的集合

－ 无论目标路径是否存在
－ 源的tree内容是否存在
产生冲突的时候会按照2来解决

如果是其它文件类型，她被单独复制连同它的数据。这种情况下，如果以斜线结尾，它就会被认为是一个目录，并将src中的写入/base（）.

如果不已斜线结尾，它会被认为是一个常规文件，并且的文件会被写入到文件中。

如果不存在，创建连同所有缺失的目录路径

3.8 ENTRYPOINT

	ENTRYPOINT有两种形式：

	ENTRYPOINT ["executable", "param1", "param2"] (像 exec, 首选)

	ENTRYPOINT command param1 param2 (作为shell执行)

Dockerfile中只能有一个ENTRYPOINT，如果你有多个ENTRYPOINT，则Dockerfile中只能最后一个会被执行

一个ENTRYPOINT会帮你配置容器作为容器的一个可执行文件，也就是说当你指定一个ENTRYPOINT，那么整个容器中都会运行这个可执行文件

ENTRYPOINT指令将会被当作一个不会被覆盖的命令参数传给运行的docker,不像CMD，这就是允许参数传递给入口，即docker run  -d 将会通过 -d参数来作为执行入口

你可以指定参数在 ENTRYPOINT JSON数组（如exec执行多个），或者通过使用一个CMD命令语句，这个入口的参数不会被docker run所重写，但是通过指定CMD的参数来重写docker run 参数

像CMD，你可以指定一个ENTRYPOINT的字符串，它将会在/bin/sh -c中执行

	FROM ubuntu
	ENTRYPOINT wc -l - 
例如，Dockerfile的镜像经常会将stdin作为输入("-")或者但列出行数("-l"),如果你像让这个可选，默认情况下你可以使用CMD

	FROM ubuntu
	CMD ["-l", "-"]
	ENTRYPOINT ["/usr/bin/wc"] 
3.9 VOLUME
	VOLUME ["/data"] 
	VOLUME指令会创建一个挂载点根据指定的名字和标记挂在外部的主机或者其他容器，更多实例可以查看docker安装说明，共享文档和目录

3.10 USER
	USER daemon 
USER质量设置镜像运行时的用户名或者Uid

3.11 WORKDIR
	WORKDIR /path/to/workdir 
WORKDIR命令执行工作目录的来执行CMD

4. Dockerfile 例子
	
		# Nginx
		#
		# VERSION               0.0.1
		
		FROM      ubuntu
		MAINTAINER Guillaume J. Charmes 
		
		# make sure the package repository is up to date
		RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
		RUN apt-get update
		
		RUN apt-get install -y inotify-tools nginx apache2 openssh-server 
---
		# Firefox over VNC
		#
		# VERSION               0.3
		
		FROM ubuntu	
		# make sure the package repository is up to date
		RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
		RUN apt-get update
		
		# Install vnc, xvfb in order to create a 'fake' display and firefox
		RUN apt-get install -y x11vnc xvfb firefox
		RUN mkdir /.vnc
		# Setup a password
		RUN x11vnc -storepasswd 1234 ~/.vnc/passwd
		# Autostart firefox (might not be the best way, but it does the trick)
		RUN bash -c 'echo "firefox" >> /.bashrc'
		
		EXPOSE 5900
		CMD    ["x11vnc", "-forever", "-usepw", "-create"] 
---
		# Multiple images example
		#
		# VERSION               0.1
		
		FROM ubuntu
		RUN echo foo > bar
		# Will output something like ===> 907ad6c2736f
		
		FROM ubuntu
		RUN echo moo > oink
		# Will output something like ===> 695d7793cbe4
		
		# You'll now have two images, 907ad6c2736f with /bar, and 695d7793cbe4 with
		# /oink.
		
		## FAQ
		1.镜像中的数据不丢失：



 ### 制作容器镜像 - 
 
 
 