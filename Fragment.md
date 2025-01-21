### Fragment

- http 请求：

​	cookie：每次都会携带在 HTTP 头中，如果使用 cookie 保存过多数据会带来性能问题

​	localStorage 和 sessionStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信

**Cookie 通常需要封装使用的主要原因之一是 Cookie 的内容本质上是一个字符串**，而 localStorage 和 sessionStorage 本身是以键值对的形式操作数据的，这使得它们的原生 API 更直观和易用

**Cookie**：

- 需要在客户端和服务器之间共享小型数据（如会话 ID）。

- 需要设置安全属性（如 HttpOnly 和 Secure）来保护数据。

| 属性           | 作用                                                 | 使用场景                                | 适用性                                                       | 设置方式                                           |
| -------------- | ---------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------- |
| **`Secure`**   | 仅在 HTTPS 协议下发送 Cookie，确保数据的传输是加密的 | 防止在不安全的 HTTP 连接下泄露敏感信息  | 仅在 HTTPS 连接下有效                                        | `document.cookie = "name=value; Secure;"`          |
| **`HttpOnly`** | 防止 JavaScript 访问 Cookie，增强对 XSS 攻击的防护   | 防止恶意脚本访问敏感信息，如 Session ID | 禁止 JavaScript 访问 Cookie                                  | `document.cookie = "name=value; HttpOnly;"`        |
| **`SameSite`** | 限制 Cookie 的跨站点发送，防止 CSRF 攻击             | 防止 Cookie 在跨站请求中被泄露          | `Strict`（严格）: 完全阻止；`Lax`（宽松）: 只对危险请求有效；`None`（无）: 允许跨站点请求发送 Cookie | `document.cookie = "name=value; SameSite=Strict;"` |