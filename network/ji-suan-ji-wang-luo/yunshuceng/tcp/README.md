# TCP

## TCP 特点

#### TCP 提供面向连接的服务

在传送数据之前必须先建立连接，数据传送结束后要释放连接。有TCP要提供可靠的、面向连接的运输服务，因此不可避免地增加了许多开销，如确认、流量控制、计时器以及连接管理等。

#### TCP连接只能是点对点

#### TCP 提供可靠交付

#### TCP 提供全双工通信

TCP 默认通信双方的应用进程在任何时候都能发送数据。TCP 连接的两端都设有发送缓存和接收缓存。在发送时，应用程序在数据发送给TCP缓存后，就可以做自己的事

## TCP 连接

为了解决单个计算机进程的标识在不同操作系统下不一致的问题，采用了统一的**协议端口**号来进行互相通信。

两个计算机进程要互相通信，不仅必须知道对方的IP地址，还要知道对方的端口号。

### 熟知端口号

| 应用程序 | FTP | HTTP | DNS |
| :--- | :--- | :--- | :--- |
| 熟知端口号 | 21 | 80 | 53 |

### 客户端口号

数值为 49152 ~ 65535

###  套接字

TCP 连接的端点叫套接字\(socket\)

{% hint style="info" %}
套接字 socket = \( IP 地址：端口号 \)

TCP 连接 = { socket1, socket2 } = { \(IP1:port\), \(IP2:port\) }
{% endhint %}

### 为什么会有四次挥手？

> [https://hit-alibaba.github.io/interview/basic/network/TCP.html](https://hit-alibaba.github.io/interview/basic/network/TCP.html)

因为TCP是双向通信的，断开连接设计上是从全联通到半联通的设计。

A跟B发出断开连接时，仅表示A不再发送数据，但是还可以接受数据。B回复确认表示知道A要断开。在B发送完应该发的数据后，A依然可以收到。最后在B没有数据发送后，再次发送请求，A回应确认。A会在超时等待没有B额外的请求后认为服务器端已经正常关闭连接，于是自己也关闭连接。

#### 第二种解答

因为服务端在接收到`FIN`, 往往不会立即返回`FIN`, 必须等到服务端所有的报文都发送完毕了，才能发`FIN`。因此先发一个`ACK`表示已经收到客户端的`FIN`，延迟一段时间才发`FIN`。这就造成了四次挥手。

如果是三次挥手会有什么问题？

等于说服务端将`ACK`和`FIN`的发送合并为一次挥手，这个时候长时间的延迟可能会导致客户端误以为`FIN`没有到达客户端，从而让客户端不断的重发`FIN`。  

