# TO DO

- REACT

- 闭包

- diff算法

- 生命周期（旧版新版的变化是为了限制副作用，递归过程变成了循环过程，异步渲染可打断）

- 工程化的内容 -- webpack/vite/parcel/rollup

  Webpack: 

  - 模块化支持（支持多种模块格式ES modules，CommonJS），将所有资源视为模块 
  - 使用loader加载和解析所有非js文件
  - Plugin插件系统

  Vite

  - 快速开发服务器 使用ES Modules和浏览器直接加载模块，无需预打包，冷启动极快
  - 热模块更新(HMR): 只更新修改的模块而不是整个应用
  - 现代化建构 基于rollup的生产环境构建，支持tree shaking和代码拆分
  - 内置一些支持，无需额外配置

  | 特性                  | Webpack                       | Vite                       |
  | --------------------- | ----------------------------- | -------------------------- |
  | **核心原理**          | 模块打包（Bundle Everything） | 原生 ES Modules + 按需打包 |
  | **启动速度**          | 冷启动慢（依赖打包过程）      | 冷启动快（无需打包依赖）   |
  | **开发服务器**        | 使用 `webpack-dev-server`     | 内置开发服务器，速度快     |
  | **热模块更新（HMR）** | 速度较慢，刷新范围较大        | 高效且粒度细（模块级更新） |
  | **生产环境优化**      | 丰富的插件支持                | 基于 Rollup，性能优化出色  |
  | **配置复杂度**        | 配置灵活但复杂                | 开箱即用，默认配置简单     |
  | **生态系统**          | 成熟且丰富                    | 生态逐渐完善               |
  | **适用场景**          | 大型复杂项目                  | 现代前端框架开发           |

- 大图片加载怎么实现

- CI/CD 流程，自动化测试/部署

  ​	•	**GitHub Actions**:

  ​	•	用于自动化测试和部署。

  ​	•	**Jenkins** 或 **GitLab CI/CD**:

  ​	•	配置持续集成和部署流程。

  ​	•	**Vercel/Netlify/AWS**:

  ​	•	零配置的前端托管服务，适合快速部署项目。

- 懒加载

- ssr改造。

- Service worker

- 低代码

- React-DND 拖拽

-  媒体查询和响应式设计

- **热模块更新（HMR）**

- UMD

- 设计模式

- AWS/API/CICD

- STAR原则

- cloud部署

- CommonJS && ECMAScript

- Express.js && koa.js

- react虚拟dom，diff算法

- 做一些token相关的

- HMR热更新

- 跨域问题

- ### NEXT.JS的Data Handling & Deployment