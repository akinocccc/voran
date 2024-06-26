---
title: 浅谈MITM攻击
date: 2021/10/02 17:22
hero_image: https://blog-1302037900.cos.ap-guangzhou.myqcloud.com/images/covers/computer_network.png
---

## 简述

MITM 攻击即中间人攻击，攻击者在客户端和服务端两端分别建立独立的连接，并交换它们之间传输的数据，使得通信两端认为其在一个私密的连接与对方传输数据，实际上其会话完全被攻击者掌控。

## 攻击过程

这里以课堂传纸条为例。

A 需要向 B 传递一个纸条，C 在其传递的过程中 ，那么在 A 向 B 传输信息的过程中，其信息是有可能被 C 截获、篡改的。

比如：

A(发)：今天去哪玩？

C(改)：今天去哪吃饭？

B(收)：今天去哪吃饭？

由上面的例子可以看出，C 在其中充当了中间人的身份，A 向 B 发送的信息已经被 C 截获和篡改了，因此称 AB 传输信息的过程中遭到了中间人攻击。

### HTTP 中间人攻击

由于 HTTP 通信没有身份验证，而且通信不加密传输(裸奔~，这样导致的一个安全隐患就是上面提及的中间人攻击，其传输过程容易被中间人篡改，因此现在更推崇 HTTPS

#### 如何防范

##### 非对称加密？

客户端使用私钥加密，将公钥和密钥发送给服务端，服务端使用公钥加密，将密钥发送给客户端，然后通过该密钥通信。但是这种方式仍然有安全隐患，比如中间人截获的客户端发送的密钥和公钥，然后用自己的公钥加密返回给客户端，用自己的私钥生成密钥，然后发送给服务端，此时通信双方是感知不到自己的通信密钥被截获了的。

##### 数字证书

将公钥发送给证书颁发机构申请证书，CA 通过自己的私钥加密公钥，通过域名等身份信息去生成证书签名，通信是否安全就取决于证书签名真伪的校验。
