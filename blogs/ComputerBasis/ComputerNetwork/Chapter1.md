# Chapter 1

## 计网基本概念

- 节点
  - 主机节点：手机、电脑等
  - 交换节点：路由器、交换机
- 链路
  - 接入网络链路：主机节点与交换节点间的链路
  - 主干(骨干)链路：交换节点与交换节点间的链路

- 协议
  - 定义：对等层的实体，在通信中应该遵守的规则
  - 协议规范了：报文格式、次序、动作

- 网络边缘
  - 边缘(edge)通过接入网络链路(access)接入核心(core)，从而使得任意端系统之间可以互相通信
  - 核心(core)的作用：数据交换

![image](https://gitee.com/percivalyang/images/raw/master/images/image.png)

- 客户端服务器模式：主从模式，主->服务器，从->客户端。该模式的缺点：可扩展性和可靠性差。

- 对等(P2P(Peer to Peer))

![image (1)](https://gitee.com/percivalyang/images/raw/master/images/image%20(1).png)