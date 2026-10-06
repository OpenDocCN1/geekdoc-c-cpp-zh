

## 创建小型大写 (Small Caps)

小型大写（有时被称为微大写）用于强调标题（见表 5.8）。使用小型大写，小写字母会被转换为大写，但尺寸比普通大写字母 A 略小。

## 普通小型大写

使用小型大写时，所有字母均为大写，但第一个字母比其他字母大。

| 表 5.8 字体变体值 | |
| 值 | 兼容性 |
| --- | --- |
| normal | IE4, FF1, S1, C1, O3, CSS1 |
| small-caps | IE4, FF1, S1, C1, O3, CSS1 |

## 为元素设置小型大写：

- 1. 在您的 CSS 中添加 `font-variant` 属性。输入属性名 `font-variant`（代码 5.8），后加冒号 (:)。
- 2. 为变体定义值。
  `small-caps;`

输入 `font-variant` 属性的值，使用以下之一：

- small-caps，将小写字母设置为真实大写字母的较小版本
- normal，覆盖可能继承的其他字体变体值

![](img/9cd61ac1d4015ed5688d0c411434a660_167_0.png)

标题使用小型大写是将其与正文区分开的一种优雅方式。

> 小型大写最好留给标题或特殊文本；它们在较小的字体下可能难以阅读。

## 5.8 font-properties.css—小型大写应用于 header 1 和 header 2，但在 h2 内部的 `strong` 元素中禁用。注意，`@font-face` 中的声明已更改为 `small-caps` 规则，因此下载的字体将在 h1 中显示 ⓘ

```css
*** CSS VDS - Chapter 5 - fontproperties.css ***

@font-face {
  font-family: 'Title Font';
  src: url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff');
  src: local('Little Trouble Girl'), url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff') format('woff');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.ttf') format('truetype');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.svg#webfont') format('svg');
  font-weight: bold;
  font-style: italic;
  font-variant: small-caps;
}
```

```css
body {
  font-family: Corbel, Helvetica, Arial, Sans-serif;
  font-size: 100%;
  font-size-adjust: .5; }
```

```css
h1, h2, h3, h4, h5, h6, .byline {
  font-family: Constancia, Georgia, Times, "Times New Roman", Serif;
  font-size-adjust: .46; }
```

```css
h1 {
  font-family: 'Title Font', Constancia, Georgia, Times, "Times New Roman", Serif;
  font-size: 3em;
  font-style: italic;
  font-weight: bold;
  font-variant: small-caps; }
```

```css
h2 {
  font-size: 2em;
  font-style: normal;
  font-weight: lighter;
  font-variant: small-caps; }
```

```css
h2 strong {
  font-size: .5em;
  font-style: italic;
  font-variant: normal; }
```

```css
p {
  font-size: .875em; }
```

```css
strong {
  font-size: 1.25em; }
```

```css
.byline {
  font-size: 1em;
  font-style: italic; }
```

```css
.byline .author {
  font-size: 1.25em;
  font-style: normal;
  font-weight: bold; }
```

## 设置多个字体值

虽然你可以独立设置字体属性，但将所有字体元素放在单个声明中（见表 5.9）通常更有用，更不用说更简洁了。要实现这一点，你可以使用简写属性 `font`。

| 表 5.9 字体值 | |
| 值 | 兼容性 |
| <font-style> | IE3, FF1, S1, C1, O3.5, CSS1 |
| <font-variant> | IE3, FF1, S1, C1, O3.5, CSS1 |
| <font-weight> | IE3, FF1, S1, C1, O3.5, CSS1 |
| <font-size> | IE3, FF1, S1, C1, O3.5, CSS1 |
| <line-height> | IE3, FF1, S1, C1, O3.5, CSS1 |
| <font-family> | IE4, FF1, S2, C1, CSS2 |

要在规则中同时定义多个字体属性：

- 1. 在你的 CSS 中添加 `font` 属性。输入属性名 `font`（代码 5.9），后加冒号 (::)。按照按照练习中剩余步骤的顺序输入值。
- 2. 可选，定义样式值。输入 `font-style` 值，后加空格。（参见“设置斜体”章节）。
- 3. 可选，定义权重值。输入 `font-weight` 值，后加空格。（参见“设置加粗”章节）。
- 4. 可选，定义变体值。输入 `font-variant` 值，后加空格。（参见“创建小型大写”章节）。
- 5. 定义大小值。输入 `font-size` 值。（参见“设置字体”章节）。
- 6. 可选，定义行高值。输入 `line-height` 值，后加分号 (;）。参见“调整间距”章节）。
- 7. 定义字体族值。输入 `font-family` 值。（参见“设置字体族”章节）。

> 提示 `font` 简写属性是一个节省时间的利器，我尽可能经常使用它。它输入和编辑的时间更短，并且可以加快加载速度。

> 提示 编辑软件（如 Dreamweaver）倾向于使用单独属性而不是简写。

> 提示 如果不想在列表中设置特定的样式或权重值，只需跳过即可。浏览器将使用其默认值。

> 提示 然而你必须至少包含一个值，即使是 `normal`。

> 提示 如果你需要覆盖由 `font` 简写设置的值，通常最好使用完整属性（如 `font-style`、`font-variant`、`font-weight` 和 `font-family`）。

5.9 font-properties.css——只要可能，字体属性已合并到简写属性中。这需要大小、字体族以及至少一个其他字体属性定义

```css
*** CSS V - Chapter 5 - font-properties.css ***
@font-face {
  font-family: 'Title Font';
  src: url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff');
  src: local('Arial'), url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.woff') format('woff');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.ttf') format('truetype');
  url('../fonts/Little-Trouble-Girl/litttroublegirl-webfont.svg') format('svg');
  font-weight: bold;
  font-style: italic;
  font-variant: small-caps;
}

body {
  font: normal 100% Corbel, Helvetica, Arial, Sans-serif;
  font-size-adjust: .5;
}

h1, h2, h3, h4, h5, h6, .byline {
  font-family: Constancia, Georgia, Times, "Times New Roman", Serif;
  font-size-adjust: .6;
}

h1 {
  font: italic bold small-caps 3em 'Title Font', Constancia, Georgia, Times, "Times New Roman", Serif;
}

h2 {
  font-size: 2em;
  font-style: normal;
  font-weight: lighter;
  font-variant: small-caps;
}

h2 strong {
  font-size: .5em;
  font-style: italic;
  font-variant: normal;
}

p {
  font-size: .875em;
}

byline {
  font-size: 1em;
  font-style: italic;
}

byline .author {
  font-size: 1.25em;
  font-style: normal;
  font-weight: bold;
}
```

## 爱丽丝漫游仙境记

路易斯·卡罗尔 著

## 第一章 兔子洞

爱丽丝开始觉得坐在河岸的姐姐身边很无聊，而且无事可做：她曾一两次偷看一眼她姐姐正在读的那本书，发现里面既没有图片也没有对话。爱丽丝想，“一本没有图片或对话的书能有什么用呢？”

于是她在心里考虑（尽管尽所能地考虑，因为天气炎热，她感到非常困倦和愚钝），制作一个雏菊花环的快乐是否值得费去起床采雏菊的麻烦。这时，一只粉粉色眼睛的白兔子从她身边经过。

这没有什么特别不起的，爱丽丝也不觉得听到兔子自言自语说“噢天哪噢天哪，我要迟了！”是很奇怪的事（当她以后回想起来时，她认为自己应该感到惊讶，但在当时这一切看起来都是很自然的）；但当兔子实际上从它身上掏出一块表时，这个版本看起来与前一个章节相似，只是行间距不同。

## 模仿访问者的样式

如果可以匹配访问者的系统字体样式，那不是很好吗？你只需将字体样式声明为以下关键字之一即可（例如，`font: icon;`）：

- caption：用于按钮等控件的字体样式
- icon：用于标记图标的字体样式
- menu：用于下拉菜单和菜单列表的字体样式
- message-box：用于对话框的字体样式
- small-caption：用于标记小型控件的字体样式
- status-bar：用于窗口顶部状态栏的字体样式

