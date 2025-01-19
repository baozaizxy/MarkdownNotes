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

 
