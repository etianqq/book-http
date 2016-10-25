# Cookie

####有效期
* 如果 cookie 不包含到期日期，则可视为会话 cookie。 会话 cookie 存储在内存中，决不会写入磁盘。 当浏览器关闭时，cookie 将从此永久丢失。
* 如果 cookie 包含到期日期，则可视为持久性 cookie。 在指定的到期日期，cookie 将从磁盘中删除。

####HttpOnly属性
| HttpOnly属性 | document.cookie是否能读取cookie | 浏览器读取cookie |
| -- | -- |-- |
| 设置 | 否 |是 |
| 不设置 | 是 | 是 |

如果cookie是服务端通过Set-Cookies方式添加的，那么，无论是否设置httponly属性，客户端都无法通过js代码清除session cookie。 （我的理解对吗？？？？？）

![](httponly.png)
