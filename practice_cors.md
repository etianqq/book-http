# CORS

####同源策略

出于安全考虑，浏览器会限制脚本中发起的跨域请求。比如，使用 XMLHttpRequest 对象和Fetch发起 HTTP 请求就必须遵守同源策略。 

具体而言，Web 应用程序通过 XMLHttpRequest 对象或Fetch能且只能向同域名的资源发起 HTTP 请求，而不能向任何其它域名发起请求。

####CORS(Cross-Origin Resource Sharing)
隶属于 W3C 的 Web 应用工作组( Web Applications Working Group )推荐了一种新的机制，即跨源资源共享（Cross-Origin Resource Sharing (CORS)）。这种机制让Web应用服务器能支持跨站访问控制，从而使得安全地进行跨站数据传输成为可能。

####1.简单请求

* 只使用 GET, HEAD 或者 POST 请求方法。如果使用 POST 向服务器端传送数据，则数据类型(Content-Type)只能是 application/x-www-form-urlencoded, multipart/form-data 或 text/plain中的一种。
* 不会使用自定义请求头（类似于 X-Modified 这种）。
```
Note: 这些跨站请求与以往浏览器发出的跨站请求并无异同。
并且，如果服务器不给出适当的响应头，则不会有任何数据返回给请求方。
```
![](/assets/cors-simple.png)

如果服务器端仅允许来自 http://foo.example 的跨站请求，它可以返回：
```Access-Control-Allow-Origin: http://foo.example```

####2.预请求(Preflighted requests)

“预请求”要求**必须先发送一个 OPTIONS 请求给目的站点***，来查明这个跨站请求对于目的站点是不是安全可接受的。这样做，是因为跨站请求可能会对目的站点的数据造成破坏。 当请求具备以下条件，就会被当成预请求处理：

* 请求以 GET, HEAD 或者 POST 以外的方法发起请求。或者，使用 POST，但请求数据为 application/x-www-form-urlencoded, multipart/form-data 或者 text/plain 以外的数据类型。比如说，用 POST 发送数据类型为 application/xml 或者 text/xml 的 XML 数据的请求。
* 使用自定义请求头（比如添加诸如 X-PINGOTHER）

####3.附带凭证信息的请求

