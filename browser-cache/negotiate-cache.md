#协商缓存

####原理

```
当浏览器对某个资源的请求没有命中强缓存，就会发一个请求到服务器，验证协商缓存是否命中，
如果协商缓存命中，请求响应返回的http状态为304并且会显示一个Not Modified的字符串
```
![](/assets/negotiate-cache.jpg)

![](/assets/negotiate-cache-reponse.png)

**协商缓存是利用的是【Last-Modified，If-Modified-Since】和【ETag、If-None-Match】这两对Header来管理的**

