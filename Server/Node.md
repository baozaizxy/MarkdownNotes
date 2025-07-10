# Node

浏览器V8引擎会把js编译。为机器语言

脱离浏览器后，node是V8引擎的容器，Node是C++写的，可以直接运行在电脑上

-  读写电脑上的文件
- 连接数据库
- 充当web服务器

 node帮助js运行在操作系统上，才能够连接数据库，读写文件，使js能够当后端语言使用

node使用单线程，在操作系统任务时同样使用event loop 

 Synchronous code 同步代码

 有global 没window

 node REPL

Read	Evaluate 	print	Loop 

process

process 是 Node.js 的一个全局对象，它提供了有关当前 Node.js 进程的信息和控制操作

| **类别** | **名称**                | **描述**                                                   | **示例**                                      |
| -------- | ----------------------- | ---------------------------------------------------------- | --------------------------------------------- |
| 属性     | `process.argv`          | 命令行参数数组。                                           | `console.log(process.argv)`                   |
| 属性     | `process.env`           | 当前环境变量对象。                                         | `console.log(process.env.PATH)`               |
| 属性     | `process.cwd()`         | 返回当前工作目录。                                         | `console.log(process.cwd())`                  |
| 属性     | `process.pid`           | 当前进程的进程 ID。                                        | `console.log(process.pid)`                    |
| 属性     | `process.platform`      | 当前操作系统平台（如 `win32`、`darwin`、`linux`）。        | `console.log(process.platform)`               |
| 属性     | `process.arch`          | 当前 CPU 架构（如 `x64`、`arm`）。                         | `console.log(process.arch)`                   |
| 属性     | `process.version`       | 当前 Node.js 的版本。                                      | `console.log(process.version)`                |
| 属性     | `process.versions`      | 包含 Node.js 和其依赖库版本的对象。                        | `console.log(process.versions)`               |
| 方法     | `process.exit([code])`  | 退出当前进程，`code` 表示退出码（默认 `0` 表示正常退出）。 | `process.exit(1)`                             |
| 方法     | `process.nextTick()`    | 在当前事件循环结束后立即执行回调函数。                     | `process.nextTick(() => console.log('Done'))` |
| 方法     | `process.on(event)`     | 监听事件，如 `exit`、`uncaughtException` 等。              | `process.on('exit', () => {...})`             |
| 方法     | `process.uptime()`      | 获取当前进程运行时间（以秒为单位）。                       | `console.log(process.uptime())`               |
| 方法     | `process.memoryUsage()` | 返回当前进程的内存使用情况。                               | `console.log(process.memoryUsage())`          |
| 方法     | `process.hrtime()`      | 返回高分辨时间，用于测量操作的精确时间（单位是纳秒）。     | `const t = process.hrtime();`                 |

常见事件

| **事件名称**        | **描述**                                                     | **示例**                                          |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| `exit`              | 当进程即将退出时触发，执行最后的清理操作。                   | `process.on('exit', () => {...})`                 |
| `uncaughtException` | 捕获未处理的异常，防止程序崩溃（建议只用于记录日志，不推荐继续运行）。 | `process.on('uncaughtException', (err) => {...})` |
| `SIGINT`            | 当按下 `Ctrl+C` 时触发。                                     | `process.on('SIGINT', () => {...})`               |

**CLI** 是 **Command Line Interface** 的缩写，指的是**命令行界面**

 

| CMD                 | 含义                         |
| ------------------- | ---------------------------- |
| pwd                 | 显示当前工作目录的绝对路径   |
| rm -r dir_name      | 删除目录及其内容             |
| rm -f file.txt      | 强制删除文件（即使文件只读） |
| cp                  | 复制                         |
| mv                  | 移动文件或重命名文件         |
| cat                 | 显示文件内容                 |
| nano / vim          | 命令行文本编辑器             |
| ping                | 测试与目标主机的连接         |
| ifconfig / ip(推荐) | 显示或配置网络接口           |

很多常见的 CLI 指令与 Linux 指令完全相同。例如，ls、cd、mkdir、rm 等指令在 Linux 和大部分 Unix-like 系统中是通用的。  



不需要单独安装npm,它和node.js是一起的

 Node.js 的模块系统基于 **CommonJS** 标准

Common.js的写法正在被ESM的写法取代

Package.json: 

| type值   | 模块系统 |
| -------- | -------- |
| module   | ESM      |
| Commonjs | CommonJS |

**CommonJS 与 ESM 的对比表**

| 特性             | **CommonJS** (`require/module.exports`)                    | **ESM** (`import/export`)                                    |
| ---------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **导入语法**     | `const module = require('./module');`                      | `import module from './module.js';`                          |
| **导出单个值**   | `module.exports = value;`                                  | `export default value;`                                      |
| **导出多个值**   | 使用对象包装多个值：<br>`module.exports = { key1, key2 };` | 命名导出：<br>`export const key1 = value1;` <br>`export const key2 = value2;` |
| **作用域**       | 独立作用域，不污染全局                                     | 独立作用域，不污染全局                                       |
| **加载时机**     | 动态加载，运行时解析                                       | 静态加载，编译时解析                                         |
| **文件扩展名**   | `.js`                                                      | `.js` 或 `.mjs`（推荐使用 `.mjs`）                           |
| **异步加载支持** | 不直接支持，但可以结合异步函数实现                         | 原生支持（动态导入）：<br>`import('./module.js').then(...)`  |
| **支持环境**     | Node.js                                                    | Node.js 和现代浏览器                                         |
| **默认导出语法** | 使用 `module.exports = value;`                             | 使用 `export default value;`                                 |
| **命名导出语法** | 使用对象：<br>`module.exports = { key1, key2 };`           | `export const key1 = value1;` <br>`export const key2 = value2;` |
| **动态导入支持** | 使用 `require()`                                           | 使用 `import()`                                              |
| **顶级 `await`** | 不支持                                                     | 支持                                                         |
| **模块优化能力** | 动态加载，优化较差                                         | 静态加载，优化更好                                           |

   

只想要import不需要export时， 可以直接import ‘./util.js’不需要from，就会直接执行execute. 这个文件

<必须的> 

[可选的]

 

js处理异步使用callback

可能发生异步的三件事asynchronous

1. interact with network
2. time function(set timeout/ set interval)
3. interact with storage（file system/database ）   

为了解决callback hell，创造了 promise

Type:nodule 没有global，无法读取相对路径  

string和code有不同的编码方式



解构

```js
const nums = [1,2,3]
const [first] = nums
// first === 1
```

 

JS尽量都不去修改所有的数据结构，对数据的增删改查尽量做到return一个新的回去

regression test 回归测试

ingredation test 集成测试

 Jest框架:可以用来做unit test 

名字中含有.test就会自动查找文件并进行test

Assertion 断言

在命令行使用 '--save-dev'将会保存在devDependencies而不是dependencies 

devDependencies是开发的依赖项而不是运行app所需的，所以部署的时候不会部署这部分 

Refactor 重构

BDD：behaviour-driven-development

TDD: test-driven-development



Interpolation 插值



### node.js的特点

- 基于事件驱动及**非阻塞 I/O（Non-blocking I/O）**：它通过 **事件循环** 来处理各种操作，而不是阻塞式地等待每个操作完成后再继续。

  **事件**：在 Node.js 中，操作（如文件读取、网络请求、数据库查询等）通常会发出事件。Node.js 通过监听这些事件来执行相应的回调函数。

  **事件循环（Event Loop）**：Node.js 使用一个单线程的事件循环来处理任务。当你调用异步操作时，Node.js 会将任务交给系统处理，而不会阻塞当前线程。处理完的任务会触发事件，回调函数会被执行。

- **单线程：** Node.js使用单线程处理请求，避免了传统多线程模型中线程切换的开销，提高了处理请求的效率。

- **基于V8引擎：** Node.js使用Google Chrome浏览器中的V8引擎解释执行JavaScript代码，具有高性能和高效的特点。

#### 单线程的优缺点

**Pros**

- 轻量级，避免了传统多线程模型中创建和销毁线程的开销
- 由于 Node.js 使用事件循环（Event Loop）来处理异步 I/O 操作，只有一个主线程，所以没有传统多线程中的线程上下文切换。这意味着 Node.js 在处理大量并发时，**不需要切换线程的上下文**，避免了多线程模式下的性能开销。
- 由于 Node.js 单线程的特性和非阻塞 I/O，特别适合 **I/O 密集型任务**（如文件操作、网络请求、数据库查询等）。它能够在等待 I/O 操作完成的同时继续执行其他任务，极大提高了系统的并发能力和响应速度。

**Cons**

- **CPU 密集型任务性能较差**，虽然 Node.js 在处理 I/O 密集型任务时表现优异，但对于 **CPU 密集型任务**（如复杂计算、大规模数据处理等），由于 Node.js 是单线程的，CPU 只能使用一个核心来执行任务，因此处理大量 CPU 密集型任务时，可能会造成主线程的阻塞，影响其他请求的响应速度
- **没有多核处理能力**，Node.js 默认是单线程的，因此它本身无法利用多核 CPU。如果服务器有多个 CPU 核心，Node.js 只能使用其中一个核心，这意味着它不能充分发挥多核 CPU 的并发能力。
- **错误容易导致进程崩溃**，在单线程的环境中，任何未捕获的异常或错误都可能导致整个 Node.js 进程崩溃。
