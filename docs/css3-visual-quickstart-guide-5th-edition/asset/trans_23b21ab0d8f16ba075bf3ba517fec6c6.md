

## Firefox 的 Firebug

Firefox 的 Firebug 插件工具已成为全球 Web 设计师的事实标准。你可以从 Firefox 附加组件网站或直接从 Firebug 网站 getfirebug.com（Win/Mac）获取它。

## 开始使用 Firebug

- 1. 打开 Firebug 面板。导航到你想要查看的网页，然后点击浏览器窗口右下角的 Firebug 图标，或选择 Firebug。

![](img/9cd61ac1d4015ed5688d0c411434a660_400_0.png)

- 2. 查看 CSS。你可以点击 CSS 标签页单独查看 CSS，也可以通过点击 HTML 标签页与 HTML 并排查看。我通常在并排模式下工作。

- 3. 检查元素。点击“检查”（Inspect）按钮，然后点击屏幕上你想要检查的元素。当你悬停在某个元素上时，它的框框将用带有颜色标记的外边距（margins）和内边距（padding）勾勒出来。Firebug 会在 HTML 代码中突出该元素，并显示所有应用的 CSS。如果声明被其他声明覆盖且未应用，则声明会被划掉。点击选择一个元素进行编辑。

- 4. 关闭一个声明。悬停在声明中属性名的左侧，会出现一个*否*（not）符号 🚫。点击它关闭该属性，再次点击它开启该属性。在视口中，你应该能立即看到属性属性开启和关闭的效果。

- 5. 编辑声明。双击属性名或值，即可输入新值。随着你的输入，任何更改的效果都几乎会立即可见。

- 6. 添加新声明。双击你想在你新声明之前的某个声明右侧的空白处，输入属性名，按下 Tab 键，然后输入属性值。不要输入结束分号（;）。更改应该会在你输入时立即出现。

## Safari 和 Chrome 中的 Web Inspector

Safari 和 Chrome 都拥有这种 Web 开发者工具，它允许你快速分析和编辑你的 CSS 和 HTML。Safari 和 Chrome 均适用于 Windows 和 Mac OS X：
www.apple.com/safari (Win/Mac)
www.google.com/chrome (Win/Mac)。

## 开始使用 Web Inspector

- 1. 在 Safari 中开启开发者菜单。打开浏览器的偏好设置（Safari>偏好...），选择高级标签卡，并勾选“菜单栏中的开发菜单”。

![](img/9cd61ac1d4015ed5688d0c411434a660_402_0.png)

任何书都可以解释如何编写 CSS 代码，但你并不是用抽象代码交流。你谈论的是颜色、形状以及：

```html
<html href="http://www.example.org/html">
<head href="http://www.example.org/head">
</head>
<div id="container">
  <img src="http://www.example.org/logo.png" />
  <div class="flags">
  <div class="flags">
  <div class="flags"></div>
  <script src="http://www.google-analytics.com/analytics.js" type="javascript/javascript"></script>
  <div class="flags">
  <div id="footer" style="display:none;"></div
  <div id="sidebar" style="display:none;"></div
</div
</html>
```

![](img/9cd61ac1d4015ed5688d0c411434a660_402_1.png)

### 检查元素标签 (Inspect Elements)
Safari 中的 Web Inspector。它在 Chrome 中看起来几乎一样。

- 2. 打开 Web Inspector 面板。导航到你想要查看的网页，在 Safari 中选择开发>Web Inspector，或在 Chrome 中选择查看>开发者>开发者工具。

- 3. 查看 CSS。你可以点击 Elements 标签页与 HTML 并排查看 CSS。

- 4. 检查元素。点击检查图标（放大镜），然后点击屏幕上你想要检查的元素。当你悬停在某个元素上时，它的框框将被勾勒出来，并带有颜色标记的外边距和内边距。Firebug 会在 HTML 代码中突出该元素，并显示所有应用的 CSS。声明被划掉以表示它们已被其他声明覆盖且未应用。点击选择一个元素进行编辑。

- 5. 关闭一个声明。悬停在 CSS 中的声明上，每个声明右侧都会出现一个复选框。取消勾选复选框以关闭声明。勾选复选框以开启。在视口中，你应该立即看到声明开启和关闭的效果。

- 6. 编辑声明。双击你想更改声明并根据需要进行编辑。随着你的输入，任何更改的效果都几乎会立即可见。

- 7. 添加新声明。双击你想在你新声明之前的某个声明右侧的空白处，输入属性名，然后输入属性值。不要输入结束分号（;）。按下回键使更改生效。

> 请记住，如果在任何时候重新加载页面，你所做的任何更改都会丢失。

## 验证你的 CSS

W3C 提供了一个工具来检查你的 CSS 是否符合标准：

- 1. 转到 W3C 验证器 (www.w3.org/validator/)。
- 2. 输入页面 URL 或粘贴你的 CSS 代码。
- 3. 报告将显示代码中的任何错误或警告。
- 4. 利用这些信息修复问题并确保你的 CSS 是有效的。

使用这些工具可以帮助你编写更整洁的代码，并确保你的网站在不同的浏览器中正常工作。

