# 云计算部分

[Here](./云计算考试内容.pdf)

1. Openstack都包含那些核心项目，作用：
	Nova（计算），swift（对象存储），glance（镜像服务），keystone（身份服务），horizon（UI界面）
	Neutron（网络和地址服务），cinder（块存储）
2. Nova有哪些核心模块，工作过程是什么：
	核心模块：
	Nova-compute（虚拟机实例创建终止迁移，接受请求，执行并更新数据库状态）
	Nova-volume（映射到实例的卷的创建附加取消）
	Nova-network（接受网络任务，控制虚拟机网络）
	Nova-scheduler（调度，决定哪台机器启动新的虚拟机实例）
	Queue（守护进程传递消息）
	SQLdatabase（存储数据）
	工作过程：
	用户输入命令，api会查看这种类型的instance是否达到最大值，给scheduler发送一个消息（实际上是发送到了Queue中）
	去运行这个实例。
	调度器接受到了消息队列Queue中API发来的消息，然后根据事先设定好的调度规则，选择好一个host，之后，这个instance会在
	这个host上创建。
	真正创建instance是由compute完成的，通过glance查看镜像。
	根据找到的镜像，到database中查找相应的数据。
	volume创建虚拟机实例的卷。
	network为虚拟机分配IP等网络资源。
3. Keystone权限控制过程是什么：
	用户传credentials给Keystone进行请求，keystone进行认证以后分配给用户一个token（令牌）
	用户获得权限，将令牌和虚拟机请求传给Nova，Nova想keystone验证令牌，获得权限后连同对镜像的请求传给
	glance，glance向keystone验证令牌，把镜像传给Nova，Nova再将用户接入网络的请求传给quantum，验证成功后，即传出成功访问的回答。
4. Swift的组件有哪些，都有什么作用：
	Proxy Server：是提供swift API的服务器进程，负责swift其余组件间的相互通信。对于每个客户端的请求，它将在Ring中查询Account、Container或Object的位置，并且相应地转发请求。
	Storage Server：提供了磁盘设备上的存储服务
	Consistency Servers：查找并解决由数据损坏和硬件故障引起的错误
	Ring：Swift最重要的组件，用于记录存储对象与物理位置间的映射关系。
5. 并行化思想：将一道指令划分为几部分，然后它们可以并发地执行。各部分的指令分别在不同的CPU上运行，这些CPU可以在单台或多台机器中，它们连接起来共同运作。
6. 前序节点可以起到限流、过滤、变换等功能。
	广播节点实际上起到了数据复制的作用，使得同一份数据进入不同的管道。
	同步节点实际上起到了数据开关的作用，控制管道开关。
7. 图的切分方式：
	边切分，点切分。（如何切，看P11）
8. BSP计算模式：
	将计算分为一系列的超步的迭代。纵向上看是一个串行的模式，一轮一轮顺序化串行。横向上看是一个并行的模式。每两个超步间设置一个栅栏作为整体同步点。确定所有并行的计算都完成后再启动下一轮超步。