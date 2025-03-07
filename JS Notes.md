### JS Notes

Map 返回新数组，不改变原数组

forEach 返回改变后的原数组

- `map`方法会生成一个新的数组，并将每次遍历的返回值按顺序放入新数组中。而`forEach`方法没有返回值，仅用于遍历数组。

Date-formate---->string

Date.parse() lead to milliseconds

**Math Method**

unlike other objects, the Math object has no constructor.

对于有构造函数的实例，可以new xxx，比如array object Date RegExp(正则对象 regular expression) Function

Math 只能引入来共享其静态方法和属性

Math.random()返回[0,1)之间的任意数

The `??` operator returns the first argument if it is not **nullish** (`null` or `undefined`).

The `break` statement "jumps out" of a loop.

The `continue` statement "jumps over" one iteration in the loop.

**set**

**RegEx**

| 元字符  | 说明                             | 示例                              |
| ------- | -------------------------------- | --------------------------------- |
| `.`     | 匹配任意单个字符（除了换行符）   | `/a.c/` 匹配 `"abc"`、`"a1c"`     |
| `\d`    | 匹配任何数字 `[0-9]`             | `/\d/` 匹配 `"123"` 中的数字      |
| `\D`    | 匹配非数字字符                   | `/\D/` 匹配 `"a"`、`"!"`          |
| `\w`    | 匹配字母、数字和下划线           | `/\w/` 匹配 `"a"`, `"1"`, `"_"`   |
| `\W`    | 匹配非字母、数字和下划线         | `/\W/` 匹配 `"!"`, `"@"`          |
| `\s`    | 匹配空白字符（空格、换行）       | `/\s/` 匹配空格                   |
| `\S`    | 匹配非空白字符                   | `/\S/` 匹配 `"a"`、`"1"`          |
| `^`     | 匹配字符串的开头                 | `/^a/` 匹配 `"abc"`               |
| `$`     | 匹配字符串的结尾                 | `/c$/` 匹配 `"abc"`               |
| `*`     | 匹配前一个字符 **0 次或多次**    | `/a*/` 匹配 `""`, `"a"`, `"aa"`   |
| `+`     | 匹配前一个字符 **1 次或多次**    | `/a+/` 匹配 `"a"`, `"aa"`         |
| `?`     | 匹配前一个字符 **0 次或 1 次**   | `/a?/` 匹配 `""`, `"a"`           |
| `{n}`   | 匹配前一个字符 **n 次**          | `/a{3}/` 匹配 `"aaa"`             |
| `{n,}`  | 匹配前一个字符 **至少 n 次**     | `/a{2,}/` 匹配 `"aa"`, `"aaa"`    |
| `{n,m}` | 匹配前一个字符 **n 到 m 次**     | `/a{2,3}/` 匹配 `"aa"` 或 `"aaa"` |
| `[]`    | 字符类，匹配括号内的任意字符     | `/[aeiou]/` 匹配元音字母          |
| `[^]`   | 字符类取反，匹配不在括号内的字符 | `/[^0-9]/` 匹配非数字字符         |
| `|`     | 或操作，匹配多个模式             | `/a|b/` 匹配 `"a"` 或 `"b"`       |
| `()`    | 分组，匹配并捕获                 | `/(ab)+/` 匹配 `"abab"`           |
| `\`     | 转义字符，匹配特殊字符           | `/\./` 匹配 `"."`                 |

**error**

```javascript
try {
  Block of code to try
}
catch(err) {
  Block of code to handle errors
}
finally {
  Block of code to be executed regardless of the try / catch result
}
```

**ReferenceError** 一般是引用了未声明的变量

**var && let && const**

var没有块作用域，已经不用了

**class**

A JavaScript class is **not** an object.

It is a **template** for JavaScript objects.

```javascript
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
  age(x) {
    return x - this.year;
  }
}

const date = new Date();
let year = date.getFullYear();

const myCar = new Car("Ford", 2014);
document.getElementById("demo").innerHTML=
"My car is " + myCar.age(year) + " years old.";
```

**style Guide**

- 变量 camelCase
- space around operator
- code indentation(缩进)
- statement with semicolon ;
- CSS uses hyphens in property-names (font-size).
- 尽量小写文件名
- Avoid global variables, avoid `new`, avoid `==`, avoid `eval()`

```html
<script src="myscript.js"></script>
```

**Don't use new Object()**

会导致代码冗余，而且会导致类型为object而不是应有的string等

```js
let x1 = "";             // new primitive string
let x2 = 0;              // new primitive number
let x3 = false;          // new primitive boolean
const x4 = {};           // new object
const x5 = [];           // new array object
const x6 = /()/;         // new regexp object
const x7 = function(){}; // new function object
```

原型、原型链

异步编程promise



作用域Scope ：

局部作用域/全局作用域（函数作用域/块作用域）

let和const声明的会产生块作用域block scope（不同代码块之间无法互相访问），var没有

每个函数在定义时都会记录创建它的作用域，称为其 **词法作用域**（Lexical Scope）。

let和const不会被变量提升，var会被变量提升

```js
console.log(hoistedVar); // 输出: undefined
var hoistedVar = 'Hoisted';

console.log(notHoisted); // 报错: Cannot access 'notHoisted' before initialization
let notHoisted = 'Not hoisted';
```

内容的生命周期：分配（声明） - 使用（读写） - 回收（垃圾回收器回收 ）

内存泄漏：程序中分配的内存由于某些原因未释放或者无法释放，称为内存泄漏

![截屏2025-01-06 下午4.32.36](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-06 下午4.32.36.png)

  ![截屏2025-01-06 下午4.33.29](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-06 下午4.33.29.png)

  但是当两个堆中的对象相互引用，尽管他们已经不再使用，垃圾回收器也不会回收，导致内存泄漏

标记清除法

![截屏2025-01-06 下午4.40.58](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-06 下午4.40.58.png)

垃圾回收机制(Garbage Collection)：JS中内存的分配和回收都是自动完成的，内存在不使用时会被垃圾回收器自动回收  

闭包(Closure): 闭包是指 **函数能够“记住”并访问其定义时的作用域**

内层函数使用外层函数的变量，形成闭包

```js
function outerFunction() {
  let outerVariable = 'I am outer';

  return function innerFunction() {
    console.log(outerVariable); // 闭包访问外部变量
  };
}

const closureFunction = outerFunction(); // outerFunction 执行完毕，但闭包仍保留对 outerVariable 的访问权限
closureFunction(); // 输出: I am outer
```

闭包可能导致内存泄漏的问题，因为内部变量被全局变量调 用不会被回收



函数提升：JS会把所有函数声明提升到作用域最前面 

函数的参数 ---> 动态参数和剩余参数

动态参数：Arguments是函数内部内置的伪数组变量，它包含了调用函数时传入的所有实参 

 剩余参数： 

![截屏2025-01-06 下午5.28.46](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-06 下午5.28.46.png)

真数组可以使用数组的方法

| **特点**         | **剩余参数 (...args)**   | **`arguments`**            |
| ---------------- | ------------------------ | -------------------------- |
| **类型**         | 数组 (Array)             | 类数组 (Array-like Object) |
| **灵活性**       | 支持数组方法，便于操作   | 需手动转换为数组           |
| **箭头函数支持** | ✅ 支持                   | ❌ 不支持                   |
| **参数控制**     | 只收集未被声明的剩余参数 | 包含所有传入参数           |



**箭头函数**

适用于本来需要匿名函数的地方，不绑定this更简洁

![截屏2025-01-06 下午5.43.57](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-06 下午5.43.57.png)

 继承上下文的this，沿用作用域链上一层的this，没有arguments，有剩余参数(...args。)



**事件捕获、事件冒泡、阻止冒泡、解绑事件**

捕获：大到小

冒泡：小到大 当一个元素触发事件后，会依次向上调用所有父级元素的同名事件

DOM.addEventListener(事件类型，事件处理函数，是否使用捕获机制)

false表示冒泡阶段触发，默认是false. 

阻止传播（同时阻止捕获和冒泡）：事件对象.stopPropagation()

解绑事件：避免重复绑定+释放内存

原生JS： removeEventListener

jQuery:

```javascript
// 绑定事件
$('#myButton').on('click', function () {
  console.log('Button clicked!');
});

// 解绑事件
$('#myButton').off('click');
```

react：无需手动解绑



**事件委托（Event Delegation）** 通过将事件监听器绑定到父级元素上，来管理子元素的事件。通过事件冒泡机制，当子元素触发事件时，这个事件会冒泡到父级元素，从而由父级元素的事件处理程序统一处理。

给父元素注册事件，触发子元素时会冒泡到父元素，从而触发事件

事件对象.target.tagname可以获取真正触发事件的元素



**事件循环eventloop**

JS是单线程的，为了解决这个问题，H5提出了web worker标准，允许JS创建多个线程。于是，JS中出现了同步和异步。

![截屏2025-01-07 下午5.11.43](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-07 下午5.11.43.png)

![截屏2025-01-07 下午5.14.55](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-07 下午5.14.55.png)

调用栈：调用栈是一个 LIFO（后进先出）结构，用于记录函数的调用顺序

异步任务队列（**Task Queue**）：异步任务队列存储的是已完成的异步任务回调，等待调用栈为空时被推入栈中执行

宏任务（Macro Task）：SetTimeout，SetInterval，I/O，UI渲染

微任务（Micro Task）: Promise.then 或 catch 的回调，MutationObserver，queueMicrotask

- 它通过 **调用栈** 和 **任务队列** 的配合，确保异步任务能够在同步代码之后依次执行。

- 微任务的优先级高于宏任务，这种机制可以确保更高效的任务调度



**location对象**

| 属性       | 描述                                           |
| ---------- | ---------------------------------------------- |
| `href`     | 获取或设置完整的 URL。                         |
| `protocol` | 获取协议部分（如 `https:`）。                  |
| `host`     | 获取主机名（如 `www.example.com:80`）。        |
| `hostname` | 获取域名部分（如 `www.example.com`）。         |
| `port`     | 获取端口号（如 `80` 或空字符串）。             |
| `pathname` | 获取路径部分（如 `/path/to/page`）。           |
| `search`   | 获取查询字符串（如 `?query=123`）。            |
| `hash`     | 获取片段标识符（如 `#section`）。              |
| `origin`   | 获取完整的源（如 `https://www.example.com`）。 |

| 方法           | 描述                                   |
| -------------- | -------------------------------------- |
| `assign(url)`  | 加载新的 URL，相当于重定向。           |
| `replace(url)` | 替换当前 URL，不能使用浏览器后退恢复。 |
| `reload()`     | 重新加载当前页面。                     |

**navigator对象**

| 属性            | 描述                                             |
| --------------- | ------------------------------------------------ |
| `userAgent`     | 获取用户代理字符串，描述浏览器和操作系统的信息。 |
| `platform`      | 获取操作系统平台（如 `Win32`、`MacIntel`）。     |
| `language`      | 获取浏览器的首选语言（如 `en-US`）。             |
| `onLine`        | 表示是否联网（`true` 或 `false`）。              |
| `vendor`        | 浏览器供应商名称。                               |
| `cookieEnabled` | 表示浏览器是否启用了 cookies。                   |

| 方法                               | 描述                                     |
| ---------------------------------- | ---------------------------------------- |
| `geolocation.getCurrentPosition()` | 获取用户的地理位置信息（需要用户授权）。 |
| `sendBeacon(url, data)`            | 用于向服务器发送少量数据。               |

**history对象**

| 属性     | 描述                           |
| -------- | ------------------------------ |
| `length` | 返回当前会话中的历史记录条数。 |
| `state`  | 返回当前历史记录的状态对象。   |

| 方法                              | 描述                                       |
| --------------------------------- | ------------------------------------------ |
| `back()`                          | 加载上一页（相当于用户点击后退按钮）。     |
| `forward()`                       | 加载下一页（相当于用户点击前进按钮）。     |
| `go(n)`                           | 加载历史记录中的指定页面，`n` 为相对索引。 |
| `pushState(state, title, url)`    | 将新的状态信息添加到会话历史中。           |
| `replaceState(state, title, url)` | 替换当前历史记录的状态信息。               |



**localStorage 本地存储**

存储在浏览器中，读取方便，容量较大，sessionStorage和localStorage约5M

localStorage：永久存储，除非手动删除，同一浏览器内多窗口共享，以键值对的形式存储使用



**创建对象的三种方式**

```js
// 使用字面量创建对象
const o = {
	name: "peiqi"
}

// 利用new Object创建对象
const o = new Object({ name: "peiqi"})
console.log(o)

// 利用构造函数创建对象
```

![截屏2025-01-09 下午5.31.19](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-09 下午5.31.19.png)

 构造函数要求：

1、命名以大写字母开头

2、只能以new操作符执行

new的过程被称为实例化，实例化构造函数没有参数时可以省略（）

构造函数内部无return，返回值即为新创建的对象

实例成员：实例对象中的属性和方法称为实例成员

构造函数的属性和方法被称为静态成员（静态属性和静态方法）



数据类型分为基本数据类型（primitive types）和引用类型(references types)

| **特性**             | **基本数据类型**                                             | **引用类型**                                                 |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **存储方式**         | 存储在栈中，值直接访问                                       | 引用存储在栈中，值存储在堆中                                 |
| **值的特性**         | 不可变，操作生成新值                                         | 可变，可以修改内部属性                                       |
| **比较方式**         | 按值比较                                                     | 按引用比较                                                   |
| **拷贝方式**         | 按值拷贝                                                     | 按引用拷贝                                                   |
| **基本数据类型包括** | `number`、`string`、`boolean`、`undefined`、`null`、`bigint`、`symbol` | `Object`、`Array`、`Function`、`Date`、`RegExp`、`Map`、`Set` 等 |

JavaScript 中的基本数据类型是原始类型（如 number、string、boolean 等）。当你访问这些基本数据类型的属性或方法时，JavaScript 会自动将它们包装为相应的对象，从而使它们具备方法和属性。这种自动的过程叫做**装箱（Boxing）**。

```js
let str = "hello";        // 基本数据类型
let strObj = new String("hello");  // String 包装类型对象

console.log(str.length);   // 输出 5
console.log(strObj.length);  // 输出 5
```



内置构造函数

原型

![截屏2025-01-10 下午10.34.19](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-10 下午10.34.19.png)

 

JS基本数据类型

```js
boolean number string null undefined symbol BigInt
```



##### 执行机制

包括编译阶段和执行阶段

- 词法分析:JS引擎将源代码解析为标记（token），即最小语法单元

  const（关键字）x（标识符）=（运算符）10（数值字面量）;（分号）

  ```js
  const x = 10;
  ```

- **语法分析器（Parser）** 会根据 **Token 序列** 生成 **抽象语法树AST（Abstract Syntax Tree）** 。若代码错误，抛出 SyntaxError

  - AST用处：

    Babel代码转换Transformation

    ESLint通过 AST 分析代码，找出错误或不符合规范的代码

    Prettier等格式化工具会基于 AST 重新排版代码

- 作用域分析:确定每个变量的作用域，并创建相应的词法环境（Lexical Environment）。在此阶段，所有的 `var` 和 `function` 声明会被提升到其所在作用域的顶部（即所谓的“变量提升”）。 注释：### 词法环境的组成部分



##### 作用域类型：

- **全局作用域**：在整个程序范围内都可访问的变量。
- **函数作用域**：仅在函数内部可见的变量。
- **块级作用域**：使用 `let` 和 `const` 声明的变量具有块级作用域，仅在 `{}` 内部可见。



变量存储在内存中，具体来说是存储在栈（Stack）和堆（Heap）中。

- **栈**：用于存储基本数据类型的值，如数字、字符串、布尔值等。
- **堆**：用于存储引用数据类型的值，如对象、数组等。



**LHS（Left-Hand Side）查找**和**RHS（Right-Hand Side）查找**。

LHS 查找是指在赋值操作中找到一个目标位置来存储某个值。它发生在等号左边的变量上。

```js
a = 2; // LHS 查找 'a'
```

RHS 查找是指在需要获取某个变量或表达式的值来进行计算或其他操作时进行的查找。它发生在等号右边的变量或表达式上。

```js
console.log(a); // RHS 查找 'a'
```



##### JavaScript 模块规范对比：CommonJS、AMD、ES Modules

JavaScript 的模块化规范主要经历了 **CommonJS、AMD（Asynchronous Module Definition）** 和 **ES Modules（ESM）** 三个重要阶段。它们主要用于 **管理 JavaScript 代码的模块化、依赖管理和加载方式**。



**CommonJS(CJS)** ： **Node.js** 采用的模块化规范，主要特点是 **同步加载**，适用于 **服务器端**，因为服务器端代码运行在本地，无需异步请求

所有代码执行时，模块已经加载完毕，无法做到动态按需加载

**不适用于前端**（浏览器不支持 require()，需要打包工具如 Webpack 转换）

```js
// math.js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

// 使用 module.exports 导出
module.exports = { add, subtract };

// app.js
const math = require('./math');  // 同步导入
console.log(math.add(2, 3));  // 输出：5
```





**AMD（Asynchronous Module Definition）** ：**RequireJS** 采用的模块化规范，主要用于 **前端**，支持 **异步加载模块**，适合浏览器环境。

能够异步加载、按需加载，适合前端。但语法复杂，可读性差。

```js
// math.js 定义模块
define([], function() {
    return {
        add: (a, b) => a + b,
        subtract: (a, b) => a - b
    };
});

// app.js  使用模块
require(['math'], function(math) {
    console.log(math.add(2, 3));  // 输出：5
});
```





**ES Modules（ESM）** 是 **ECMAScript 2015（ES6）** 引入的官方模块化方案，适用于 **现代 JavaScript 运行环境（浏览器 & Node.js）**。

```js
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// 默认导出
export default function multiply(a, b) {
    return a * b;
}

// app.js 导入
import { add, subtract } from './math.js';
import multiply from './math.js';

console.log(add(2, 3));  // 输出：5
console.log(multiply(2, 3));  // 输出：6

// 动态导入 按需加载
import('./math.js').then(math => {
    console.log(math.add(2, 3));  // 输出：5
});
```



| 规范         | 适用环境             | 语法                           | 加载方式                   | 主要特点                      |
| ------------ | -------------------- | ------------------------------ | -------------------------- | ----------------------------- |
| **CommonJS** | Node.js              | `require()` / `module.exports` | **同步加载**               | 适用于服务器端，缓存模块      |
| **AMD**      | 浏览器（RequireJS）  | `define()` / `require()`       | **异步加载**               | 适用于前端，按需加载          |
| **ESM**      | 现代浏览器 & Node.js | `import` / `export`            | **静态解析**，支持动态导入 | 官方标准，支持 `tree shaking` |



#### JS延迟加载的方式

延迟加载（Deferred Loading）是一种优化网页性能的技术，可以延迟加载页面中的资源（如脚本、样式表、图片等），从而加快页面的初始加载速度。

1. **懒加载图片（Lazy Loading Images）**

   ```html
   <img src="image.jpg" loading="lazy" alt="description">
   ```

2.  **懒加载脚本（Lazy Loading Scripts）**

   **使用 async 和 defer 属性**：

   - async：脚本异步加载，不会阻塞页面渲染。

   - defer：脚本延迟执行，直到页面解析完毕后执行脚本。

   ```html
   <script src="script.js" async></script>
   <script src="script.js" defer></script>
   ```

3. **动态插入脚本**：

   ```js
   const loadScript = (src) => {
     const script = document.createElement('script');
     script.src = src;
     script.async = true;  // 或者 script.defer = true;
     document.head.appendChild(script);
   };
   
   // 在需要时加载脚本
   loadScript('script.js');
   ```

4. 懒加载组件

   ```react
   import React, { Suspense, lazy } from 'react';
   
   // 懒加载组件
   const LazyComponent = lazy(() => import('./LazyComponent'));
   
   function App() {
     return (
       <div>
         <Suspense fallback={<div>Loading...</div>}>
           <LazyComponent />
         </Suspense>
       </div>
     );
   }
   ```

   

#### 严格模式的限制

1. 变量声明必须显式
2. 全局对象的this不会指向window而是undefined
3. **对象不能定义重复的属性名**
4. **不可删除 configurable: false 的属性**



#### 使用JS判断一个数组

1.  **Array.isArray()**

2. ```js
   console.log([1, 2, 3] instanceof Array); // true
   console.log("hello" instanceof Array);   // false
   console.log({} instanceof Array);        // false
   ```

3. **Object.prototype.toString.call()**

   ```js
   console.log(Object.prototype.toString.call([1, 2, 3])); // "[object Array]"
   console.log(Object.prototype.toString.call("hello"));   // "[object String]"
   console.log(Object.prototype.toString.call({}));        // "[object Object]"
   ```

4. **constructor 属性**

   ```js
   console.log([1, 2, 3].constructor === Array); // true
   console.log("hello".constructor === Array);   // false
   console.log({}.constructor === Array);        // false
   ```

   

#### 遍历对象的方法

1.  **for...in**，**会遍历原型链上的属性**，需要使用 hasOwnProperty() 过滤：

   ```js
   for (let key in obj) {
       if (obj.hasOwnProperty(key)) {
           console.log(key, obj[key]);
       }
   }
   ```

2. **Object.keys()**

   只返回对象自身的属性（不包括原型链上的）。

   可与 forEach()、map() 等数组方法配合使用。

   仅返回**可枚举**的属性，无法获取不可枚举的属性。

   ```js
   const obj = { a: 1, b: 2, c: 3 };
   
   Object.keys(obj).forEach(key => {
       console.log(key, obj[key]);
   });
   // 输出:
   // a 1
   // b 2
   // c 3
   ```

3. **Object.values()**
   Object.values() 返回对象所有可枚举属性的值，适用于仅需要属性值的情况。

4. **Object.entries()**
   Object.entries() 返回对象的**可枚举属性**键值对数组。

   ```js
   const obj = { a: 1, b: 2, c: 3 };
   
   Object.entries(obj).forEach(([key, value]) => {
       console.log(key, value);
   });
   // 输出:
   // a 1
   // b 2
   // c 3
   ```



#### JavaScript 大数相加 

在 JavaScript 中，由于 Number 类型的安全整数范围限制（Number.MAX_SAFE_INTEGER 约为 2^53 - 1），直接对大整数相加可能会导致精度丢失。

因此，可以使用 **字符串模拟** 大整数相加，或者使用 **BigInt** 类型。

BigInt 能够处理任意长度的整数运算，不会有精度丢失的问题。

字符串

```js
function addBigNumbers(a, b) {
  let res = '';
  let carry = 0;
  let i = a.length - 1;
  let j = b.length - 1;

  while (i >= 0 || j >= 0 || carry) {
    const x = i >= 0 ? Number(a[i]) : 0;
    const y = j >= 0 ? Number(b[j]) : 0;
    const sum = x + y + carry;
    
    res = (sum % 10) + res; // 取个位数
    carry = Math.floor(sum / 10); // 进位
    
    i--;
    j--;
  }

  return res;
}

console.log(addBigNumbers("12345678901234567890", "98765432109876543210"));
// 输出: "111111111011111111100"
```



#### 拖拽的监控

1. Event.clientX,Y表示**鼠标指针相对于浏览器可视窗口（viewport）的** **左上角**
2. offsetLeft 表示**当前元素相对于其最近的** offsetParent（一般是 position 不是 static 的父元素）的 **左侧偏移量**。
3. 给mousedown,mousemove及mouseup事件绑定事件



#### 创造类的方法

1.  **使用 class（ES6 标准）**

   ```js
   class Person {
     constructor(name) {
       this.name = name;
     }
   
     sayHello() {
       console.log(`Hello, my name is ${this.name}`);
     }
   }
   
   const p = new Person("Alice");
   p.sayHello(); // Hello, my name is Alice
   ```

   ​	•	**ES6 语法**，更清晰、面向对象的写法。

   ​	•	**支持继承**（extends 关键字）。

   ​	•	**语法糖**，本质上是 function + prototype 的封装。

2. **使用 function 构造函数（ES5 及更早）**

   ```js
   function Person(name) {
     this.name = name;
   }
   
   Person.prototype.sayHello = function() {
     console.log(`Hello, my name is ${this.name}`);
   };
   
   const p = new Person("Bob");
   p.sayHello(); // Hello, my name is Bob
   ```

   ​	•	传统的 **构造函数 + 原型** 方法，等效于 class。

   ​	•	new 关键字创建实例，方法定义在 prototype 上。

3. **使用 Object.create()**

   ```js
   const personProto = {
     sayHello() {
       console.log(`Hello, my name is ${this.name}`);
     }
   };
   
   const p = Object.create(personProto);
   p.name = "Charlie";
   p.sayHello(); // Hello, my name is Charlie
   ```

4. **使用工厂函数（Factory Function）**

   ```js
   function createPerson(name) {
     return {
       name,
       sayHello() {
         console.log(`Hello, my name is ${this.name}`);
       }
     };
   }
   
   const p = createPerson("David");
   p.sayHello(); // Hello, my name is David
   ```

   **避免使用 this**，适合**函数式编程**。
