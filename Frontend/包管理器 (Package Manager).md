### 1. **npm (Node Package Manager)**

- **简介**：npm 是 Node.js 的默认包管理器，也是世界上最大的软件注册表之一。它提供了丰富的命令行接口来管理依赖项，并且拥有庞大的社区支持。

```
npm init -y
-y意味着所有问题的回答都是yes，不要再问了
```

 

```cmd
# 初始化一个新的 npm 项目
npm init

# 安装一个依赖包到项目中
npm install <package-name>

# 更新所有依赖包到最新版本
npm update

# 运行自定义脚本
npm run <script-name>

```

npx 是一个随 **npm**（Node.js的包管理器）一起提供的命令行工具，它的主要作用是帮助你运行 **npm** 包中的可执行文件，而无需事先将这些包全局安装到系统中。



### 2. **Yarn**

- **简介**：由 Facebook 开发并维护，旨在解决 npm 在速度和安全性方面的一些局限性。Yarn 通过锁文件 (`yarn.lock`) 来确保不同环境中依赖的一致性。

```cmd
# 初始化一个新的 Yarn 项目
yarn init

# 安装一个依赖包到项目中
yarn add <package-name>

# 更新所有依赖包到最新版本
yarn upgrade

# 运行自定义脚本
yarn run <script-name>

```



### 3. **pnpm**

- **简介**：pnpm 是一种新型的包管理器，它解决了传统 npm 和 Yarn 在磁盘空间利用率上的不足，采用了一种称为“内容可寻址存储”的方法来存储依赖包。

```cmd
# 初始化一个新的 pnpm 项目
pnpm init

# 安装一个依赖包到项目中
pnpm add <package-name>

# 更新所有依赖包到最新版本
pnpm update

# 运行自定义脚本
pnpm run <script-name>

```



**Monorepo**（单一代码库）是一种代码管理策略，其中所有项目和子项目都存储在一个版本控制系统（如Git）中的同一个代码库里。与将不同模块分开存储在多个独立代码库中的传统做法（即多仓库）不同，monorepo允许所有的代码共享一个统一的存储位置。
