#响应头Cache-Control

每个资源都可以通过Http头Cache-Control来定义自己的缓存策略，Cache-Control控制谁在什么条件下可以缓存响应以及可以缓存多久。 最快的请求是不必与服务器进行通信的请求：通过响应的本地副本，我们可以避免所有的网络延迟以及数据传输的数据成本。为此，HTTP 规范允许服务器返回一系列不同的 Cache-Control 指令，控制浏览器或者其他中继缓存如何缓存某个响应以及缓存多长时间。

Cache-Control 头在 HTTP/1.1 规范中定义，取代了之前用来定义响应缓存策略的头（例如 Expires）。当前的所有浏览器都支持 Cache-Control，因此，使用它就够了。

Cache-Control中设置的常用指令。

**max-age**

该指令指定从当前请求开始，允许获取的响应被重用的最长时间（单位为秒。例如：Cache-Control:max-age=60表示响应可以再缓存和重用 60 秒。需要注意的是，在max-age指定的时间之内，浏览器不会向服务器发送任何请求，包括验证缓存是否有效的请求，也就是说，如果在这段时间之内，服务器上的资源发生了变化，那么浏览器将不能得到通知，而使用老版本的资源。所以在设置缓存时间的长度时，需要慎重。

**public和private**

如果设置了public，表示该响应可以在浏览器或者任何中继的Web代理中缓存，public是默认值，即Cache-Control:max-age=60等同于Cache-Control:public, max-age=60。

在服务器设置了private比如Cache-Control:private, max-age=60的情况下，表示只有用户的浏览器可以缓存private响应，不允许任何中继Web代理对其进行缓存 - 例如，用户浏览器可以缓存包含用户私人信息的 HTML 网页，但是 CDN 不能缓存。

**no-cache**

如果服务器在响应中设置了no-cache即Cache-Control:no-cache，那么浏览器在使用缓存的资源之前，必须先与服务器确认返回的响应是否被更改，如果资源未被更改，可以避免下载。这个验证之前的响应是否被修改，就是通过上面介绍的请求头If-None-match和响应头ETag来实现的。

    需要注意的是，no-cache这个名字有一点误导。
    设置了no-cache之后，并不是说浏览器就不再缓存数据，只是浏览器在使用缓存数据时，需要先确认一下数据是否还跟服务器保持一致。
    如果设置了no-cache，而ETag的实现没有反应出资源的变化，那就会导致浏览器的缓存数据一直得不到更新的情况。

**no-store**

如果服务器在响应中设置了no-store即Cache-Control:no-store，那么浏览器和任何中继的Web代理，都不会存储这次相应的数据。当下次请求该资源时，浏览器只能重新请求服务器，重新从服务器读取资源。

怎样决定一个资源的Cache-Control策略呢？下面这个流程图，可以帮到你。

![](/assets/cache4.png)
