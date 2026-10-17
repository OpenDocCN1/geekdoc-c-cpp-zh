
结果如如图 3-31 所示的网格布局。注意，此布局由单行两列组成，其中第一列包含跨越两行排列的三列。但请记住，实际的列宽并不是由类名设置的，而是在样式表中定义的。类名只是帮助我们解释 HTML 文件中网格布局的工具。

## 图 3-31 示例网格布局

![](img/bf90ebf56b5f948b05e7a26851204c31_222_0.png)

现在你已经看到了布局网格中 HTML 代码的通用结构，你将为 Pandasia Chocolates 网站的一个新页面创建一个网格，该页面提供有关巧克力和公司的信息。Anne 已为图 3-32 所示的页面内容设计了一个网格。

## HTML 206 HTML 与 CSS | 教程 3 页面布局设计

### 图 3-32 关于 Pandasia 巧克力（About Pandasia）的建议网格布局

![](img/bf90ebf56b5f948b05e7a26851204c31_223_0.png)

Anne 的布局包含三个主行。第一行包含页面标题，第三行包含页面页脚。第二行由两列组成：第一列显示公司信息，第二列显示常见问题列表。

## 要创建“关于 Pandasia 巧克力”（About Pandasia Chocolates）

1. 使用你的编辑器打开 `html` 文件夹下的 `pc_about.html` 文件。在内容部分输入你的名字和日期，并将文件保存为 `pc_about.html`。
2. 在页眉下方，插入以下用于第一行的 `div`：
```html
<div class="row"></div>
```
3. 接下来，插入以下包含列的第二行 `div`：
```html
<div class="row">
  <div class="col-2-3">
    <div class="row">
      <div class="col-1-4"></div>
      <div class="col-1-4"></div>
      <div class="col-1-2"></div>
    </div>
    <div class="row">
      <div class="col-1-1"></div>
    </div>
  </div>
  <div class="col-1-3"></div>
</div>
```
4. 最后，插入以下用于第三行的 `div`：
```html
<div class="row"></div>
```
5. 花些时间检查你的代码，确保它与图 3-33 所示的结构和类名匹配。
6. 保存更改但不要关闭。

## HTML 208 HTML 与 CSS | 教程 3 页面布局设计

现在你已经建立了页面内容的网格，你将设置网格的样式，从网格行开始。

### 设计网格行

网格行包含浮动列。由于网格行在页面内新起一行，它应该只在清除了之前的浮动列时才显示。由于它包含一组浮动列，它必须能够扩展高度以覆盖这些对象（否则浮动列有溢出到网格行的风险）。与节中页脚后的行一样，可以使用以下样式规则建立这些规则：

```css
div.row:after {
  clear: both;
  content: "";
  display: table;
}
```

将此类名添加到新的样式 `pc_grids.css` 中，你将用它格式化 `pc_about.html` 文件中的网格布局。

![](img/bf90ebf56b5f948b05e7a26851204c31_224_0.png)

### 图 3-34 突出了网格行的样式规则

# 教程 3 设计页面布局 | HTML 和 CSS HTML 209

**图 3-34** 行级 `div` 元素的样式

```css
/* 网格行样式 */
div.row {
  clear: both;
}
div.row:after {
  clear: both;
  content: ""
  display: table;
}
```

接下来，你将为网格列创建样式规则。

### 设计网格列

每一列都需要在其所在的行内进行浮动。在为“关于熊猫巧克力”（About Panda Chocolates）页面设置的网格中，网格列放置于通用类名 `class="col-numerator-denominator"` 的 `div` 元素中。

> 提示
> 如需复习属性选择器，特别是 `class="*"`，请参阅教程 2 中的图 2-15。

其中 `col-numerator-denominator` 提供了列的宽度。例如，`col-1-3` 表示该列是总行的第三部分。若要让所有列浮动，可以使用以下属性选择器，它可以匹配所有类 属性以 `"col-"` 字符串开头的元素。

```css
div[class^="col"] {
  float: left;
}
```

现在将此样式规则添加到 `pc_grids.css` 样式文件中。

- **要浮动网格列：**
1. 在“网格列”（Grid Columns）部分，插入以下样式规则：
```css
div[class="col-"] {
  float: left;
}
```

**图 3-35** 高亮了网格列的样式规则。

| 匹配所有 `div` 元素 | 网格列样式 /* | |
| --- | --- | --- |
| 其类 属性以 `"col-"` 开头 | `div[class^="col-"] { float: left; }` | 将每一列浮动到左侧 |

- 2. 保存对文件的更改。

HTML 210 HTML 和 CSS | 教程 3 设计页面布局

最后，你必须根据每个列的类名建立每列的宽度。例如，类名为 `col-1-3` 的 `div` 元素将使用以下样式规则将其宽度设置为父元素（即网格行）宽度的 1/3 或 33.33%。

```css
div.col-1-3 { width: 33.33%; }
```

为宽度从 25% 到 100% 的网格列添加样式规则。

### 设置网格列的宽度：

- 1. 在“网格列”（Grid Columns）部分，添加以下样式规则：

```css
div.col-1-1 { width: 100%; }
div.col-1-2 { width: 50%; }
div.col-1-3 { width: 33.33%; }
div.col-2-3 { width: 66.67%; }
div.col-1-4 { width: 25%; }
div.col-3-4 { width: 75%; }
```

图 3-36 分配给不同类元素的宽度值。

![](img/bf90ebf56b5f948b05e7a26851204c31_227_0.png)

| 全宽列 | `div[class="col"] { left: }` | 三之一和三之二宽列 |
| --- | --- | --- |
| | `div.col-1-1 { width: 100%; }` `div.col-1-2 { width: 50%; }` `div.col-1-3 { width: 33.33%; }` `div.col-2-3 { width: 66.67%; }` `div.col-1-4 { width: 25%; }` `div.col-3-4 { width: 75%; }` | 四分之一和四之三宽列 |

- 2. 保存对文件的更改。

按照这种方式，你还可以包含其他基于百分比的列。例如，六分之一列的宽度将为 8.33%，以此此类推。

### 添加页面内容

现在你已经建立了网格的基本框架，可以为每一行和每一列添加页面内容了。为了避免手动输入内容，Anne 准备了一个文件，其中包含出现在“关于熊猫巧克力”（About Pandaisia Chocolates）页面上的文章文本。现在开始插入这些内容，从网格中的第一行文本开始。

![](img/bf90ebf56b5f948b05e7a26851204c31_227_1.png)

教程 3 设计页面布局 | HTML 和 CSS HTML 211

向网格中插入页面内容：

- 1. 回到编辑器中的 `pc_about.html` 文件。
- 2. 紧接 `<div class="row">` 标签之后，插入以下 `h1` 标题：
   `<h1>About Pandaisia Chocolates...</h1>`

图 3-37 显示了 `h1` 标题在第一行网格中的放置位置。

![](img/bf90ebf56b5f948b05e7a26851204c31_228_0.png)

在网格的第一行添加标题

```html
<header>
<div class="row">
  <h1>About Pandaisia Chocolates...</h1>
</div>
</header>
```

接下来，你将插入左侧的文本。

- 3. 打开编辑器中的 `pc_text.txt` 文件，复制来自“公司”（Company）部分的 HTML 代码。
- 4. 将这些代码直接插入到网格顶部的 `<div class="col-2-3">` 标签之后。

图 3-38 显示了标题的放置位置。

![](img/bf90ebf56b5f948b05e7a26851204c31_228_1)

关于公司的信息

```html
<div class="row">
  <h1>About Pandaisia Chocolates...</h1>
</div>
```

接下来，你将插入第二行左侧的文本。

- 5. 回到编辑器中的 `pc_text.txt` 文件，复制来自“享受巧克力”（Enjoying Chocolates）部分的 HTML 代码。
- 6. 将这些代码插入到网格中的第一列中，如图 3-39 所示。

图 3-39

| 行标题 | 添加关于巧克力的内容 |
| --- | --- |
| 插入到第一列的内容 | `<div class="row">\n  <h2>Chocolate</h2>\n  <div class="col-1-2">\n<h3>Enjoying Chocolates</h3>\n    <p>我们相信新鲜巧克力是最好的。防腐剂会改变巧力的风味和质地；为了结果，巧克力应在购买后尽快食用。存放在阴凉处或 60° 至 70° 的温度下，如酒窖。</p>\  </div>\n</div>\n<div class="row">\n  <div class="col-1-2">  </div>\n  <div class="col-1-2">  </div>\n</div>` |

- 7. 按照相同的方式，为剩余的三个列添加内容。返回编辑器中的 `pc_text.txt` 文件，复制来自“享受巧克力”（Enjoying Chocolate）部分的最后三个部分：“健康巧克力”（Healthy Chocolate）、单产地与混合”（Single-Origin and Blend）以及“道德生产”（Ethical Produce）。每个部分包含一个 `h3` 标题和一段文本。将复制的代码插入到剩余的三个宽列中，如图 3-40 所示。

图 3-40

向剩余的列添加内容

```html
<h3>健康巧克力</h3>
<p>巧力的声誉不好是因为大众产巧克力充斥了大量的牛奶、糖和脂肪，这些虽然好吃但不健康。使用有机成分，将加工糖降到最低，并生产含量为 73% 的黑巧克力。在该水平下，你可以享受到巧克力饮食的好处！</p>
</div>
<div class="col-1-2">
  <div class="row">
    <h3>单产地与混合</h3>
    <p>我们相信由单一地区收获的单一品种可制成的单产地巧克力。单产地巧克力吸收了地区的独特风味，就像葡萄酒采纳地区特征一样。其他巧克力师使用来自多个地区的混合口味。让我们知道你更倾向于哪种。</p>
  </div>
  <div class="col-1-2">
    <h3>道德生产</h3>
    <p>我们直接与秘鲁、厄瓜多尔和洪拉斯的农民合作，我们亲身体验了经济如何影响他们。我们支付高于市场的价格以维持我们的合作关系并支持公平贸易。我们一直在努力为优质巧克力建立一个可持续的市场，并支持生产这些巧力的勤劳的人。</p>
  </div>
</div>
```

- 8. 第二行的右侧列包含一个常见问题列表。返回编辑器中的 `pc_text.txt` 文件，复制来自“常见问题”（Frequently Asked）部分的 `aside` 元素及其内容。
HTML 341

- 9. 回到编辑器中的 `pc_about.html` 文件，并将复制的代码粘贴到右侧列中，如图 3-41 所示。

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

粘贴到 `aside` 元素中的常见问题（FAQs）内容

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
