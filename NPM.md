#### NPM(node package manager)

CI/CD 持续集成（Continuous Integration）、持续交付（Continuous Delivery）、或持续部署（Continuous Deployment）

开发者提交代码到 Git 仓库 ---> CI 工具（如 Jenkins、GitHub Actions、GitLab CI）触发构建 ---> 自动运行测试，生成构建结果

**持续交付**：部署是“可选”的。

**持续部署**：部署是“自动”的。



@media 

```css
@media (条件) {
  /* CSS 规则 */
}
```

响应式布局(responsitive design)

1、fluid grid layouts流式布局：使用百分比或 em 作为单位，而不是固定像素（px）

2、弹性布局**Flexible Images**：根据父组件的大小展示

```css
img {
  max-width: 100%;
  height: auto;
}
```

3、media query 为不同屏幕尺寸定义不同的样式

响应式设计注意优先移动端(media first)

```css
/* 默认小屏样式 */
body {
  font-size: 14px;
}

/* 大屏样式 */
@media (min-width: 900px) {
  body {
    font-size: 16px;
  }
}
```

