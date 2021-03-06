# I/O层设计

``akka.io`` 包已由Akka和[``spray.io``](spray.io) 团队协作开发。其设计采用``spray-io`` 模块的开发经验，并加以改进为更一般基于actor的服务使用。

### 要求
为了形成通用的可扩展的IO层基础，使之适合于广泛的应用，在Akka remoting 和spray HTTP 是原有基础上，为设计的关键驱动因素建立了以下要求：

* 数以百万计的并发连接的可扩展性

* 从数据输入通道到进入目标actor邮箱要有最低可能的延迟

* 最大的吞吐量

* 在两个方向的可选back-pressure （即在议定允许的地方对本地发送者限流，同时允许本地读者对远程发送者限流）

* 一个纯粹基于actor的 API 和不可变的数据表示形式

* 通过很瘦的SPI集成新运输方式的可扩展性;目标是不会强迫迫I/O 机制到最低共同标准，而是相反，完全允许特定协议的用户级API。

### 基本体系结构
每个传输实现，可作为一个单独的Akka扩展，提供一个`ActorRef`代表联系客户端代码的初始点。这个"管理器"可接受请求建立一个通信通道 （例如连接或侦听一个TCP套接字）。每个通信通道都由一个特定actor代表，暴露给客户端代码，在其整个生命周期服务于与此通道的所有交互。

实现的核心要素是传输特定"selector"的actor ；例如TCP中它将包装一个`java.nio.channels.Selector`。通道actor通过发送相应消息到其指定的选择器actor，来注册其感兴趣的渠道的读或写。然而，实际的通道读写是由通道actor自己完成的，这样将选择器actor从耗时的任务中解放出来，从而保证了低延迟。选择器actor唯一的责任是管理的底层的选择器的键集合和实际选择操作，这是唯一会阻塞的操作。

通道到选择器的指定由管理actor操作。并且在通道的整个生存期内都保持不变。从而管理actor基于一些特定于实现的分配逻辑在一个或多个选择器actor中 "编制（stripes)" 新渠道。这种逻辑可能 （部分地） 委派给选择器actor，例如，当他们认为自己有能力处理的时候可以选择拒绝被指定一个新渠道。

管理actor创建 （并因此监督） 选择器actor，它们相应地创建并监督其频道actor。某一单一传输实现的actor层次结构因此包含三个截然不同的actor层次，管理actor在顶部，通道actor在叶子节点，选择器actor在中间。

背压(Back-pressure)输出通过允许用户能够在其`Write`消息中指定它是否想收到会写入操作系统内核的排队确认消息来实现。背压输入通过向通道actor发送消息，暂时禁用通道的阅读兴趣，直到通过相应的恢复命令重新启用读操作来实现。在流量控制的运输情况下 ——例如 TCP —— 在接收端不消费数据的行为 （从而使数据保持在内核读取缓冲区中） 会传播回给发送者，跨网络链接这两个机制。

### 设计的好处
整个实现保持在actor模型内，允许我们删除显式线程处理逻辑的需要，同时也意味着有没有涉及锁 （除了那些底层传输工具库的部分）。只编写actor代码会使实现更加简洁，同时Akka高效的actor消息传递没有对这一好处带来很大的开销。事实上 I/O 基于事件的性质能很好地映射到actor模型，在此模型中我们期望明确的性能和可伸缩性优势，而不是传统的解决方案的显式线程管理和同步。

监督层次结构的另一个好处是，清理资源是自然而然的： 关闭一个选择器的actor会自动清理所有通道actor，允许通道的恰当关闭，并将适当的消息发送到用户级客户端actor。DeathWatch允许通道actor注意到其用户级别的处理器actor的消亡，并在这种情况下也以一种有序的方式终止 ；这自然就减少了泄露未关闭通道的可能性。

使用 `ActorRef` 暴露所有功能的选择，确保了这些引用可以被自由的分发和代理，并在用户认为合适的时候处理一般情况，包括使用远程处理和生命周期监测（只是随便列出两个）。

### 怎样去添加一个新的传输
最好的开始是研究 TCP 引用的实现，从中可以良好的获取其基本工作原理，然后设计和实施，对新的协议是类似的，但也会有问题。有 I/O 机制之间差异巨大 （例如比较文件 I/O 和消息代理） ，此 I/O 层的目标是明确**不能**把他们都硬塞进一个统一的 API，这就是为什么只有基本体系结构的思想记录在这里。


