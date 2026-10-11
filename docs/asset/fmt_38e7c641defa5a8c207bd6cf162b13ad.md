
如果你只想设置父元素的子元素（而不是孙元素后代），必须指定父选择器和子元素选择器，它们之间用闭角括号 (`>`) 隔开。

```
copy > em { color: red; }
```

大于号

直接子元素选择器的通用语法。

## 定义子元素选择器：

- 1. 建立直接子元素选择器列表。输入父元素的选择器（HTML、类或 ID），后跟一个右角括号 (`>`），然后是子元素选择器（HTML、类或 ID）。

`article.copy > p > em {...}`

你可以根据需要重复此操作，最终的选择器是你要应用样式的目标（见代码 4.3）。在选择器和大于号之间可以有一个空格，也可以不留空格。

- 2. 如果匹配模式，则将使用样式。

`<article class="copy"><p>...<em>...</em></p></article>`

当且仅当最终选择器是嵌套在前一个元素直接子元素时，步骤 1 中的样式才会生效。将标签放在任何其他 HTML 标签内都会破坏该模式。

- 3. 只有当 `<em>` 标签是 `<p>` 的子元素，且 `<p>` 又是使用 `copy` 类的 `<article>` 的子元素时，样式才会应用于该 `<em>` 标签。

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <title>爱丽丝仙游游</title>
  <style type="text/css" media="all">
  article.copy p > em {
    color: red;
    font-weight: bold;
  }
</style>
</head>
<body class="copy">
  <h1>爱丽丝在<em>仙游境</em>中的奇游</h1>
  <h2>第二章 泪之池</h2>
  <p>'真奇怪，太奇怪了！’<em>爱丽丝喊道</em>……</p>
  <p>她继续<em>计划</em>……</p>
  <p>可怜的<em>爱丽丝</em>！</p>
  <blockquote>
    <p><em>爱丽丝的右脚，</em> <em>女士</em></p>
    <p>“噢天呐，我都在些什么<em>胡话</em>啊！’……</p>
  </blockquote>
</article>
</body>
</html>
```

![](img/9cd61ac1d4015ed5688d0c411434a660_98_0.png)

## 第二章 泪之池

“真奇怪，太奇怪了！”爱丽丝喊道……

她继续计划……

可怜的爱丽丝！

爱丽丝的右脚，女士

“噢天呐，我都在些什么胡话啊！”……

> 代码 4.3 的结果。红色文本符合直接子元素标准。在这种情况下，`<em>` 标签在段落内匹配，但在标题内不匹配。

![](img/9cd61ac1d4015ed5688d0c411434a660_99_0.png)

## 4.4 只有当 `<em>` 标签位于紧跟另一个段落的段落中时，样式才会应用于该标签

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <title>爱丽丝仙游游</title>
  <style type="text/css" media="all">
p + p {
  color: red;
  font-weight: bold;
}
</style>
</head>
<body>
  <article class="copy">
    <h1>爱丽丝在<em>仙游境</em>中的奇游</h1>
    <h2>第二章 <em>泪之池</em></h2>
    <p><em>真奇怪，太奇怪了！</em> <em>爱丽丝喊道</em>……</p>
    <p>她继续<em>计划</em>……</p>
    <p>可怜的<em>爱丽丝</em></p>
    <blockquote>
      爱丽丝的右脚，<em>女士</em>
      <p>“噢天呐，我都在些什么<em>胡话</em>啊！……”</p>
    </blockquote>
  </article>
</body>
</html>
```

![](img/9cd61ac1d4015ed5688d0c411434a660_100_0.png)

## 选择性样式设置

### 定义兄弟元素选择器：

- 1. 建立一个通用兄弟元素选择器列表。输入第一个兄弟元素的选择器（HTML、类或 ID）、一个波浪号 (`~`)，然后是另一个选择器（HTML、类或 ID）（见代码 4.5）。

```css
p ~ p { color: red; }
```

- 2. 如果匹配模式，则将使用样式。

```css
<p>...</p><p>...</p><blockquote><p>...</p></</blockquote>>
```

| 表格 4.2 通用选择器 | 格式 | 满足以下条件应用样式 |

| :--- | :--- | :--- |

| a * | b | 无论 b 的父元素如何，均在 a 内部 |

| a ~ b | b | b 是紧跟在 a 之后的任何元素的兄弟元素 |

| *:hover | 任何元素 | 鼠标指针悬停在元素上 |

| *:disabled | 任何元素 | 禁用状态 |

| *:first-child | 任何元素的第一个子元素 |

| *:lang() | 任何元素 | 使用指定的语言 |

| *:not(s) | 任何元素 | 未使用指定的选择器 |

| *:first-letter | 任何元素的第一个字母 |

> 样式将应用于出现在第一个选择器之后的所有兄弟元素，而不仅仅是第一个，而是直到遇到另一种类型的元素为止的任何同类型兄弟元素。IE 不支持子兄弟选择器，因此您需要单独为这些元素设置样式。更多信息请参见第 1 章。

> 虽然本节所示的通用选择器与组合选择器一起使用，但它也可以与任何选择器配合。

## 4.5 只有当 `<em>` 标签位于带有任何前置兄弟元素的段落中时，样式才会应用于该标签

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <title>爱丽丝仙游游</title>
  <style type="text/css" media="all">
p + p {
    color: red;
    font-weight: bold;
  }
</style>
</head>
<body class="copy">
  <h1>爱丽丝在<em>仙游境</em>中的奇游</h1>
  <h2>第二章 泪之池</h2>
  <p>'真奇怪，太奇怪了！’<em>爱丽丝喊道</em>……</p>
  <p>她继续<em>计划</em>……</p>
  <p>可怜的<em>爱丽丝</em>！</p>
  <blockquote>
    <p><em>爱丽丝的右脚，</em> <em>女士</em></p>
    <p>“噢天呐，我都在些什么<em>胡话</em>啊！”……</p>
  </blockquote>
</article>
</body>
</html>
```

# 链接样式设置

尽管链接是一个标签，但它的各个状态并不是。要为这些状态设置属性，你必须使用与链接可能拥有的每个状态相关的伪类（按此顺序）：

- `:link` 允许你声明尚未被选择的超文本链接的外观。

- `:visited` 允许你设置访问者之前选择过的链接的外观——即标签中 `href` 属性的 URL 是浏览器历史记录的一部分。

- `:hover` 允许你设置当访问者的指针悬停在元素上时元素的外观。

- `:active` 设置元素在被访问者点击或选中时的样式。

关于用于链接的样式的建议，请参见侧边栏的“选择链接样式”。

### 设置对比明显的链接外观：

1. 样式化锚点标签（anchor tag）。

```
{{...}
```

虽然不是强制性的，但最好先定义通用的锚点样式（代码 4.6）。这与设置 `:link` 伪类的不同之处在于，这些样式应用于所有的链接伪类。因此，你想要声明任何保持不变或仅在一种状态下更改的样式。

# 第 1 章 掉进兔子洞

# 第 2 章 泪水池 — 链接

# 第 3 章 召开会赛与长故事

# 第 4 章 兔子送来 — 小比尔中的悬停

# 第 5 章 来自毛虫的建议 — 激活

# 第 6 章 猪与胡椒

# 第 7 章 疯狂茶茶会

# 第 8 章 皇后的地鼠球场

# 第 9 章 呆甲龟的故事

# 第 10 章 龙虾舞曲

# 第 11 章 谁偷了饼干？

# 第 12 章 爱丽丝的证词

> 代码 4.6 的结果显示了为每个状态设置的样式，帮助用户理解正在发生什么。

## 代码 4.6 为默认状态以及所有四个链接状态设置了样式，创建了颜色区分 B。请注意，我通过 `text-decoration` 关闭了下划线，但使用 `border-bottom` 添加了下划线效果。

```html
<!-- HTML5 -->
<!DOCTYPE html>
<html lang="en">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<title>爱丽丝在仙仙游</title>
<style type="text/css" media="all">
 a {
  display: block;
  text-decoration: none;
  padding: 5px;
  width: 200px; }
a:link {
  color: rgb(255,102,102);
  border-bottom: 1px dotted rgb(255,51,51);
}
a:visited {
  color: rgb(255,153,153);
  border-bottom: 1px dotted rgb(255,235,235);
}
a:hover {
  color: rgb(255,0,0);
  border-bottom: 1px solid rgb(255,0,0);
}
a:active {
  color: rgb(0,0,255);
  border-bottom: 1px dotted rgb(102,102,102); }
</style>
</head>
<body>
<navigation>
<a href=""><<strong>第 1 章. </strong>掉进兔子洞</a>
<a href=""><<strong>第 2 章. </strong>泪水池</a>
<a href=""><<strong>第 3 章. </strong>召开会赛与长故事</a>
<a href=""><<strong>第 4 章. </strong>兔子送来的小比尔中</a>
<a href=""><<strong>第 5 章. </strong>来自毛虫的建议</a>
<a href=""><<strong>第 6 章. </strong>猪与胡椒</a>
<a href=""><<strong>第 7 章. </strong>疯狂茶茶会</a>
<a href=""><<strong>第 8 章. </strong>皇后的地鼠球场</a>
<a href=""><<strong>第 9 章. </strong>呆甲龟的故事</a>
<a href=""><<strong>第 10 章. </strong>龙虾舞曲</a>
<a href=""><<strong>第 11 章. </strong>谁偷了饼干？</a>
<a href=""><<strong>第 12 章. </strong>爱丽丝的证词</a>
</navigation>
</body>
</html>
```

2. 样式化默认链接状态。输入你想要元素的元素选择器（锚点标签、类或 ID），后跟一个冒号 (`:`），然后是 `link`。

```
a:link {......}
```

你可以覆盖为锚点标签设置的样式，但此规则应位于 `:visited` 伪类之前。

3. 样式化访问过的链接状态。输入你想要元素的元素选择器（锚点标签、类或 ID），后跟一个冒号 (`:`），然后是 `visited`。

```
a:visited {...}
```

4. 样式化悬停链接状态。输入你想要元素的元素选择器（锚、类或 ID），后跟一个冒号 (`:`），然后是 `hover`。

```
a:hover {...}
```

5. 样式化激活链接状态。输入你想要元素的元素选择器（锚、类或 ID），后跟一个冒号 (`:`），然后是 `active`。

```
a:active {...}
```

6. 样式化元素状态。使用 `text-decoration`。

### 用于链接的样式。

大多数浏览器默认设置链接的颜色。

### 链接的交互。

链接可以设置不同的样式。

![](img/9cd61ac1d4015ed5688d0c411434a660_110_0.png)

# 3. 样式元素的聚焦状态（focus state）。

输入选择器（HTML、类或 ID），

冒号（:），然后输入 focus。

```
input: {...}
```

一旦元素获得焦点

（被点击或轻触），样式就会发生变化，并在元素

失去焦点（称为 blur/模糊）时，样式会恢复到

悬停（hover）或默认样式。

C: 代码 4.7 的结果。这展示了处于四种动态状态下的简单表单。提供这种视觉反馈可以帮助用户知道哪个表单字段已准备就绪，或者他们已经点击了按钮。

# 4. 样式元素的激活状态（active state）。

输入选择器（HTML、类或 ID），

冒号（:），然后输入 active。

```
input:active {...}
```

当用户在元素框内点击时（在第 10 章中解释）

# 5. 样式会根据用户的反应，在必要时应用于元素的

状态。

```
<input type="button"
value="Search">
```

所有使用特定选择器的标签都对其状态进行了样式设置。

> 提示：定义链接和伪类的顺序是有区别的。例如，将 :hover 伪类放在 :visited 伪类之前，会导致链接在被访问后 :hover 无法工作。为了获得最佳效果，请按此顺序定义样式：link（链接）、visited（已访问）、focus（聚焦）和 active（激活）。

> 提示：在更改 :hover 的 s 属性时要谨慎。更改类型、字体大小、字重和其他属性会导致文本比其在布局中保留的空间变大或变小，并强制整个页面重新填充内容，这会非常困扰访问者。

> 提示：在这个示例中，使用 `input` 来显示动态状态。`input` 有一个样式缺点，即所有 input 类型都……在本章的稍后部分，你将看到如何使用标签属性设置样式，这将允许你为文本字段和按钮设置不同的样式。

> 提示：记住伪元素顺序的一种方法是 me LoVe HaTe：Link（链接）、Visited（已访问）、Hover（悬停）、Active（激活）。

> 提示：如果你设置了 :hover，你总是想要设置 :focus。为什么？Hover 仅适用于与元素的非键盘（鼠标）交互。对于仅使用键盘的 Web 用户，:focus 将生效。

# 新 CSS3：使用伪类为特定子元素设置样式 ★

设计师通常希望对另一个元素内部第一个出现的元素应用样式，例如父元素的第一个孩子。

`first-child` 伪元素自 CSS2.22 起已可用；但 CSS3 提供了一系列新的结构伪元素，用于精确设置元素子元素的样式（表 4.4）：

- first-child——如果选择器类型是其父元素的第一个子元素，则设置该第一个实例的外观。

- first-of-type——当元素的选择器类型在父元素中第一次出现时设置其外观。

- nth-child(#)——设置指定子元素的样式。例如，段落的第三个孩子是 `p:nth-child(3)`。

- nth-of-type(#)——设置选择器类型在父元素中特定位置的样式，第七个段落是 `p:nth-of-type(7)`。

- last-of-type(#)——设置选择器类型在父元素中特定位置的样式，但从底部开始。例如，倒数第三个段落是 `p:last-of-type(3)`。

- last-child——如果指示的选择器是父元素的最后一个子元素，则设置其外观。

- last-of-type——设置其父元素中特定选择器类型的最后一个实例的外观。

## 文本装饰：

要不要加下划线

下划线是 Web 上指示超链接的标准方式。然而，许多带有下划线的链接会让页面变成密不透风的线条堆，文本变得难以阅读。此外，如果访问者关闭了下划线，他们就看不到链接，特别是当链接颜色和文本颜色相同时。

CSS 允许你关闭链接下划线，覆盖访问者的偏好。我建议这种做法，并依靠清晰的颜色选择来突出超链接，或者依靠 `border-bottom`（下边框）这种替代下划线方法，这可以让你更好地控制下划线的样式。更多信息请参见第 14 章。

## 为元素的子元素设置样式：

- 1. 根据它们在父元素中的位置对元素设置样式。输入你想设置样式的元素的选择器（HTML、类或 ID）、冒号（:）；以及表 4.4 中的其中一个结构伪元素（代码 4.8）。

```
li:first-child {...}
li:first-of-type {...}
li:nth-of-type(3) {...}
li:nth-last-of-type(2) {...}
li:last-child {...}
li:last-of-type {...}
```
