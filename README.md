akka文档中文翻译
===========

该文档是[Akka官方文档](http://akka.io/docs)的中文翻译。使用[Gitbook](https://www.gitbook.io/)制作。

本文大量参考了[上海广谈信息技术有限公司](http://www.gtan.com/)的[《Akka 2.0文档》](http://www.gtan.com/welfare04.html)。
[广谈公益](http://www.gtan.com/welfare.html)还有很多优秀的资源，如感兴趣请移步参考。

###贡献力量

欢迎大家对该文档贡献力量，提出[宝贵意见](../../issues)，修改并提交[Pull Requests](../../pulls)。

如果对scala和akka感兴趣，欢迎加入“无水scala群”：231809997，有各路scala高手帮你释疑。

对贡献的要求是保持术语和代码的一致

* **术语的一致**：以[《Akka 2.0文档》](http://www.gtan.com/welfare04.html)的术语为准，如果有更好的选择，欢迎[提出issue](../../issues)
* **代码的一致**：书的内容放在`版本号/语言/`目录下，如`2.3.6/scala/`，生成的html文件放在`版本号/语言/book/`目录下。如非必要，不要提交其他无关内容或生成的内容。

###翻译进度与状态

#####2.3.6 scala

* [x] Introduction
* [x] 引言
   * [x] Akka是什么?
   * [x] 为什么使用Akka?
   * [x] 入门
   * [x] 必修的“Hello World”
   * [x] 用例和部署场景
   * [x] Akka使用实例
* [x] 概述
   * [x] 术语，概念
   * [x] Actor系统
   * [x] 什么是Actor?
   * [x] 监管与监控
   * [x] Actor引用, 路径与地址
   * [x] 位置透明性
   * [x] Akka与Java内存模型
   * [x] 消息发送语义
   * [x] 配置
* [x] Actors
   * [x] Actors
   * [x] 类型Actor
   * [x] 容错
   * [x] 调度器
   * [x] 邮箱
   * [x] 路由
   * [x] 有限状态机(FSM)
   * [x] 持久化
   * [x] 测试Actor系统
   * [x] Actor DSL
* [ ] Futures与Agents
   * [ ] Futures (翻译完成，待校验)
   * [ ] Agents (翻译完成，待校验)
* [ ] 网络
   * [ ] 集群规格
   * [ ] 集群用法
   * [ ] 远程 (翻译完成，待校验)
   * [ ] 序列化 (翻译完成，待校验)
   * [ ] I/O (翻译完成，待校验)
   * [ ] 使用TCP (翻译完成，待校验)
   * [ ] 使用UDP (翻译完成，待校验)
   * [ ] ZeroMQ (翻译完成，待校验)
   * [ ] Camel
* [ ] 实用工具
   * [ ] 事件总线 (翻译完成，待校验)
   * [ ] 日志 (翻译完成，待校验)
   * [ ] 调度器 (翻译完成，待校验)
   * [ ] Duration (翻译完成，待校验)
   * [ ] 线路断路器 (翻译完成，待校验)
   * [ ] Akka扩展 (翻译完成，待校验)
   * [ ] 微内核 (翻译完成，待校验)
* [ ] 如何使用：常用模式 (翻译完成，待校验)
   * [ ] 消息限流
   * [ ] 跨节点平衡工作负载
   * [ ] 工作拉取模式，来限流和分发工作，防止邮箱溢出
   * [ ] 顺序终止
   * [ ] Akka AMQP代理
   * [ ] Akka 2中的关闭模式
   * [ ] 使用Akka做分布式（内存）图像处理
   * [ ] 案例分析：一个使用Actor的自动更新缓存
   * [ ] 使用蜘蛛模式发现actor系统的消息流向
   * [ ] 周期信息调度
   * [ ] 模板模式
* [ ] 实验模块
   * [x] 持久化
   * [ ] 多节点测试 (翻译完成，待校验)
   * [ ] Actors(使用Java的Lambda支持) not supported
   * [ ] FSM(使用Java的Lambda支持) not supported
   * [ ] 外部贡献 (翻译完成，待校验)
* [ ] Akka开发者信息
   * [ ] 构建Akka (翻译完成，待校验)
   * [ ] 多JVM测试 (翻译完成，待校验)
   * [ ] I/O层设计 (翻译完成，待校验)
   * [ ] 开发指南 (翻译完成，待校验)
   * [ ] 文档指南 not supported
   * [ ] 团队 not supported
* [ ] 工程信息
   * [ ] 迁移指南 not supported
   * [ ] 问题追踪 not supported
   * [ ] 许可证 not supported
   * [ ] 赞助商 not supported
   * [ ] 项目 not supported
* [ ] 附加信息
   * [ ] 常见问题 (翻译完成，待校验)
   * [ ] 图书 not supported
   * [ ] 其他语言绑定 not supported
   * [ ] Akka与OSGi not supported
   * [ ] 部分HTTP框架名单 not supported

xring开始更新自己的翻译
