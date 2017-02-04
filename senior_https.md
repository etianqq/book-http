# HTTPS

HTTPS其实是有两部分组成：**HTTP + SSL / TLS**，也就是在HTTP上又加了一层处理加密信息的模块。
服务端和客户端的信息传输都会通过TLS进行加密，所以传输的数据都是加密后的数据。

![](/assets/ssl.png)

####加密技术

* **公开密钥加密(public-key cryptography)**->加密算法是公开的,而密钥是保密的.加密和解密都会用到密钥（使用一对非对称的密钥，一把私钥一把公钥）。

* **共享密钥加密(common key crypto system)**->也被叫做对称密钥加密。以共享密钥方式加密时必须将密钥也发给对方。

**https采用共享密钥加密和公开密钥加密两者并用的混合加密机制**

![](/assets/https-crpt.png)

####数字证书

证书的一个作用是用来证明作为通信乙方的服务器是否规范,另外一个作用就是确认对方服务器背后运营的企业是否真实存在.拥有该特性的证书就是EV SSL证书(extended validation SSL certificate)

![](/assets/certificate.png)
