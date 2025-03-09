### react

使用JS直接操作DOM浏览器会进行大量的重绘重排

原生JS没有组件化的编码方案，代码复用率极低

JSX 比 HTML 更加严格。你必须闭合标签，如 `<br />`。你的组件也不能返回多个 JSX 标签。你必须将它们包裹到一个共享的父级中，比如 `<div>...</div>` 或使用空的 `<>...</>` 包裹

react使用组件化模式，声明式编码（对应js和jquery是命令式编码），提高开发效率及组件复用率

 使用虚拟DOM+Diffing算法，尽量减少与真实DOM的交互。

babel es6-->es5  

```html
<script type="text/babel"></script>
```



函数式组件：适合简单组件的定义

类式组件：适合复杂组件的定义。  

js分号可加可不加 一般不加

![截屏2025-01-05 下午3.30.02](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2025-01-05 下午3.30.02.png)

```react
//必须继承React.Component
//然后重写Render()方法，该方法一定要有返回值，返回一个虚拟DOM
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
//渲染 【这个跟之前也是一样的】
ReactDOM.Render(<Welcom name = "ss" />,document.getElementById("div"));
```

执行过程：

 1.React解析组件标签，找到相应的组件

 2.发现组件是类定义的，随后new出来的类的实例，并通过该实例调用到原型上的render方法

 3.将render返回的虚拟DOM转化为真实的DOM,随后呈现在页面中





组件实例的三大属性：props / state / refs 



浅拷贝：引用地址被复制，原始对象和新对象共享同一个引用，修改引用类型会相互影响。

 Slice / assign / ...(展开运算符) / concat  

```js
const array = [1, 2, 3];
const shallowCopy = array.slice(); // 浅拷贝
shallowCopy[0] = 100;

console.log(array);       // [1, 2, 3]，原数组不变
console.log(shallowCopy); // [100, 2, 3]
```

深拷贝：深拷贝会递归地复制对象的所有层级属性，无论是基本类型还是引用类型，都会创建全新的副本，因此原对象和新对象完全独立。

JSON.stringify() 和 JSON.parse() 是简单快捷的深拷贝方法



- `<section>` 是小写的，所以 React 知道我们指的是 HTML 标签。
- `<Profile />` 以大写 `P` 开头，所以 React 知道我们想要使用名为 `Profile` 的组件

![截屏2024-12-22 下午4.32.52](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2024-12-22 下午4.32.52.png)

1. `{` 开启 JavaScript 表达式
2. `baseUrl + person.imageId + person.imageSize + '.jpg'` 会生成正确的 URL 字符串
3. `}` 结束 JavaScript 表达式

```react
function AlertButton({ message, children }) {
  // 多个props参数，{messgae, children}解构
  return (
    <button onClick={() => alert(message)}>
      {children}
    </button>
  );
}
```



#### 添加交互

##### **state 如同一张快照** 

与普通 JavaScript 变量不同，React 状态的行为更像一个快照。设置它并不改变你已有的状态变量，而是触发一次重新渲染。这在一开始可能会让人感到惊讶！

```react
console.log(count);  // 0
setCount(count + 1); // 请求用 1 重新渲染
console.log(count);  // 仍然是 0！
```

React 的 setState 或 useState 中的状态更新并不会立即修改状态的值。

状态更新被“安排”在当前事件处理完成后由 React 合并并生效。这是为了优化性能，避免不必要的重新渲染

如果需要在状态更新后获取最新值，可以使用 useEffect 钩子来监听状态变化。

**react只会在渲染时使用新的快照以及时渲染 但是若要马上print或者alert以及任何同步的操作就都还是未更新的state，而state会在所有动作结束后，最后才执行**

**更改state对象**

通常情况下，你会使用 `...` 展开语法来复制你想改变的对象和数组。

也可以使用immer库来减少重复代码

```react
 import { useImmer } from 'use-immer';
 const [person, updatePerson] = useImmer({
    name: 'Niki de Saint Phalle',
    artwork: {
      title: 'Blue Nana',
      city: 'Hamburg',
      image: 'https://i.imgur.com/Sd1AgUOm.jpg',
    }
  });

  function handleNameChange(e) {
    updatePerson(draft => {
      draft.name = e.target.value;
    });
  }
```

**React 不会跨 \*多个\* 需要刻意触发的事件（如点击）进行批处理**——每次点击都是单独处理的。

​	•	**传递值的方式**（比如 setState(number + 1)）会直接替换 state，但在异步更新中，它可能基于旧的值计算新的 state，导致问题。

​	•	**传递函数的方式**（比如 setState(n => n + 1)）确保每次状态更新时，React 都会使用最新的 state 来计算新值，避免了依赖快照的问题。

总而言之，以下是你可以考虑传递给 `setNumber` state 设置函数的内容：

- **一个更新函数**（例如：`n => n + 1`）会被添加到队列中。
- **任何其他的值**（例如：数字 `5`）会导致“替换为 `5`”被添加到队列中，已经在队列中的内容会被忽略。

##### 状态管理

命令式 UI 编程的例子中，表单**没有使用** React 生成，而是使用原生的DOM

在 React 中，你不必直接去操作 UI —— 你不必直接启用、关闭、显示或隐藏组件。相反，你只需要 **声明你想要显示的内容，** React 就会通过计算得出该如何去更新 UI。

花一点时间来重构你的 state 结构，会让你的组件更容易被理解，减少重复并且避免歧义。你的目的是**防止出现在内存中的 state 不代表任何你希望用户看到的有效 UI 的情况。**

**state的结构**

- **如果某两个 state 变量总是一起变化，则将它们统一成一个 state 变量可能更好**

- **因为 `isSending` 和 `isSent` 不应同时为 `true`，所以最好用一个 `status` 变量来代替它们，这个 state 变量可以采取三种有效状态其中之一**：`'typing'` (初始), `'sending'`, 和 `'sent'`

  仍然可以声明一些常量，以提高可读性：

  ```react
  const isSending = status === 'sending';
  
  const isSent = status === 'sent';
  ```

  但它们不是 state 变量，所以你不必担心它们彼此失去同步。

- 避免冗余的state，如果它可以从计算中得出，则不应该单独放在state中

- #### 不要在 state 中镜像 props

- 避免深度嵌套的state，**如果 state 嵌套太深，难以轻松更新，可以考虑将其“扁平化”**

  •	childIds.map() 会动态生成一个 PlaceTree 的列表。

  •	React 要求在渲染任何 **列表** 时（由 .map() 等方法生成的元素），每个子元素都必须有一个唯一的 key。

##### 组件间共享状态

状态提升在父组件中使用state

##### state进行保留和重置

只要一个组件还被渲染在 UI 树的相同位置，React 就会保留它的 state。 如果它被移除，或者一个不同的组件被渲染在相同的位置，那么 React 就会丢掉它的 state。

它是位于相同位置的相同组件，所以对 React 来说，它是同一个计数器。

```react
      {isFancy ? (
        <Counter isFancy={true} /> 
      ) : (
        <Counter isFancy={false} /> 
      )}
    // 这种会保留state
```

##### 迁移状态逻辑至Reducer中

const [tasks, dispatch] = useReducer(tasksReducer, initialTasks);
task: id  dispatch: action	tasksReducer：import的处理函数 initialTasks:初始化数据

reducer 函数就是你放置状态逻辑的地方。它接受两个参数，分别为当前 state 和 action 对象，并且返回的是更新后的 state

由于 `reducer` 函数接受 state（`tasks`）作为参数，因此你可以 **在组件之外声明它**

 Immer 为你提供了一种特殊的 `draft` 对象，你可以通过它安全地修改 state

##### 使用context深层传递参数

##### Context 的使用场景 

- 在使用 context 之前，先试试传递 props 或者将 JSX 作为 `children` 传递。

- **主题：** 如果你的应用允许用户更改其外观（例如暗夜模式），你可以在应用顶层放一个 context provider，并在需要调整其外观的组件中使用该 context。
- **当前账户：** 许多组件可能需要知道当前登录的用户信息。将它放到 context 中可以方便地在树中的任何位置读取它。某些应用还允许你同时操作多个账户（例如，以不同用户的身份发表评论）。在这些情况下，将 UI 的一部分包裹到具有不同账户数据的 provider 中会很方便。
- **路由：** 大多数路由解决方案在其内部使用 context 来保存当前路由。这就是每个链接“知道”它是否处于活动状态的方式。如果你创建自己的路由库，你可能也会这么做。
- **状态管理：** 随着你的应用的增长，最终在靠近应用顶部的位置可能会有很多 state。许多遥远的下层组件可能想要修改它们。通常 [将 reducer 与 context 搭配使用](https://zh-hans.react.dev/learn/scaling-up-with-reducer-and-context)来管理复杂的状态并将其传递给深层的组件来避免过多的麻烦。

![截屏2024-12-30 下午3.53.14](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2024-12-30 下午3.53.14.png)

##### 使用ref引用

`ref.current` 属性访问该 ref 的当前值

这个值是有意被设置为可变的，意味着你既可以读取它也可以写入它。就像一个 React 追踪不到的、用来存储组件信息的秘密“口袋”。（这就是让它成为 React 单向数据流的“脱围机制”的原因 

**组件不会在每次递增时重新渲染。** 与 state 一样，React 会在每次重新渲染之间保留 ref。但是，设置 state 会重新渲染组件，更改 ref 不会！

![截屏2024-12-30 下午8.27.39](/Users/sherryzheng_mac/Library/Application Support/typora-user-images/截屏2024-12-30 下午8.27.39.png)

ref.current没有state的限制，修改ref.current不是异步行为

- 不要在渲染过程中读取或写入 `ref.current`。这使你的组件难以预测。
- **将 ref 视为脱围机制**。当你使用外部系统或浏览器 API 时，ref 很有用。如果你很大一部分应用程序逻辑和数据流都依赖于 ref，你可能需要重新考虑你的方法。

由于 React 会自动处理更新 DOM以匹配你的渲染输出，因此你在组件中通常不需要操作 DOM。但是，有时你可能需要访问由 React 管理的 DOM 元素 —— 例如，让一个节点获得焦点、滚动到它或测量它的尺寸和位置。在 React 中没有内置的方法来做这些事情，所以你需要一个指向 DOM 节点的 **ref** 来实现。

useRef` Hook 返回一个对象，该对象有一个名为 `current` 的属性。最初，`myRef.current` 是 `null`。当 React 为这个 `<div>` 创建一个 DOM 节点时，React 会把对该节点的引用放入 `myRef.current

**避免更改由 React 管理的 DOM 节点。**

用ref删除由react控制的dom, 会导致崩溃

可以像其他prop一样将ref从父组件中传到子组件，再通过useRef实现父组件对子组件的控制

##### 使用effect同步

每当你的组件渲染时，React 会先更新页面，然后再运行 `useEffect` 中的代码。换句话说，**`useEffect` 会“延迟”一段代码的运行，直到渲染结果反映在页面上**。

子组件中不可以出现对DOM进行修改的函数，因为它试图在渲染期间对 DOM 节点进行操作。在 React 中，渲染应该是纯粹的计算JSX，不应该包含任何像修改 DOM 这样的副作用。解决办法是 **使用 `useEffect` 包裹副作用，把它分离到渲染逻辑的计算过程之外**

默认情况下，Effect 会在 **每次** 渲染后运行。

```react
useEffect(() => {
  // 这里的代码会在每次渲染后运行
});

useEffect(() => {
  // 这里的代码只会在组件挂载（首次出现）时运行
}, []);
```

开发环境下react会挂载两次以检查组件被卸载时有没有关闭连接，生产环境下恢复正常只挂载一次



##### 不必使用effect的情况

- **不必为了渲染而使用 Effect 来转换数据。**
- **不必使用 Effect 来处理用户事件。**

**如果一个值可以基于现有的 props 或 state 计算得出，不要把它作为一个 state，而是在渲染期间直接计算这个值**。

**通过将 `userId` 作为 `key` 传递给 `Profile` 组件，使  React 将具有不同 `userId` 的两个 `Profile` 组件视为两个不应共享任何状态的不同组件**。

当你决定将某些逻辑放入事件处理函数还是 Effect 中时，你需要回答的主要问题是：从用户的角度来看它是 **怎样的逻辑**。如果这个逻辑是由某个特定的交互引起的，请将它保留在相应的事件处理函数中。如果是由用户在屏幕上 **看到** 组件时引起的，请将它保留在 Effect 中。

尽可能在渲染期间进行计算，以及在事件处理函数中调整 state

初始化问题：

如果某些逻辑必须在 **每次应用加载时执行一次**，而不是在 **每次组件挂载时执行一次**，可以添加一个顶层变量来记录它是否已经执行过了：

```react
let didInit = false;

function App() {
  useEffect(() => {
    if (!didInit) {
      didInit = true;
      // ✅ 只在每次应用加载时执行一次
      loadDataFromLocalStorage();
      checkAuthToken();
    }
  }, []);
  // ...
}

// 或者在模块初始化前执行
if (typeof window !== 'undefined') { // 检测我们是否在浏览器环境
   // ✅ 只在每次应用加载时执行一次
  checkAuthToken();
  loadDataFromLocalStorage();
}

function App() {
  // ...
}
```

数据尽量从父组件传向子组件 而非相反

useEffect的return在依赖项发生变化或者组件卸载时执行，以确保副作用被正确清理（例如取消订阅、移除事件监听器等）。

每次 useEffect 执行时：

​	1.	**局部作用域的特性**：let ignore = false 定义了一个局部变量，只存在于当前的 useEffect 执行上下文中。

​	2.	**闭包特性**：异步操作（如 fetchResults 的 then 回调）会捕获当前的 ignore，并将其绑定到该 useEffect 的执行环境中。

​	3.	**React 的行为**：当依赖发生变化时，React 不会重用之前的 useEffect，而是完全重新执行一次。因此，每次都会生成新的 ignore。



- 如果你可以在渲染期间计算某些内容，则不需要使用 Effect。
- 想要缓存昂贵的计算，请使用 `useMemo` 而不是 `useEffect`。
- 想要重置整个组件树的 state，请传入不同的 `key`。
- 想要在 prop 变化时重置某些特定的 state，请在渲染期间处理。
- 组件 **显示** 时就需要执行的代码应该放在 Effect 中，否则应该放在事件处理函数中。
- 如果你需要更新多个组件的 state，最好在单个事件处理函数中处理。
- 当你尝试在不同组件中同步 state 变量时，请考虑状态提升。
- 你可以使用 Effect 获取数据，但你需要实现清除逻辑以避免竞态条件



##### 响应式Effect的生命周期





- 在 JavaScript 中，如果对象和函数是在不同时间创建的，则它们被认为是不同的。
- 尽量避免对象和函数依赖。将它们移到组件外或 Effect 内。



##### 自定义Hook

**自定义 Hook 共享的只是状态逻辑而不是状态本身。对 Hook 的每个调用完全独立于对同一个 Hook 的其他调用**。





JSX是为了写虚拟dom更加容易，不用像react.createElement()这样来创建，babel将JSX翻译成react.createElement()

 XML早起用于存储和传输数据，已被JSON取代

```xml
<student>
  <name>tom</name>
  <age>19</age>
</student>
```

 JSON: parse(解析成js) stringfy(JS转成json )

JSX中使用小驼峰 比如：fontSize 

component需要start with uppercase letter

 

函数是无状态的，它们的行为仅依赖于输入参数

- **面向对象编程（OOP）**：对象的状态通常是可变的，这使得在程序中追踪和管理状态变得复杂。你可能需要显式处理对象的状态变化。

- **函数式编程（FP）**：强调不可变性，状态变化通常通过创建新对象或新值来实现，而不直接修改原有的状态。不可变数据的使用使得状态变得更容易跟踪，避免了多次修改数据的副作用。

函数式组件通过 Hooks，将状态和副作用分离，显著提高了代码的简洁性和可读性

**函数式更新**（如 setState((prev) => ...)），确保每次更新基于最新状态。函数式组件每次渲染都会生成一个新的闭包，这个闭包“捕获”了当时的状态值和变量。

每次组件重新渲染时，所有的事件处理函数、useEffect 的回调函数等，都会捕获当前那一刻的状态值，而不是直接操作共享的状态对象。

**react函数式组件是基于快照进行操作，函数式组件每次渲染都会生成一个新的闭包，这个闭包“捕获”了当时的最新状态值和变量。**

**class组件中的所有方法（如事件处理器、componentDidMount 等）都直接操作同一个 this.state 对象（可能是过期值）。由于状态是共享的，全局一致的，异步操作会引发冲突所以函数式编程能解决很多异步操作的冲突问题**



**`this` 指向规则对比表格**

| 场景             | `this` 指向                                     | 示例代码                                                     | 说明                                                     |
| ---------------- | ----------------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| **全局环境**     | 浏览器中指向 `window`，严格模式下为 `undefined` | ```js console.log(this); // window (非严格模式) ```          | 在全局范围，`this` 默认为全局对象（严格模式除外）。      |
| **对象方法调用** | 指向调用方法的对象                              | ```js const obj = { foo() { console.log(this); } }; obj.foo(); // obj ``` | 方法被对象调用时，`this` 指向该对象。                    |
| **构造函数**     | 指向新创建的实例对象                            | ```js function Person() { console.log(this); } new Person(); // 新实例对象 ``` | 使用 `new` 调用时，`this` 指向构造函数的实例对象。       |
| **箭头函数**     | 继承定义时所在上下文的 `this`                   | ```js const arrow = () => console.log(this); arrow(); // 外部上下文的 `this` ``` | 箭头函数不创建自己的 `this`，而是继承定义位置的 `this`。 |
| **显式绑定**     | 指向显式绑定的对象                              | ```js function foo() { console.log(this); } foo.call(obj); // obj ``` | 使用 `call`、`apply` 或 `bind` 时，`this` 指向指定对象。 |
| **事件处理器**   | 浏览器中默认指向事件目标元素                    | ```js button.addEventListener('click', function() { console.log(this); }); ``` | 在事件绑定中，`this` 默认指向事件目标。                  |



JSX是react.createElement的语法糖

```js
<ul className="list">
  <li key="1">1</li>
  <li key="2">2</li>
</ul>

React.createElement(
  "ul",
  {
    // 传入属性键值对
    className: "list",
    // 从第三个入参开始往后，传入的参数都是 children
  },
  React.createElement(
    "li",
    {
      key: "1",
    },
    "1"
  ),
  React.createElement(
    "li",
    {
      key: "2",
    },
    "2"
  )
);
```



**react严格模式**

- **检查不安全的生命周期方法**：会标记那些已被废弃的生命周期方法（如 componentWillMount）。

- **标记意外的副作用**：比如在渲染阶段产生的副作用（如直接修改 DOM）。

- **检测过时的 API**：如字符串 ref（推荐使用 useRef 或回调形式的 ref）。

- **双调用 render 方法**（仅开发模式）：在组件初始化时调用两次 render 方法，确保组件没有副作用。



##### custom hooks

自定义 Hook 不是 React 内置的功能，它只是一个开发者约定的模式，用于复用组件逻辑

这个 useCustomHook 和普通的函数唯一的约定是：名字以 use 开头，并且在内部调用了其他 React Hook（如 useState、useEffect）。

调用不能放在if语句，不能放在for/while中

```react
// ❌ 错误：在条件语句中调用
function MyComponent() {
  if (true) {
    const [count, setCount] = React.useState(0); // Error
  }
}
```



##### react ecosystem



error_boundary

只能用class component

they are not recommended and they are not deprecated. 



React 自动代理了大多数事件，但某些特殊情况需要手动绑定

- 监听 document 或 window 级别的事件（如 keydown、scroll）。

- React 版本不支持的特殊事件（如 onPointerEnter）。





##### 更新函数

根据先前的 state 更新 state

假设 `age` 为 `42`，这个处理函数三次调用 `setAge(age + 1)`

```react
function handleClick() {
  setAge(age + 1); // setAge(42 + 1)
  setAge(age + 1); // setAge(42 + 1)
  setAge(age + 1); // setAge(42 + 1)
}
```

最终都age只是43，因为state是快照，**设置 state 只会为下一次渲染变更 state 的值**，**一个 state 变量的值永远不会在一次渲染的内部发生变化**

为了解决这个问题，**你可以向 `setAge` 传递一个 \*更新函数\***，而不是下一个状态：

```react
function handleClick() {
  setAge(a => a + 1); // setAge(42 => 43)
  setAge(a => a + 1); // setAge(43 => 44)
  setAge(a => a + 1); // setAge(44 => 45)
}
```

这里，`a => a + 1` 是更新函数。它获取 待定状态 并从中计算 下一个状态。



##### useEffect

1. **数据获取（API 请求）**：在组件挂载时发起 HTTP 请求并更新状态来渲染返回的数据。

2.  **事件监听（如滚动、键盘事件）**

   ```react
   import { useEffect } from 'react';
   
   function ScrollListener() {
     useEffect(() => {
       const handleScroll = () => {
         console.log('Scrolled!');
       };
   
       window.addEventListener('scroll', handleScroll);
   
       // 清理函数
       return () => {
         window.removeEventListener('scroll', handleScroll);
       };
     }, []); // 仅在组件挂载和卸载时执行
   
     return <div>Scroll to trigger event.</div>;
   }
   ```

3.  **DOM 操作**

4. **订阅/取消订阅（WebSocket、事件源）**

   ```react
   import { useEffect, useState } from 'react';
   
   function WebSocketComponent() {
     const [message, setMessage] = useState('');
   
     useEffect(() => {
       const socket = new WebSocket('ws://example.com/socket');
   
       socket.onmessage = (event) => {
         setMessage(event.data);
       };
   
       // 清理函数：关闭 WebSocket 连接
       return () => {
         socket.close();
       };
     }, []); // 仅在组件挂载时执行一次
   
     return <div>{message}</div>;
   }
   ```

   



##### useReducer

`useReducer` 是一个 React Hook，它允许你向组件里面添加一个 reducer。

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

#### 参数 

- `reducer`：用于更新 state 的纯函数。参数为 state 和 action，返回值是更新后的 state。state 与 action 可以是任意合法值。
- `initialArg`：用于初始化 state 的任意值。初始值的计算逻辑取决于接下来的 `init` 参数。
- **可选参数** `init`：用于计算初始值的函数。如果存在，使用 `init(initialArg)` 的执行结果作为初始值，否则使用 `initialArg`。

#### 返回值 

`useReducer` 返回一个由两个值组成的数组：

1. 当前的 state。初次渲染时，它是 `init(initialArg)` 或 `initialArg` （如果没有 `init` 函数）。
2. `dispatch` 函数。用于更新 state 并触发组件的重新渲染。



React 会把当前的 state 和这个 action 一起作为参数传给 reducer 函数，然后 reducer 计算并返回新的 state，最后 React 保存新的 state，并使用它渲染组件和更新 UI。

```react
import React, { useReducer } from 'react';

// 定义初始状态
const initialState = { count: 0 };

// 定义 reducer 函数
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    default:
      throw new Error();
  }
}

function Counter() {
  // 使用 useReducer Hook
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}

export default Counter;
```



##### useCallback

`useCallback` 是一个允许你在多次渲染中缓存函数的 React Hook。在组件顶层调用 `useCallback` 以便在多次渲染中缓存函数

**场景**：当你把函数作为 prop 传递给子组件时，使用 useCallback 可以防止子组件不必要的重新渲染，因为函数引用不会发生变化。

```react
const memoizedCallback = useCallback(() => {
  // 你的函数逻辑
}, [dependencies]); // 依赖项变化时才重新创建函数
```



##### useMemo

- **作用**：返回一个 memoized 的值。它会记住计算结果，只有在依赖项发生变化时才会重新计算值。

- **场景**：当你需要计算一个开销较大的值，并且这个值只有在某些依赖项变化时才需要重新计算时，可以使用 useMemo 来优化性能。

```react
const memoizedValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]); // 只有 a 和 b 改变时才重新计算值
```



##### useLayoutEffect

`useLayoutEffect` 可能会影响性能。尽可能使用 [`useEffect`](https://zh-hans.react.dev/reference/react/useEffect)。

主要的区别在于它会在 DOM 更新后、屏幕绘制之前同步执行回调。换句话说，useLayoutEffect 在浏览器绘制之前，**同步**地执行它的副作用操作，而 useEffect 是在浏览器绘制之后异步执行的。

**避免闪烁或布局抖动**：如果某些副作用操作需要在屏幕绘制前完成，避免由于 useEffect 的异步执行导致的闪烁，可以选择 useLayoutEffect。



##### useTransition

`useTransition` 是一个让你可以在后台渲染部分 UI 的 React Hook， 是一个让你可以在后台渲染部分 UI 的 React Hook。

```react
const [isPending, startTransition] = useTransition();
```

`useTransition` 返回一个由两个元素组成的数组：

1. `isPending`，告诉你是否存在待处理的 transition。
2. `startTransition` 函数，你可以使用此方法将更新标记为 transition。



##### useDeferredValue



##### useContext

`useContext` 是一个 React Hook，可以让你读取和订阅组件中的context。

useContext 是 React 中的一个 Hook，用于访问 **Context** 中存储的值。它让我们能够跨越组件树的层级，直接访问共享的状态或数据，避免了通过 props 层层传递数据的麻烦。

Context 分为以下几个部分：

- **React.createContext**：用于创建一个 Context 对象。
- **Context.Provider**：用于在组件树中提供共享的数据。
- **useContext**：用于访问共享的 Context 数据。

```react
import React, { createContext, useState } from 'react';

// 创建一个 Context light是默认值
const ThemeContext = createContext('light');

function App() {
  const [theme, setTheme] = useState('light');

  return (
    // 使用 Provider 提供 Context 值
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <ChildComponent />
    </ThemeContext.Provider>
  );
}
```

```react
import React, { useContext } from 'react';
import { ThemeContext } from './App';

function ChildComponent() {
  // 使用 useContext 获取 Context 的值
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <div>
      <p>Current theme is {theme}</p>
      <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
        Toggle Theme
      </button>
    </div>
  );
}
```

- useContext 会返回当前 Context 的值，它被确定为传递给树中调用组件上方最近的 `SomeContext.Provider` 的 `value`。
- 如果 useContext 没有找到合适的 Provider，它将返回 createContext 时指定的默认值。

***Trick**: `useContext()` 总是在调用它的组件 **上面** 寻找最近的 provider。它向上搜索， **不考虑** 调用 `useContext()` 的组件中的 provider。*



##### useImperativeHandle





### React Fiber 的了解

**React Fiber** 是 React 16 中引入的一种新的协调算法（reconciliation algorithm），旨在提高 React 的性能和可扩展性。

在旧版 React 中，协调（reconciliation）和渲染过程是同步执行的。**当应用需要进行大量更新时（需要耗费大量计算和渲染时间），React 会阻塞 UI，直到所有更新完成**，导致应用在长时间更新时会变得不响应。Fiber 解决了这个问题，通过异步执行更新操作来分解工作

RequestIdeCallback messageChannel

浏览器的主线程分为JS和渲染

**react自顶向下**

React 的渲染过程通常遵循 **自顶向下的执行顺序**。这意味着，当一个组件的状态（state）或属性（props）发生变化时，React 会从根组件（root component）开始，逐层向下渲染子组件，更新每个组件的 UI。

这个过程可以分为以下几个步骤：

1. **触发更新**：当组件的状态或属性发生变化时，React 会触发更新过程。React 会生成一个新的虚拟 DOM，并与现有的虚拟 DOM 进行比较（称为“协调”或 reconciliation），计算出哪些部分的 UI 需要更新。
2. **虚拟 DOM 比较**：React 会对比新旧虚拟 DOM，找出差异，然后根据差异来更新实际的 DOM。这是通过一个算法（Fiber 和其前身）完成的。
3. **从根组件向下更新**：React 会从根组件开始，逐层向下渲染所有的子组件。如果子组件的状态或属性发生变化，React 会再次对比和更新对应的部分。

#### React Fiber特性

1. **分段执行和时间切片（Time Slicing）**：渲染任务被切分成多个小的任务块（称为 Fiber），**每次处理一个小部分的任务，然后暂停**，在下一个渲染周期继续执行。这意味着即使渲染过程需要耗费大量时间，也不会阻塞主线程，用户仍然可以进行交互。
2. **优先级调度（Priority Scheduling）**：React 可以根据任务的重要性和紧急性调整渲染顺序。高优先级任务（如用户交互、动画等）会优先执行，而低优先级任务（如网络请求或非关键 UI 更新）可以延迟执行。
3. **异步渲染（Async Rendering）**：React 可以在处理更新时暂停和恢复渲染，在渲染过程中，React 会检测是否有需要优先响应的任务，如用户输入，滚动等，如果有，这些任务会被立即执行，保证用户体验。



#### React的diff算法

React 的 **diff 算法**（也称为 **reconciliation 算法**）是 React 用来比较两个虚拟 DOM（Virtual DOM）树的差异，并最终更新实际 DOM 的核心算法。

1. **虚拟 DOM 的存在**：React 使用虚拟 DOM 来提高性能，避免每次状态更新时直接操作真实 DOM。虚拟 DOM 是对实际 DOM 的轻量级副本。
2. **最小化 DOM 更新**：每当组件的状态或属性发生变化时，React 会重新生成虚拟 DOM。然后，通过 diff 算法，React 会计算出新的虚拟 DOM 和旧的虚拟 DOM 之间的差异，并只更新需要更改的部分。这样做的好处是减少了对真实 DOM 的频繁操作，提高了性能。

##### 算法核心思想

1. **基于节点类型比较**
   **同类型节点**：如果新旧虚拟 DOM 中的节点类型相同，React 会进行更深层次的比较，检查属性（props）和子节点的差异。
   **不同类型节点**：React 会丢弃旧的节点，并创建新的节点
2. **Component 比较**：React 会比较它们的 **props** 和 **state**，如果发生变化，React 会触发组件的更新生命周期方法来更新组件内部的渲染结果。
3. **子节点的优化**：React 采用 **深度优先遍历** 的策略来比较子节点。当渲染过程中有多个子节点需要更新时，React 会优先比较同级节点，以减少不必要的 DOM 操作
4. **key 值优化**：通过使用 key，React 可以准确识别哪些元素被添加、删除或重新排序，从而避免重新渲染整个列表

##### diff的优化策略

1. 通过 **基于节点类型比较** 来减少不必要的渲染，确保只有发生变化的部分才会更新。
2. 使用 **key 值优化** 列表渲染，避免不必要的 DOM 更新。
3. **组件的优化**，如 shouldComponentUpdate 和 React.memo，避免不必要的 re-render。
4. 使用 **异步渲染**（Fiber）来拆分任务，避免 UI 渲染的卡顿和阻塞。



### React生命周期相关

#### 类组件生命周期函数

1. **Mounting（挂载）**：组件被创建并插入到 DOM 中
2. **Updating（更新）**：组件的 props 或 state 发生变化时
3. **Unmounting（卸载）**：组件被从 DOM 中移除时

##### **Mounting（挂载）阶段**

- **constructor(props)**
- **render()**:
- **componentDidMount()**:

##### **Updating（更新）阶段**

- **shouldComponentUpdate(nextProps, nextState)**
- **getSnapshotBeforeUpdate(prevProps, prevState)**
- **componentDidUpdate(prevProps, prevState, snapshot)**

#####  **Unmounting（卸载）阶段**

- **componentWillUnmount()**

##### **函数组件的生命周期（使用 Hooks）**

- **useState**：管理状态。
- **useEffect**：执行副作用操作，类似于 componentDidMount、componentDidUpdate 和 componentWillUnmount。

**componentWillUnmount**：useEffect 返回一个清理函数，该函数会在组件卸载时执行，相当于 componentWillUnmount。

```react
useEffect(() => {
  return () => {
    console.log("Component unmounted");
  };
}, []);
```



### 首屏加载问题

#### 一般的解决方案

1. **懒加载（Lazy Loading）**

2. **代码分割（Code Splitting）**
   **动态导入**：使用 Webpack 的动态导入（import()）来实现代码分割，Webpack 会自动将不同的代码块拆分成单独的文件，并在需要时加载。

   ```js
   import('./component').then((module) => {
     // Do something with the module
   });
   ```

3. **服务器端渲染（SSR）**

4.  **压缩和优化资源**

   **压缩 JavaScript 和 CSS**：使用 Webpack、Terser 或其他工具压缩代码。

   **优化图片**：使用合适的图片格式（如 WebP）、调整图片大小，使用图像压缩工具。

5. **资源预加载（Preload）**
   通过 <link rel="preload"> 可以在浏览器加载页面时提前加载关键资源，如字体、样式表、脚本等，确保它们在需要时能够快速加载。

   ```html
   <link rel="preload" href="critical.css" as="style" />
   <link rel="preload" href="critical.js" as="script" />
   ```

6. **HTTP/2 和并行请求**
   如果你的服务器支持 HTTP/2，启用 HTTP/2 可以通过一个连接并行加载多个资源，从而减少请求的延迟时间。

7.  **服务端缓存与客户端缓存**

8. **使用 CDN（内容分发网络）**



#### React中的解决方案

1. **代码分割（Code Splitting）**

   **React.lazy + Suspense**：React 提供了 React.lazy 和 Suspense，允许你按需加载组件，只有在组件需要渲染时才加载相应的代码。

   React.lazy 会延迟加载组件，Suspense 用于显示加载状态，直到懒加载的组件加载完成。

   ```react
   import React, { Suspense } from 'react';
   
   const LazyComponent = React.lazy(() => import('./LazyComponent'));
   
   function App() {
     return (
       <Suspense fallback={<div>Loading...</div>}>
         <LazyComponent />
       </Suspense>
     );
   }
   ```

2. **Server-Side Rendering (SSR)**：浏览器可以直接渲染页面，不需要等 JavaScript 加载和执行后才显示内容。

3. **静态页面生成（Static Site Generation, SSG）**：静态页面在**构建时就生成**了 HTML 文件，这样页面加载时不需要任何后端渲染，极大提高了性能。

4. **前端缓存优化**
   **Service Worker**：使用 Service Worker 缓存静态资源，可以避免每次访问都重新加载资源，提升首屏加载速度。



### SSR

**原理**：

1. **用户发起请求**：浏览器向服务器发起请求，获取页面内容。
2. **服务器渲染 React 组件**：服务器根据请求的数据和路由，使用 React 和 ReactDOMServer 在服务器端渲染页面。
    ReactDOMServer.renderToString() 或 ReactDOMServer.renderToStaticMarkup()：React 会根据应用组件渲染成 HTML 字符串，而不是仅仅返回 JavaScript 代码
3. **返回 HTML 页面**
4. **客户端复水（Hydration）**：当浏览器加载并渲染 HTML 后，React 会接管这个页面，使用客户端 JavaScript 将 React 应用挂载到页面上，恢复组件的状态和事件监听器。



### 组件通信

#### 子组件向父组件通信

1. **通过 Props 传递回调函数（常见）**

   父组件通过 **回调函数** 让子组件传数据。

   ```js
   function Child({ sendDataToParent }) {
     const handleClick = () => {
       sendDataToParent("Hello from Child!");
     };
   
     return <button onClick={handleClick}>Send Data</button>;
   }
   
   function Parent() {
     const handleReceiveData = (data) => {
       console.log("Received from child:", data);
     };
   
     return <Child sendDataToParent={handleReceiveData} />;
   }
   ```

2. **使用 useRef 获取子组件的方法**
   useImperativeHandle **配合 forwardRef 让父组件访问子组件的某些方法**。

   **适用于** focus()、reset()、play() 之类的方法调用，而不是用于管理 React 组件的状态。

   **避免直接暴露子组件的 DOM 或状态**，只提供必要的 API。

   从 React 19 开始， `ref` 可作为 prop 使用。在 React 18 及更早版本中，需要通过 `forwardRef` 来获取 `ref`。

   ```react
   const Counter = forwardRef((props, ref) => {
     const [count, setCount] = React.useState(0);
   
     useImperativeHandle(ref, () => ({
       reset: () => setCount(0),
     }));
   
     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={() => setCount(count + 1)}>Increment</button>
       </div>
     );
   });
   
   function Parent() {
     const counterRef = useRef(null);
   
     return (
       <div>
         <Counter ref={counterRef} />
         <button onClick={() => counterRef.current.reset()}>Reset Counter</button>
       </div>
     );
   }
   ```

3. **使用 Context 进行全局状态管理**

   ```react
   const DataContext = React.createContext();
   
   function Child() {
     const { data, updateData } = React.useContext(DataContext);
     return (
       <div>
         <p>Data from Parent: {data}</p>
         <button onClick={() => updateData("Updated Data")}>Update Parent</button>
       </div>
     );
   }
   
   function Parent() {
     const [data, setData] = React.useState("Initial Data");
   
     return (
       <DataContext.Provider value={{ data, updateData: setData }}>
         <Child />
       </DataContext.Provider>
     );
   }
   ```

4. **使用 Redux / Zustand / Recoil 等全局状态管理**

   

5.  **事件总线（Event Emitter）**

   **事件总线（Event Bus）** 是一种**发布-订阅模式（Pub-Sub）** 的实现，它允许不同的组件或模块之间进行**解耦通信**，特别适用于没有直接父子关系的组件之间的数据传递。

   ```js
   class EventEmitter {
     constructor() {
       this.events = {}; // 存储事件
     }
   
     // 监听事件
     on(event, listener) {
       if (!this.events[event]) {
         this.events[event] = [];
       }
       this.events[event].push(listener);
     }
   
     // 触发事件
     emit(event, ...args) {
       if (this.events[event]) {
         this.events[event].forEach(listener => listener(...args));
       }
     }
   
     // 取消监听
     off(event, listener) {
       if (this.events[event]) {
         this.events[event] = this.events[event].filter(l => l !== listener);
       }
     }
   }
   ```

   **1️⃣ 创建事件总线（eventBus.js）**

   ```js
   import EventEmitter from "./EventEmitter"; // 引入手写的 EventEmitter
   
   const eventBus = new EventEmitter();
   export default eventBus;
   ```

   **2️⃣ 在组件 A 中发送事件**

   ```js
   import eventBus from "./eventBus";
   
   function ComponentA() {
     const sendMessage = () => {
       eventBus.emit("update", "Data from Component A");
     };
   
     return <button onClick={sendMessage}>Send Event</button>;
   }
   
   export default ComponentA;
   ```

   **3️⃣ 在组件 B 中接收事件**

   ```js
   import { useEffect, useState } from "react";
   import eventBus from "./eventBus";
   
   function ComponentB() {
     const [message, setMessage] = useState("");
   
     useEffect(() => {
       eventBus.on("update", setMessage);
   
       return () => {
         eventBus.off("update", setMessage); // 组件卸载时移除监听
       };
     }, []);
   
     return <div>Received: {message}</div>;
   }
   
   export default ComponentB;
   ```

   



### React Router







Redux

React Router

高阶组件（HOC）

Render Props 模式

受控组件 vs 非受控组件

React 18 的并发模式（Concurrent Rendering）







在 JavaScript 中，执行上下文和执行栈是什么

 手撕：已知级联组件的下拉菜单列表结构，输入一个值，找出其对应的value值以及对应的所有父节点value
