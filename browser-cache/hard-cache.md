#强缓存


####原理

```
当浏览器对某个资源的请求命中了强缓存时，返回的http状态为200。
在chrome的开发者工具的network里面size会显示为from cache。
```
![](/assets/hard cache.png)

强缓存是利用```Expires```或者```Cache-Control```这两个http response essay-header实现的，它们都用来表示资源在客户端缓存的有效期。

