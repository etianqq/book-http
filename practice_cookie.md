# Cookie

cookie的基本思想就是让浏览器积累一组服务器特有的信息，每次访问服务器时都将这些信息提供给它。

注意点：

1. **浏览器要负责存储cookie信息**
2. 浏览器只向服务器发送服务器产生的那些cookie
3. HTTP cookie与JS中document.cookies设置，有相似之处，也有不同之处。


####Max-Age(有效期)
默认是会话cookie。

* 如果 cookie 不包含到期日期，则可视为**会话 cookie**。 会话 cookie 存储在内存中，决不会写入磁盘。 当浏览器关闭时，cookie 将从此永久丢失。
* 如果 cookie 包含到期日期，则可视为**持久性 cookie**。 在指定的到期日期，cookie 将从磁盘中删除。

####domain属性

**浏览器只向指定域中的服务器主机名发送cookie**。

这样服务器就将cookie限制在了特定的域中。

####secure属性
一个布尔值。

如果包含这个属性，就只有在HTTP使用SSL安全连接时才能发送cookie。

####HttpOnly属性

HttpOnly 属性限制了 cookie 对 HTTP 请求的作用范围。特别的，该属性指示用户代理忽略那些通过“非 HTTP” 方式对 cookie 的访问（比如js的接口）。

注意 HttpOnly 属性和 Secure 属性相互独立：一个 cookie 既可以是 HttpOnly 的也可以有 Secure 属性。

| HttpOnly属性 | document.cookie是否能读取cookie | 浏览器读取cookie |
| -- | -- |-- |
| 设置 | 否 |是 |
| 不设置 | 是 | 是 |

![](httponly.png)

