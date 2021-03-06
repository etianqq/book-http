#ETag, If-None-Match


![](/assets/cache2.png)

1. 浏览器第一次跟服务器请求一个资源，服务器在返回这个资源的同时，在respone header加上ETag。
```
ETag是服务器根据当前请求的资源生成的一个唯一标识。
这个唯一标识是一个字符串，只要资源有变化这个串就不同，跟最后修改时间没有关系。
```

2. 浏览器再次跟服务器请求这个资源时，在request header上加上If-None-Match（值就是上一次请求时返回的ETag的值）。
3. 服务器再次收到资源请求时，根据浏览器传过来If-None-Match和然后再根据资源生成一个新的ETag，如果这两个值相同就说明资源没有变化，否则就是有变化；
如果没有变化则返回304 Not Modified，但是不会返回资源内容；
如果有变化，就正常返回资源内容。
与Last-Modified不一样的是，当服务器返回304 Not Modified的响应时，由于ETag重新生成过，response header中还会把这个ETag返回，即使这个ETag跟之前的没有变化。

![](/assets/cache3.png)

如上例中所示，在使用了If-None-Match之后，服务器只需要很小的响应就可以达到相同的结果，从而优化了性能。

```
协商缓存需要配合强缓存使用.
如上图，有强缓存的相关Cache-Control，因为如果不启用强缓存的话，协商缓存根本没有意义。
```



