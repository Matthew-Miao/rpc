# RPC

功能:

代理层

注册中心

路由层

故障转移

协议层

拦截器层

SPI

## 前言

本视频内容以 原理为主，代码为辅，自主思考较多。

讲解顺序：架构-设计-代码

## 基本概念

RPC全程是远程过程调用协议，是一个协议，具体落地实现由自己决定。

RPC由来:

在微服务下，A服务想要调用B服务，这就是远程调用

RPC和HTTP的区别？

## RPC演变以及架构



## 代理层

**代理设计模式**

代理层用于封装多余的操作，例如：制定协议，编码，从注册中心要服务，负载均衡，调用，容错机制。所有的流程都在代理层中封装好了。调用方只需要进行调用方法即可。

>   在mybatis中的mapper层也是如此

## 注册中心

>   这一小节讲解：服务注册/发现过程，配置文件，以redis为角度讲解注册中心

用于提供服务注册以及服务发现功能。

提供方将服务提供给注册中心

调用方进行服务发现时给具体的接口创建代理对象，封装逻辑。服务发现(依赖注入)

## 路由层

**负载均衡算法**

**根据算法选择合适的服务。**

**静态负载均衡算法**
轮询（Round Robin）：服务器按照顺序循环接受请求。
随机（Random）：随机选择一台服务器接受请求。
权重（Weight）：给每个服务器分配一个权重值，根据权重来分发请求到不同的机器中。
IP哈希（IP Hash）：根据客户端IP计算Hash值取模访问对应服务器。
URL哈希（URL Hash）：根据请求的URL地址计算Hash值取模访问对应服务器。
一致性哈希（Consistent Hash ）：采用一致性Hash算法，相同IP或URL请求总是发送到同一服务器。
**动态负载均衡算法**
最少连接数（Least Connection）：将请求分配给最少连接处理的服务器。
最快响应（Fastest Response）：将请求分配给响应时间最快的服务器。
观察（Observed）：以连接数和响应时间的平衡为依据请求服务器。
预测（Predictive）：收集分析当前服务器性能指标，预测下个时间段内性能最佳服务器。
动态性能分配（Dynamic Ratio-APM）：收集服务器各项性能参数，动态调整流量分配。
服务质量（QoS）：根据服务质量选择服务器。
服务类型（ToS）: 根据服务类型选择服务器

## 协议层

服务与服务之间进行通信需要制定好双方协议，是为了安全校验，状态显示，粘包半包等。

为了跨平台存储以及网络传输因此需要序列化。

在传输时也会出现粘包半包问题，也需要解决。

**半包：**

因窗口大小原因只发送了一半的数据，因此需要等待发送方继续发送再进行先接受

**粘包：**

假设发送放发了2条数据，并且这2条数据在一个窗口下，因此会出现粘包的问题

>   因序列化方式都是以工具类的形式存在，并且只需要对比每种序列化的性能即可选择，因此这一小节主要讲数据格式，粘包半包，编码解码，代码层面

## 拦截器层

在服务发送前后以及服务接收前后可进行一系列的拦截操作，或者是增强行为等。这是一个拓展机制。

## SPI

使用SPI后对于整个程序的拓展性有了极大的提升。

**概念：**

制定好接口规范协议后，其他服务按照你制定好的服务协议。随后使用SPI进行可插拔方式来加载不同的类。

例如：jdbcl驱动，我先制定好一个协议，我不管你是什么sql厂商，你都遵循我的协议来，然后我使用spi机制来进行加载类就行。

## 容错层

在服务提供方发生错误时(无法提供服务)，此时有可能还会有其他服务能提供，因此还需要尝试找其他服务。

##线程池-高并发

## 整体代码

## 项目演示
