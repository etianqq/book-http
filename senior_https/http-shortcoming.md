#HTTP 缺点

####1.通信使用明文(不加密),内容可能被窃听.(抓包工具可以获取请求和响应内容)

![](/assets/http-shortcoming1.png)

####2.不验证通讯方的身份,可能遭遇伪装.(任何人都能发送请求,不管对方是谁都会返回响应).

![](/assets/http-shortcoming2.png)

####3.无法证明报文的完整性,可能会遭篡改.(没有办法确认发出的请求/响应和接收到的请求/响应前后一致)

![](/assets/http-shortcoming3.png)