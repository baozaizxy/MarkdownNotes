渲染后移

渲染是指数据渲染成DOM,DOM渲染成图像依然是浏览器要做的

不能通过props传递函数因为函数无法被序列化/stringtify为json



Prisma 是一个 **现代化的 TypeScript/JavaScript ORM（对象关系映射）**，用于与数据库交互，提供 **类型安全、自动生成 SQL 查询、简化数据库操作** 的能力。



 **use client 的底层运行机制**



在 Next.js **编译构建时（build time）**，它会：

1. **检测** use client **组件**：**遇到** use client **指令的组件**，Next.js 会将它标记为 **Client Component**。**没有** use client **的组件默认是 Server Component**。
2. **拆分** Server Component **和** Client Component：**Server Component 直接在服务器端渲染成 HTML，返回给客户端**。**Client Component 只返回一个占位 HTML（skeleton），然后浏览器下载 JavaScript 代码**，在客户端运行。
3. **客户端 Hydration（复水）**：服务器返回 HTML，客户端收到后会用 React Hydration **接管页面**，让 Client Component 拥有交互能力。



**SEO 需要完整的 HTML 结构**，但 use client 组件在服务器端只返回 <div> 占位符。**搜索引擎爬虫不会执行 JavaScript**，所以不会看到 use client 组件的内容。