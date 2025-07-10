### CSS

渐变border实现原理：

首先实现一个渐变的背景作为底板，然后在这个底板上加上一个仅有content大小纯色背景

实际上使用background-clip实现

accent-color 是一种 CSS 属性，用于设置表单控件（如复选框、单选框、进度条等）的主题色，



### 跳动的按钮

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      keyframes: {
        pulseBounce: {
          '0%, 100%': { transform: 'scale(1)' },
          '50%': { transform: 'scale(1.15)' },
        },
      },
      animation: {
        pulseBounce: 'pulseBounce 1s ease-in-out infinite',
      },
    },
  },
}
```

```html
<button class="bg-blue-500 text-white px-4 py-2 rounded animate-pulseBounce">
  Click Me
</button>
```

1. 在tailwind.config.js中将**自定义动画**及**关键帧**配置好

2. ```js
   module.exports = {
     theme: {
       extend: {
         // 自定义样式
       }
     }
   }
   ```

   - Module.exports = {} 这是node.js的导出语法
   - theme在tailwindcss的配置文件结构中表示主题设置，是**tailwind预设的配置入口**
   - extend是tailwind的约定属性，表示在不覆盖默认配置的前提下添加自己的配置项

3. extend.keyframes

   - pulseBounce 是你自定义动画的**名字**
   - 内部是一个 @keyframes 动画的关键帧定义
   - '0%, 100%'：表示动画开始和结束时，缩放为正常大小（1倍）
   - '50%'：动画进行到一半时，缩放为 1.15 倍

3.  Extend.animation

   - pulseBounce 是你给这个动画起的名字（将来你用 animate-pulseBounce 就可以了）

   - 'pulseBounce 1s ease-in-out infinite' 是 Tailwind 会生成的 CSS：

   - ```css
     animation-name: pulseBounce;
     animation-duration: 1s;
     animation-timing-function: ease-in-out;
     animation-iteration-count: infinite;
     ```

     
