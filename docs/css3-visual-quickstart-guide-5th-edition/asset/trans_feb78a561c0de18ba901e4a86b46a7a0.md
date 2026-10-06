

## 代码 3.11 继续

```html
<h1 style="font:italic bold small-caps 3em/9 Constantia, Georgia, Times, 'Times New Roman', Serif;
  color:red>爱丽丝仙境游游</</h1>
<p class="byline">作者：<span class="author">刘易·卡罗尔</span></p>
<article>
  <header>
    <h2><strong>第一章. </strong>掉兔子洞</h2>
  </header>
  <figure id="gallery">
    <img src="./images/AAIW-illos/alice26a.png" alt="alice15a">
    <figcaption>
      “闪烁，闪烁，小蝙蝠！<br>
      我真奇你在做什么”
    </figcaption>
  </figure>
  <p>爱丽丝开始觉得坐在岸边姐姐旁非常无聊了……</p>
</article>
</body>
</html>
```

![](img/9cd61ac1d4015ed5688d0c411434a660_84_0.png)

# 爱丽丝仙境游游
作者：刘易·卡罗尔

第一章. 掉兔子洞

爱丽丝开始觉得坐在岸边姐姐旁非常无聊了。由于无事可做，她一或几次偷看了看姐姐正在读的书；书里既没有插画也没有对话。爱丽丝想：“如果没有插画或对话，书还有什么用呢？”

于是她在心里考虑着（因为她很困，炎热的天气让她感到昏昏欲睡），去散散步的快乐或许值得她起身走在雏菊丛中。这时，一只白兔兔子飞快地从她身边跑过。

没有什么比这更特别的了，爱丽丝事后回想起来也没有那么在意。她觉得自己并没有太预料到这一点，但当兔子真的从背甲外套里掏出一块表，揣进兜里，然后匆匆离开时，这一切似乎又很自然。爱丽丝跳了起来，因为她觉得看到兔子从外套里掏表或把表放进兜里太新奇了。本着强烈的好奇，她跑过田野，幸运的是，她及时钻进了灌篱丛下一个巨大的兔子洞。

代码 3.11 的结果。所有外边距（margins）均为 0，为你的设计提供了一个整洁的画布。

CSS 基础 61

# 分组：使用相同样式定义元素

如果你让两个或多个选择器（selectors）具有相同的声明（declarations），可以将这些选择器用逗号分隔并组合在一个列表中 A。根据需要，你可以在声明块（declaration block）中定义公共属性，并单独为每个选择器添加规则以进行精细调整。

## 如何分组选择器：

- 1. 添加一组用逗号分隔的选择器。输入用逗号分隔的选择器列表（HTML、类或 ID）。你可以在逗号后添加一个或多个换行符、空格或制表符，这不会影响代码，但使其更具可读性。
```css
h1, h2, .byline, #gallery {...}
```
这些选择器都接收相同的声明。CSS 规则可以定义在文档 head 部分的 style 标签中，也可以定义在导入或链接到 HTML 文档的外部 CSS 文件。

- 2. 为选择器组添加公共声明。在大括号内，输入分配给所有列出选择器的样式声明——格式为 `属性: 值`——使用分号（;）并分隔列表中的单独声明。你也可以在声明后添加一个或多个换行符、空格或制表符，这不会影响代码，使其更具可读性。
```css
font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
```

- 3. 根据需要添加精细调整。你可以单独为每个选择器添加或更改声明以适应你的需求。如果你覆盖了组规则中设置的声明，请确保该规则在 CSS 中位于组规则之后。（参见第 4 章“层叠顺序”）。
```css
h1 {...}
```

> 提示：像这样分组选择器可以节省大量时间和减少重复工作。但要注意，当你更改组合声明中任何属性的值时，你会更改列表中每个选择器的该值。

> 提示：分组选择器不会直接影响它们的层叠顺序（在第 4 章解释）；相反，分组处理方式就像每个选择器按照它们列出的顺序被分配了该规则一样。

# 注释：定义 1 级和 2 级标题、作者行以及 gallery ID 的公共样式

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <title>爱丽丝仙境游游</title>
  <style type="text/css" media="all">
  @import url('ch01.css');
  * {
    margin: 0;
    padding: 0;
  }
  h1, h2, .byline, #gallery {
    font-family: Constantia, Georgia, Times, "Times New Roman", Serif;
  }
  h1 {
    color: gray;
  }
  h2 {
    font-size: normal small-caps 2em;
    color: darkred;
  }
  strong {
    font-weight: normal;
    color: black;
  }
  p.byline {
    font-size: 1.25em;
    font-style: normal;
    font-weight: bold;
    word-spacing: -3em;
    text-align: right;
    color: rgba(255, 0, 0.75);
  }
  .author {
    font-size: 1.25em;
    font-style: normal;
    font-weight: bold;
    color: rgba(255, 0, 0,1);
    word-spacing: 0em;
    text-transform: uppercase;
    vertical-align: -.6em;
  }
  #gallery {
    position: relative;
    bottom: 10px;
    right: 10px;
    display: block;
```

# 代码 3.12 继续

```css
<style>
  font-style: italic;
  width: 300px;
  float: left;
  margin: 20px 20px 0 0;
  border: 1px double rgba(255, 0, 0,.5);
</style>
</head>
<body>
<h1 style="font:italic bold small-caps 3em/9 Constantia, Georgia, Times, 'Times New Roman', Serif;
  color:red>爱丽丝仙境游游</</h1>
<p class="byline">作者：<span class="author">刘易·卡罗尔</span></p>
<article>
  <header>
    <h2><strong>第一章. </strong>掉兔子洞</h2>
  </header>
  <figure id="gallery">
    <img src="./images/AAIW-illos/alice26a.png" alt="alice15a">
    <figcaption>
      “闪烁，闪烁，小蝙蝠！<br>
      我真奇你在做什么”
    </figcaption>
  </figure>
  <p>爱丽丝开始觉得坐在岸边姐姐旁非常无聊了……</p>
</article>
</body>
</html>
```

# 整合在一起

- 1. 将内容添加到你的 HTML 文件中。使用你在第 2 步的 HTML 文件，添加文本和图像内容。我倾向于使用《爱丽丝仙境游》，但任何内容都可以。文本的好来源是古书计划（www.gutenberg.org）。
- 2. 标记你的内容。所有样式都需要网页中的标记才能应用。请确保标记标题和段落。
- 3. 在你的标记中添加类（class）和 ID。类可以提供为特定元素应用特定样式的“钩子”。但不要过度，仅在有助于区分元素类型时添加类，在区分特定元素时添加 ID。
- 4. 将你的 HTML、类和 ID 声明添加到文档 head 中的 `<style>` 标签中。你可以根据第 5-12 章所示的样式对它们进行任何设置。
- 5. 为你的 CSS 代码添加注释。注释可以包含关于代码的信息，或者关于创作者（你）以及如何就问题联系他们。
- 6. 将第 4 步中的内联样式移动到外部文件中。创建一个文本文件，然后仅复制并粘贴 CSS 代码（`<style>` 标签标签内的所有内容）到文件中。确保保存文件以 `.css` 结尾。
- 7. 从外部样式表添加 `<link>`。当你在浏览器中测试网页时，它看起来应该和第 4 步一样，但现在 CSS 可以供你所有的网页访问。

