# 身份认证(Cookies vs Tokens)

常用身份验证有两种方式：
* cookies
* token
![](/assets/cookie-token.png)

####Cookies
* cookies是stateful
* 不需要前端存储
* 有CSRF(跨站点伪造请求)风险

认证信息在服务端和客户端都需要存储（通常情况下）。服务端通过reponse: ```Set-Cookie```头信息为客户端设置cookie。
![](/assets/response-set-cookie.png)

一般，客户端不需要做特殊配置，就可以在后续的ajax请求中带上cookie。

如果是跨域，jsonp请求默认挂cookie，CORS要特殊处理。

####Tokens


