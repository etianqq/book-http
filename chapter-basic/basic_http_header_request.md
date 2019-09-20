# 请求首部字段

####1. Authorization 
告知服务器，用户代理的认证信息（证书值）。

应用场景：需要传token信息，或者类似的认证信息（比如App H5页面使用的ak）
![](/assets/http-header-authorization.png)

####2.Referer
告知服务器请求的原始资源的URI。

    后端做重定向时可能需要这个信息。注意，它不会带上hash。
    
![](/assets/http-header-referer.png)

####3.User-Agent
会创建请求的浏览器和用户代理名称等信息传达给服务器。
