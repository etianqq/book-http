#Cache-Control:max-age

***http1.1***的时候，提出了一个新的essay-header，就是Cache-Control，这是一个相对时间，在配置缓存的时候，以秒为单位，用数值表示，如：Cache-Control:max-age=315360000，它的缓存原理是：

1. 浏览器第一次跟服务器请求一个资源，服务器在返回这个资源的同时，在respone header加上Cache-Control属性，如：

![](/assets/expires-response2.png)
2. 浏览器在接收到这个资源后，会把这个资源连同所有response header一起缓存下来；
3. 浏览器再请求这个资源时，先从缓存中寻找，找到这个资源后，根据它第一次的请求时间和Cache-Control设定的有效期，计算出一个资源过期时间，再拿这个过期时间跟当前的请求时间比较，如果请求时间在过期时间之前，就能命中缓存，否则就不行。
4. 如果缓存没有命中，浏览器直接从服务器加载资源时，Cache-Control Header在重新加载的时候会被更新。

```
优点：
Cache-Control描述的是一个相对时间，在进行缓存命中的时候，都是利用客户端时间进行判断，
所以相比较Expires，Cache-Control的缓存管理更有效，安全一些。
```

```
注意
如果同时启用Expires和Cache-Control， Cache-Control优先级高于Expires。
```
![](/assets/expires-response3.png)

