# HTTP首部
HTTP首部字段根据实际用途分为4种类型：

1. 通用首部字段：request和response都会使用的首部
2. 请求首部字段：request使用的
3. 响应首部字段：response使用的
4. 实体首部字段：针对request和response报文的实体部门使用的首部

下面的首部字段是在工作中用的过的：

####请求首部字段
#####1. Authorization 
告知服务器，用户代理的认证信息（证书值）。

应用场景：需要传token信息，或者类似的认证信息（比如App H5页面使用的ak）
![](http-header-authorization.png)

#####2.If-Match(请求首部字段)
和ETag搭配使用，处理资源缓存。

只有If-Match和ETag值匹配**一致**时，服务器才会接受请求。

#####3.If-None-Match
只有在If-None-Match和ETag值匹配**不一致**时，服务器才会接受请求。与If-Match首部字段作用相反。

#####4.If-Modified-Since
该字段指定日期时间后，资源发生了更新，服务器会接受请求。

#####4.If-Unmodified-Since
和If-Modified-Since作用相反。

该字段指定日期时间后，资源发生了更新，服务器会接受请求。



