# http报文中与缓存相关的首部字段

![](/assets/http-cache-detail.png)

#####1.If-Match(请求首部字段)
和ETag搭配使用，处理资源缓存。

只有If-Match和ETag值匹配**一致**时，服务器才会接受请求。

#####2.If-None-Match
只有在If-None-Match和ETag值匹配**不一致**时，服务器才会接受请求。与If-Match首部字段作用相反。

#####3.If-Modified-Since
该字段指定日期时间后，**资源发生了更新**，服务器会接受请求。

#####4.If-Unmodified-Since
和If-Modified-Since作用相反。

该字段指定日期时间后，资源**未发生了更新**，服务器才处理请求。


参看文章：[浅谈浏览器http的缓存机制](http://www.cnblogs.com/vajoy/p/5341664.html)


