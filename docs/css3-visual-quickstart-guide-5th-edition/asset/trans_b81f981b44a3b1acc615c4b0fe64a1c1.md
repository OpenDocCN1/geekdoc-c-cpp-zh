

## 4.10 如果元素是一个没有使用 dialog 类的段落，它将以红色和斜体显示

## CSS3 新特性：不对元素设置样式

到目前为止，你已经了解了当标签满足某些条件时如何对它设置样式。否定选择器 `:not()` 允许你针对特定的选择器不对某些元素设置样式。

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type"
    content="text/html; charset=UTF-8" />
  <title>爱丽丝漫游仙境</title>
  <style type="text/css" media="all">
    p:not(:dialog) {
      color: red;
      font-style: italic;
    }
  </style>
</head>
<body>
  <p class="dialog">“为什么？”毛毛
 虫说道。</p>
  <p>这是另一个奇怪的问题...</p>
  <p class="dialog">“回来！”毛毛
- 虫...</p>
</body>
</html>
```

```## 若要不为特定元素设置样式：

- 1. 设置元素样式以排除某些选择器。输入你想要样化的元素选择器（HTML、类或 ID）、一个冒号 (:)、`:not()`，然后在括号中输入你想要从该规则中排除的选择器（见代码 4.10）。

```css
p:not(.dialog) {...}
```

- 2. 如果元素包含指定的选择器，则该元素不会被设置样式。

`<p class='dialog'>...</p>`

`<p>...</p>`

样式将应用于匹配初始选择器但不匹配括号内选择器的元素上。

> “为什么？”毛毛虫说道。

> 这是另一个奇怪的问题；由于爱丽丝想不出任何合理的理由，而且毛毛虫似乎正处于一种*非常*不悦的心绪中，她转身离开了。

“回来！”毛毛虫在她身后喊道，“我有重要的话要说！”

代码 4.10 的结果显示，使用 dialog 类的段落没有获得该样式。

## 使用伪元素

伪元素是元素中一个特定且独特的部分——例如段落的首字母或第一行——它可以独立于元素的其余部分进行样式设置。（其他伪元素的列表，请参见表 4.5。）

## 处理首字母和首行

你可以直接使用 **:first-letter** 伪元素访问任何文本块的首字母。可以使用 **:first-line** 伪元素将任何文本块的第一行孤离开来进行样式处理。

## 若要高亮显示文章的开头：

- 1. 设置元素的默认版本。
```css
article p {...}
```
虽然不是强制的，但通常情况下，为你将设置**:first-letter** 伪元素的选择器设置默认样式是一个好主意（见代码 4.11）。

表 4.5 伪元素
| 格式 | 名称 | 满足什么条件时设置样式 | 兼容性 |
| :--- | :--- | :--- | :--- |
| first-letter, ::first-letter | 首字母 | 文本中的第一个字母 | IE5.5, FF1, O3.5, S1, CSS1 |
| first-line, ::first-line | 文本的第一行 | 它们是文本的第一行 | IE5.5, FF1, O3.5, S1, CSS1 |
| ::after, ::after | 之后 | 元素紧前的空间 | IE8, FF1, O5, S1, CSS2 |
| ::before, ::before | 之前 | 元素紧后的空间 | IE8, FF1, O5, S1, CSS2 |

![](img/9cd61ac1d4015ed5688d0c411434a660_115_0.png)

## 4.11 文章中段落的首字母和首行设置了样式 Ⓑ

- 2. 如果元素的首字母是同类型中的第一个，则对其首字母设置样式。输入你想要设置首字母的选择器（article p）、一个冒号 (:)，然后是 `:first-letter`。

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type"
  content="text/html; charset=UTF-8" />
  <title>标题</title>
  <style type="text/css" media="all">
  article p {
    font-size: 16px;
    line-height: 24px;
    color: rgb(102,102,102);
  }
  article p:first-of-type:first-letter {
    color: red;
    font-size: 3em;
    float: left;
  }
  article p:first-of-type:first-line {
    font-size: 1.2em;
    font-weight: bold;
    color: rgb(0,0,0);
  }
</style>
</head>
<body>
<article>
<p>爱丽丝漫游仙境</p>
<p>这是另一个奇怪的问题...</p>
</article>
</body>
</html>
```

