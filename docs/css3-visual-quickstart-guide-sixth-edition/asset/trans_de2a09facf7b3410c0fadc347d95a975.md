

提示 你可以将动态伪类 :hover、:active 和 :focus 应用于任何元素，而不仅仅是链接。

提示 常规锚链接样式会被不同状态及其之间的状态继承。例如，你为 :link 外观设置的字体，将被 :active、:visited 和 :hover 状态继承。

提示 Web 是一种超文本媒介，因此使用户能够区分文本、链接和已访问链接非常重要。因为用户并不总是开启“下划线链接”选项，所以为每个文档设置链接外观是个好主意。

提示 如果使用过多颜色，访问者可能无法分辨哪些词是链接，哪些不是。

提示 本示例中，链接样式是为整个页面设置的，但链接可用于多种用途。例如，链接可用于全局导航、文章标题列表，甚至作为动态控件。因此，根据链接的用途设置样式是个好主意：

```
nav a {...}
nav a:link {...}
nav a:visited {...}
```

提示 前面的样式仅应用于导航元素中的链接。

## 交互样式

加载后，网页远非静态。用户会立即开始与页面交互，在屏幕上移动指针并随处点击。动态伪类允许你在用户与元素交互时对其进行样式设置，从而提供视觉反馈：

- :hover—与链接相同，但设置指针悬停在元素上时的外观。
- :focus—应用于可接收焦点的元素，例如表单文本字段。
- :active—与链接相同，但设置元素被单击或选中时的样式。

## 定义动态伪类：

- 1. 设置默认元素的样式。
  `input {...}`
  虽然可选，但通常为接收动态样式的元素设置默认非动态样式是个好主意（代码 4.7）。

- 2. 设置元素悬停状态的样式。
  输入选择器（HTML、类或 ID）、冒号 (:)，然后是 hover。
  `input:hover {...}`
  只要指针进入元素的框（关于盒模型的详细信息见第 10 章），样式更改就会发生。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Alice&rsquo;s Adventures in Wonderland</title>
  <style type="text/css" media="all">
  input {
    border: 3px solid gray;
    background-color: silver;
    color: gray;
    padding: 0 5px;
    font-size: 1.5em; }
  input[type="button"] {
    border-radius: 1em;
    color: silver;
    background-color: gray; }
  input:hover {
    background-color: white;
    border-color: pink;
    color: silver; }
  input:focus {
    border-color: red;
    background-color: white;
    color: black;
    outline: none; }
  input:active {
    color: red;
    border-color: pink;
    background-color: silver; }
  </style>
</head>
<body>
  <footer>
    <label>Mailing list:</label>
    <input type="text" value="email"
      placeholder="enter your email">
    <input type="button" class="active"
      value="submit">
  </footer>
</body>
</html>
```

## 默认

Mailing List: email submit

## 悬停

Mailing List: email submit

## 激活

Mailing List: email submit

## 焦点

Mailing List: email submit

代码 4.7 的结果。这展示了简单表单字段的四种动态状态。提供这种视觉反馈可以帮助用户知道哪个表单字段可供使用，或者他们是否单击了按钮。

> 提示 更改 :hover 的某些属性时建议谨慎。更改字体系列、字体大小、粗细等属性可能会导致文本大小超出布局中为其预留的空间，并迫使整个页面重新排列内容，这会真正惹恼访问者。

> 提示 本示例使用 input 来展示动态状态。input 的一个样式缺点是所有输入类型都使用相同的标签。本章后面你将看到如何使用标签属性来设置样式，这将允许你为文本字段和按钮设置不同的样式。

- 3. 设置元素焦点状态的样式。输入选择器（HTML、类或 ID）、冒号 (:)，然后是 focus。
  `input:focus {...}`
  只要元素获得焦点（被单击或通过 Tab 键定位到），样式更改就会发生，然后在元素失去焦点（称为 blur）时恢复为悬停或默认样式。

- 4. 设置元素激活状态的样式。输入选择器（HTML、类或 ID）、冒号 (:)，然后是 active。
  `input:active {...}`
  只要用户在元素框内单击（在第 10 章中解释），样式更改就会发生，然后在释放时恢复为悬停或默认样式。

- 5. 样式会根据用户的反应必要地应用于元素的状态。
  `<input type="button" value="Submit">`
  使用特定选择器的所有标签都将对其状态进行样式设置。

> 提示 定义链接和动态伪类的顺序很重要。例如，将 :hover 伪类放在 :visited 伪类之前，会导致链接被访问后 :hover 不再工作。为获得最佳效果，请按以下顺序定义样式：link、visited、hover、focus、active。

> 提示 记住伪元素顺序的一种方法是使用助记符 LoVe HAte：Link Visited Hover Active。

> 提示 如果你设置了 :hover，则应始终设置 :focus。为什么？悬停仅应用于元素的非键盘（鼠标）交互。对于仅使用键盘的 Web 用户，:focus 将适用。

## ★使用伪类设置特定子元素的样式

设计师通常希望将样式应用于在另一个元素中首先出现的元素，例如父元素的第一个子元素。

first-child 伪元素自 CSS2 起即可用；然而，CSS3 提供了一系列新的结构伪元素，用于精确设置元素子元素的样式（表 4.4）：

- :first-child—如果选择器类型是父元素的第一个子元素，则设置其首次出现时的外观。
- :first-of-type—设置选择器类型在父元素中首次出现时的元素外观。
- :nth-child(#)—设置指定子元素特定出现次数的外观。例如，段落的第三个子元素将是 p:nth-child(3)。
- :nth-of-type(#)—设置选择器类型在父元素中特定出现次数的外观。例如，第七个段落将是 p:nth-of-type(7)。
- :nth-last-of-type(#)—设置选择器类型在父元素中特定出现次数的外观，但从底部开始计算。例如，从底部算起的第三个段落将是 p:nth-last-of-type(3)。
- :last-child—如果指定选择器类型的元素是父元素的最后一个子元素，则设置其外观。
- :last-of-type—设置特定选择器类型在其父元素中最后一次出现时的外观。

## 文本装饰：下划线还是不加下划线

下划线是 Web 上指示超文本链接的标准方式。然而，过多带下划线的链接会使页面变成一团难以穿透的线条，文本变得难以阅读。此外，如果访问者关闭了下划线，他们将无法看到链接，尤其是当链接和文本颜色相同时。

CSS 允许你关闭链接的下划线，从而覆盖访问者的偏好。我推荐这种做法，并倾向于依靠清晰的颜色选择来突出超文本链接，或依靠 border-bottom 这种替代下划线方法，它能让你更好地控制下划线的样式。有关更多信息，请参见第 14 章。

