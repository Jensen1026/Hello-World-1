# Kubernetes 学习

[TOC]

## 参考资料

* 《Kubernetes 权威指南（纪念版）》

## Kubernetes 入门

### Kubernetes 是什么？

* 在 Kubernetes 中，Service 是分布式集群架构的核心，一个 Service 对象拥有如下关键特征：
  * 拥有一个唯一指定的名字；
  * 拥有一个虚拟 IP（Cluster IP、Service IP 或 VIP）和端口号；
  * 能够提供某种远程服务能力；
  * 被映射到了提供这种服务能力的一组容器应用上。

#### Kubernetes 组件

##### Pod

* 每个 Pod 里运行着一个特殊的被称为 Pause 的容器，其他容器则为业务容器，这些业务容器共享 Pause 容器                                                               的网络栈和 Volume 挂载卷，因此他们之间的通信和数据交换更为高效。pause 容器也被称为“根容器”。

#### 问题与解决方案

* 如何扩容和升级？

  在 Kubernetes 集群中，你只需为需要扩容的 Service 关联的 Pod 创建一个 RC（Replication Controller），则该 Service 的扩容以至于后来的 Service 升级等头疼问题都迎刃而解。在一个 RC 定义文件中包括以下3个关键信息：
  
  * 目标 Pod 的定义；
  * 目标 Pod 需要运行的副本数量（Replicas）；
  * 要监控的目标 Pod 的标签（Label）。
  
* 在通常情况下，Cluster IP 是在 Service 创建后由 Kubernetes 系统自动分配的，其他 Pod 无法预先知道某个 Service 的 Cluser IP 地址，因此需要一个服务发现机制来找到这个服务。

  ```text
  最初时，Kubernetes 巧妙地使用了 Linux 环境变量（Environment Variable）来解决这个问题。即根据 Service 的唯一名字，容器可以从环境变量中获取到 Service 对应的 Cluster IP 地址和端口，从而发起 TCP/IP 连接请求。
  ```

  