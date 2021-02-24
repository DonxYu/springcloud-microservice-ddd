微服务+DDD代码结构例子
======================

#### 前言

这是一个基本的微服务 + DDD演示例子(待完善)，基于 Spring Boot 2.2.4.RELEASE

结构例子(待完善),目前(2021-02-24)暂时写了Infrastructure层和Interfaces层的样例内容。

微服务 + DDD，个人觉得应该是首先是从微服务的角度(如何划分微服务)考虑去划分大的业务模块，每一个微服务都应该是一个可以单独部署，各司其职的模块；

微服务实际开发中，也结合DDD的思想去划分所有属于自己的领域。
    
微服务的划分与落地，其实也应该是以DDD的思想做去指导的，所以无论我们代码结构如何规划，也并非一成不变，应该从实际出发，去思考划分结构的意义。代码的分层是为了让我们的代码对业务的表达更加清晰。
    
此例子是对于微服务+DDD反应到实际开发，代码的结构设计上的一种初步的思考与探索,一个样板工程，不应该成为我们对实际DDD思考与设计的限制，本例仅供参考。
    
本例博客链接 : [一个微服务+DDD(领域驱动设计)的代码结构示例](https://www.cnblogs.com/ealenxie/p/9559781.html)
    
#### DDD的结构图

![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830125911190-468037055.png)<p>
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830125945668-1072959527.png)

#### 项目结构图
本项目是一个假设已经划分好了业务微服务，设计遵循DDD的架构与角色，代码设计上就分为Infrastructure，Domain，Application，Interfaces，项目结构图如下:

![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830132619533-611437668.png)

#### 结构说明

**Infrastructure层**
    
基础实施层，向其他层提供通用的技术能力(比如工具类,第三方库类支持,常用基本配置,数据访问底层实现)，结构如图:
            
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134304547-660094458.png)<p>
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134336916-1945132941.png)
        
**Domain层**
    
主要负责表达业务概念,业务状态信息和业务规则；是整个系统的核心层,几乎全部的业务逻辑会在该层实现，结构如图:
        
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134410240-623245752.png)<p>
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134515558-56966635.png)
        
**Application层**
        
相对于领域层,应用层是很薄的一层,应用层定义了软件要完成的任务,要尽量简单。
        
注: 下图package-info里面所说的对内对外，对程序而言，事实上是从展现层调用应用层，应用层调用领域层，领域层或调用基础实施层。结构如图:
    
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134844172-1295041747.png)<p>
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830134819652-762502148.png)

**Interfaces层**
    
负责向用户显示信息和解释用户命令，请求应用层以获取用户所需要展现的数据(比如获取首页的商品数据)。结构如图:

![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830135806554-1845171786.png)<p>
![avatar](https://images2018.cnblogs.com/blog/994599/201808/994599-20180830135840092-1534652017.png)

#### 谈谈我个人对微服务的理解

微服务架构设计，一个微服务应该就是一个可单独部署，可运行的应用，也就是微服务最小的运行单元。

微服务本身内部高度内聚，微服务与微服务之间低耦合。 首先对于应用划分上，就应该想清楚每个微服务的职责，每个微服务服务内部建立起自己的依赖，完成自己的职责和业务。

微服务与微服务之间交互通过HTTP或RPC接口调用，降低微服务之间代码实现和业务的耦合。

微服务的实现不应该受限某程序语言(或Java，或Go，或Python)，不应该受限于某框架(或SpringCloud，或Dubbo，或各种RPC框架等等)。

我的代码结构是对于一个微服务本身(即应用)划分的，领域是对于微服务内部本身而言的，即这个微服务涉及哪些领域。

首先从大的方向去划分每一个微服务，然后再从每一个微服务确定所包含的领域，领域的边界，等等。

比如划分了一个 认证授权服务，那么 领域可能有 用户，权限；实体可能有角色，资源等等。领域行为可能有认证，授权，用户登录退出等等。

为什么要研究DDD？无论是DDD也好，还是以前的MVC架构，笔者认为两者真正反应到代码层次的结构划分其实并不重要，研究DDD的目的不是为了跟风，为了让微服务划分更加合理，让代码对业务的表达更加清晰，以应对项目发展壮大后难拆解，难扩展的问题。

DDD的难题在如何划分领域，如何界定领域的边界，如何找出领域的聚合根,如何设计聚合等等问题；笔者见识浅薄，羞愧问一句:"目前真的有项目的微服务是以领域驱动设计为理念基础做指导,让代码真正做到落地？"。

微服务的难题在乎如何划分微服务，如何治理微服务等等问题。
    
个人才疏学浅，如有雷同或是不当之处，望各位见谅和帮忙指正。
    
感谢各位提出意见和支持。


#### 关于本样例中的部分内容

一个微服务有哪些必要组件,实现哪些功能,取决于业务

本例中只是笔者总结自身经验写了一些基本样例内容(仅供参考)，有些内容甚至都可以算是个人研发规范，这里写是为了对此微服务DDD结构例子的内容做个填充。

[关于样例中的Infrastructure](https://github.com/EalenXie/spring-microservice-ddd/blob/master/doc/infrastructure.md)

[关于样例中的装配(Assembler)](https://github.com/EalenXie/spring-microservice-ddd/blob/master/doc/assembler.md)

#### 本文参考内容

[可以落地的DDD到底长什么样？](https://www.cnblogs.com/hafiz/p/9388334.html)

[DDD领域驱动设计基本理论知识总结](https://www.cnblogs.com/netfocus/archive/2011/10/10/2204949.html)
    
[领域驱动设计(Domain Driven Design)参考架构详解](https://blog.csdn.net/bluishglc/article/details/6681253)
