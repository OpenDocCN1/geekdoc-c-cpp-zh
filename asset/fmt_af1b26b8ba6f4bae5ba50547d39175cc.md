
Copyright 2018 Cengage Learning. 版权所有。未经全部或部分复制、扫描或复制。WCN 020-200-233

# 教程 3 设计页面布局 | HTML 与 CSS

- 2. 保存你对文件的更改，然后在浏览器中重新加载 `pc_about.html` 文件。图 3-43 显示了页面的最终布局。

图 3-43

About Pandasiaia Chocolates 页面内容的格式

![](img/bf90ebf56b5f948b05e7a26851204c31_232_0.png)

第一行

## 关于 Pandasiaia 巧克力

## 我们的公司

## 常见问题

我们是一家位于佛蒙特州埃塞（Essex）的公司，多年来一直致力于制作精美的巧克力。我们只使用传统方法和高质量原料，创造出浓郁风味与丝滑口感的完美融合。

你有喜爱的巧克力吗？

我喜欢黑巧克力，它非常适合早晨吃，并能给我提供能量。

你喜欢怎么吃它？

我喜欢融化后吃，搭配水果、坚果，或者直接吃。

我们通常会和朋友、家人和同事分享我们的产品。

我们的产品很快吸引了人们在生日、婚礼和纪念日等特殊场合，或作为一种奖赏。

如果你有一盒我们的巧克力，你每天会吃几次？

巧克力是“罪恶食品”吗？

不，完全不是！

## 关于巧克力

第二行

我们认为，最好的巧克力是那种凸显巧克力风味和质地的巧克力。因此，我们在巧克力中仅使用最优质的原料。我们将它们储放在阴凉、黑暗的地方，作为零食或冬季甜点。

## 健康的巧克力

## 单源巧克力

## 混合巧克力

```html
<div class="row">
  <footer>Pandasiaia Chocolates&copy; 2017 All Rights Reserved</footer>
</div>
```
图 3-42 显示了网格中最后一行的代码。关于 Pandasiaia 巧克力的页面内容已完成。

```html
<div class="row">
  <footer>Pandasiaia Chocolates&copy; 2017 All Rights Reserved</footer>
</div>
```

网格中的最后一行

- 11. 保存你对文件的更改。
Anne 已经创建了样式表，其中包含了此页面内容的字体样式和颜色样式。将 `pc_about.html` 文件链接到 `pc_reset.css`、`pc_grids.css` 和 `pc_styles2.css` 样式表文件。

> 要链接样式：
1. 滚动到文档顶部，在 `title` 元素之后插入以下 链接 元素：
```html
<link href="pc_reset.css" rel="stylesheet" />
<link href="pc_grids.css" rel="stylesheet" />
<link href="pc_styles2.css" rel="stylesheet" />
```

# HTML 214 HTML 与 CSS | 教程 3 设计页面布局

图 3-41 为常见问题添加内容

```html
<div class="col-1-3">
  <aside>
    <h2>常见问题</h2>
    <dl>
      <dt>你们提供婚礼巧克力服务吗？</dt>
      <dd>是的！这是我们最喜欢做的事情。我们销售各种包装设计的巧克力，非常适合婚礼或其他特殊场合。</dd>
    </dl>
    <dt>Pandasiaia 在哪里？</dt>
    <dd>很高兴你问了这个问题。Pandasiaia 并不是一个地方；它是希腊宴会女神的名字，而没有巧力的哪里叫宴会呢？</dd>
  </aside>
</div>
```

粘贴到 `aside` 元素中的常见问题内容

- 10. 转到最后一行，在 `div` 标签的开始标签和结束标签 `</div>` 之间插入以下 HTML 代码：
```html
<footer>Pandasiaia Chocolates&copy; 2017 All Rights Reserved</footer>
```
图 3-42 显示了网格中最后一行的代码。关于 Pandasiaia 巧克力的页面内容已完成。

图 3-42 为最后一行添加页脚

```html
<div class="row">
  <footer>Pandasiaia Chocolates&copy; 2017 All Rights Reserved</footer>
</div>
```

网格中的最后一行

- 11. 保存你对文件的更改。
Anne 已经创建了样式表，其中包含了此页面内容的字体样式和颜色样式。将 `pc_about.html` 文件链接到 `pc_reset.css`、`pc_grids.css` 和 `pc_styles2.css` 样式表文件。

> 要链接样式：
1. 滚动到文档顶部，在 `title` 元素之后插入以下 `link` 元素：
```html
<link href="pc_reset.css" rel="stylesheet" />
<link href="pc_grids.css" rel="stylesheet" />
<link href="pc_styles2.css" rel="stylesheet" />
```

# HTML 218 HTML 和 CSS | 教程 3 设计页面布局

图 3-45

# 为每个 div 添加了轮廓

![](img/bf90ebf56b5f948b05e7a26851204c31_235_0.png)

- 5. 关闭任何已打开的文件

Anne 对你在 Pandaisia Chocolates 页面上所做的工作表示感谢。她认为网格行和列周围的轮廓有助于查看布局样式，这将便于在原处进行修改。目前，你将保留这些轮廓，以协助她进行页面设计工作。

# 使用 CSS 创建字母大字

一种流行的设计元素是字母大字（drop cap），它由正文中一个放大并下沉文本的字母组成。要创建字母大字，你需要增加元素第一个字母的字体大小，并将其浮动到左边距。通常，如果调整第一个字母的高度，字母大字看起来会更好，让周围的内容环绕该字母排列。寻找字体大小和行高的最佳组合是一个不断尝试的过程；遗憾的是，在某个浏览器中有效的方案在另一个浏览器中可能并不好看。以下样式规则适用于为第一个段落元素应用字母大字：

```
p:first-of-type:first-letter {
  font-size: 4em;
  float: left;
  line-height: 0.8;
}
```

对于额外的的设计效果，你可以将字母大字的字体更改为草体或装饰字体。

# 引入 CSS 网格

网格（Grids）是创建布局的一种快速且灵活的方法，但并非没有问题。最明显的问题是，设置网格通过添加另一层标记增加了 HTML 代码的大小和复杂性。另一个同样严重的问题是，网格破坏了基本规则，即 HTML 文件应该只包含有意义的内容，所有的演示指令都应该放置在外部样式表中。然而，使用 HTML 网格系统，`div` 元素除了定义网格如何渲染外没有其他用途。如果设计师想更改布局，HTML 文件和样式表都需要进行修改，这为网站设计增加了额外的复杂性。

# 定义 CSS 网格

由于网格是一个重要且实用的工具，W3C 正在致力于向 CSS 中添加样式。为了在不使用 `div` 元素的情况下创建网格显示，CSS 现在正在添加以下基于网格的属性：

```
selector {
  display: grid;
  grid-template-rows: track-list;
  grid-template-columns: track-list;
}
```

`display` 属性的 `grid` 关键字规定所选元素将以网格形式显示。网格中的行列数由 `grid-template-rows` 和 `grid-template-columns` 属性设置，其中 `track-list` 是由空格分隔的行或列单位列表，包含使用任何 CSS 单位表示的关键字。行或列的高度和宽度将根据其内容自动调整。

例如，以下样式为 `section` 元素建立了一个网格。该网格由三行组成，第一行和最后一行设置为 100 像素，中间行自动匹配其内容。网格还由三列组成，第一列和最后一列的宽度为 25%，中间列占据每个网格行的剩余。

```
section {
  display: grid;
  grid-template-rows: 100px auto auto;
  grid-template-columns: 25% 50% 25%;
}
```

CSS 还使用了 `fr` 单位，它代表在所有其他行或列占据其最大尺寸后，网格上可用空间的比例。例如，以下样式创建了四列：两列宽度分别为 200 像素和 250 像素，两列分别为 1fr 和 2fr：

```
grid-template-columns: 200px 250px 1fr 2fr;
```

`fr` 单位可以被视为可用空间的“份额”，因此在这个示例中，450 像素分给了前两列，剩余的所有空间在最后两列之间分配，其中第四列分配三分分之一或二之二。

# 将内容分配给网格单元格

一旦建立了网格，你就可以将元素放在特定的网格单元中。默认情况下，元素按照它们在 HTML 中出现的顺序排列。但是，你可以使用网格属性精确指定每个元素应该所在的位置。以下样式规则显示了如何将第一个段落放在第一个单元格：

```
p {
  grid-column: 1 / 2;
  grid-row: 1 / 2;
}
```
