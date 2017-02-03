#Last-Modified,If-Modified-Since

1. 浏览器第一次跟服务器请求一个资源，服务器在返回这个资源的同时，在***respone*** header加上Last-Modified属性（表示这个资源在服务器上的最后修改时间）：

![](/assets/negotiate-cache1.png)
2. 浏览器再次跟服务器请求这个资源时，在***request*** header上加上If-Modified-Since属性（该值就是上一次请求时返回的Last-Modified的值）：
![](/assets/negotiate-cache2.png)
3. 服务器再次收到资源请求时，根据浏览器传过来If-Modified-Since和资源在服务器上的最后修改时间判断资源是否有变化，如果没有变化则返回304 Not Modified，但是不会返回资源内容；如果有变化，就正常返回资源内容。
当服务器返回304 Not Modified的响应时，response header中不会再添加Last-Modified，因为既然资源没有变化，那么Last-Modified也就不会改变，这是服务器返回304时的response essay-header：
![](/assets/negotiate-cache3.png)
4. 浏览器收到304的响应后，就会从缓存中加载资源。
5. 如果协商缓存没有命中，浏览器直接从服务器加载资源时，Last-Modified Header在重新加载的时候会被更新，下次请求时，If-Modified-Since会启用上次返回的Last-Modified值。

```
一般来说，在没有调整服务器时间和篡改客户端缓存的情况下，这两个essay-header配合起来管理协商缓存是非常可靠的，
但是有时候也会服务器上资源其实有变化，但是最后修改时间却没有变化的情况，就会影响协商缓存的可靠性。
```