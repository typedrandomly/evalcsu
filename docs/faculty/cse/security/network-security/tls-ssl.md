# TSL / SSL

Created: November 18, 2021
Sort: Security

> 传输层安全性协议（Transport Layer Security，TLS）及其前身安全套接层（Secure Sockets Layer，SSL）是一种安全协议。
—— From Wiki
> 

## TSL / SSL 的作用

TSL 是用于在 Web 服务器和浏览器之间建立加密链接的标准安全技术，此安全链接可确保传输的所有数据保持私密：

1. 所有信息都是**加密传播**，第三方无法窃听。
2. 具有**校验机制**，一旦被篡改，通信双方会立刻发现。
3. 配备**身份证书**，防止身份被冒充。

## TLS 握手过程

通过握手，客户端和服务器协商各种参数用于创建安全连接：

- 服务端收到请求，即握手开始：
    - 当客户端连接到支持 TLS 协议的服务器要求创建安全连接并列出了受支持的密码包（包括加密算法、散列算法等）。
- 服务端响应请求：
    - 服务器从该列表中决定密码包，并通知客户端。
    - 服务器发回其数字证书，此证书通常包含服务器的名称、受信任的证书颁发机构（CA）和服务器的公钥。
- 客户端再次回应：
    - 首先，确认其颁发的证书的有效性；
    - 其次，为了生成会话密钥用于安全连接，客户端使用服务器的公钥加密随机生成的密钥，并将其发送到服务器，只有服务器才能使用自己的私钥解密。
- 服务器最后响应：
    - 前面三步利用随机数，双方生成用于加密和解密的对称密钥。

这就是TLS协议的握手，握手完毕后的连接是安全的，直到连接（被）关闭，如果上述任何一个步骤失败，TLS握手过程就会失败，并且断开所有的连接。

## TSL 的强健性

在交换协议过程中，往往面临着如下问题：

- 不同公钥/私钥加密密钥的长度；
- 不同的公钥证书；

TSL 的基本原理是公钥加密，在握手阶段中都会生成一个随机数，在确认证书签名无误的情况下，双方利用证书私钥对随机数进行签名，协商生成"对话密钥"，然后传递自己的公钥，交给对方进行校验，从而保证了 TSL 的强健性。

## Reference

阮一峰：[https://www.ruanyifeng.com/blog/2014/02/ssl_tls.html](https://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

Wiki：[https://zh.wikipedia.org/wiki/傳輸層安全性協定](https://zh.wikipedia.org/wiki/%E5%82%B3%E8%BC%B8%E5%B1%A4%E5%AE%89%E5%85%A8%E6%80%A7%E5%8D%94%E5%AE%9A)