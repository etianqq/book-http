#强缓存


####原理

```
当浏览器对某个资源的请求命中了强缓存时，返回的http状态为200。
在chrome的开发者工具的network里面size会显示为from cache。
```
![](/assets/hard cache.png)

强缓存是利用```Expires```或者```Cache-Control```这两个http response essay-header实现的，它们都用来表示资源在客户端缓存的有效期。

#####1.```Expires``` response header

Expires是http1.0提出的一个表示资源过期时间的essay-header，它描述的是一个绝对时间，由服务器返回，用GMT格式的字符串表示，如：Expires:Thu, 31 Dec 2037 23:55:55 GMT，它的缓存原理是:

1. 浏览器第一次跟服务器请求一个资源，服务器在返回这个资源的同时，在respone header加上Expires属性，如：

![](/assets/expires-response1.png)

2. 浏览器在接收到这个资源后，会把这个资源连同所有response header一起缓存下来；

3. 浏览器再请求这个资源时，先从缓存中寻找，找到这个资源后，拿出它的Expires跟当前的请求时间比较，如果请求时间在Expires指定的时间之前，就能命中缓存，否则就不行。

4. 如果缓存没有命中，浏览器直接从服务器加载资源时，Expires Header在重新加载的时候会被更新。

```
缺点:
由于它是服务器返回的一个绝对时间，在服务器时间与客户端时间相差较大时，缓存管理容易出现问题。
比如随意修改下客户端时间，就能影响缓存命中的结果。
```
#####1.```Cache-Control``` response header

http1.1的时候，提出了一个新的essay-header，就是Cache-Control，这是一个相对时间，在配置缓存的时候，以秒为单位，用数值表示，如：Cache-Control:max-age=315360000，它的缓存原理是：

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