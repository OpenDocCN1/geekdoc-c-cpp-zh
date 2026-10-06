

TIP `text-transform` 属性最好用于动态生成文本的格式化。例如，如果数据库中的名称全大写，你可以使用 `text-transform` 让它们更具可读性。

TIP 请注意，capitalize 会大写文本中的所有字母，即使是像 "of" 和 "the" 这样应该保持小写的单词也是如此。在实际上，`capitalize` 主要用于人名。

TIP **不要用全大写字母输入文本**。当 HTML 文本为全大写时，在 CSS 中控制它会困难得多。此外，任何使用辅助设备阅读的人都会将其听为大叫。最好使用普通文本配合 `text-transform` 来将文本样式化为大写。

![](img/9cd61ac1d4015ed5688d0c411434a660_182_0.png)

将代码 6.5 应用于代码 6.1：书名下的刘易斯·卡罗尔（Lewis Carroll）的名字全大写了（与第 5 章解释的小大写字母相反）。

## 新 CSS3：添加文本阴影 ★

投影影是为二维设计增加深度和纹理的一种悠久方法。大多数浏览器都支持 CSS 中的 `text-shadow` 属性（表 6.5），它允许你为任何文本阴影定义颜色、偏移（x 和 y）、扩散和模糊。虽然该属性目前在其他浏览器中不起作用，但在旧版本中也同样不起作用。

| 表 6.5 Text-Shadow 值 |
| 值 | 兼容性 |
| --- | --- |
| <color> | FF1.9, S1, C2, O03 |
| <x-offset> | FF1.9, S1, C2, O03 |
| <y-offset> | FF1.9, S1, C2, O03 |
| <blur> | FF1.9, S1, C2, O03 |
| none | FF1.9, S1, C2, O03 |

定义文本阴影：

![](img/9cd61ac1d4015ed5688d0c411434a660_183_0.png)

- 1. 在你的 CSS 规则中添加 `text-shadow` 属性。在 CSS 列表中输入 `text-shadow`，后跟一个冒号（: 代码 6.5）。

```
text-shadow:
```

- 2. 指定 x、y 偏移。输入一个空格，然后是两个由空格分隔的正或负长度值。

```
2px 2px
```

第一个值是偏移阴影的垂直距离（正为向下，负为向上）。第二个值是水平偏移（正为向右；负为向左）。

- 3. 指定模糊量。输入一个空格，然后是应用到阴影上的模糊长度值。所有负值都将被视为 0。

```
2px
```

> 代码 6.6 应用于代码 6.1：虽然你可能需要将修改后的标题与之前的屏幕截图对比才能注意到区别，但标题现在看起来在页面上略微凹陷，就像浮雕一样。而章节标题现在真的跃出了页面。

160 第 6 章

## 6.6 text-properties.css — 投影阴影

属性允许 x/y 偏移和模糊半径。书名具有双阴影，营造出微妙的浮雕效果，而章节标题有一个强烈的阴影，略微向左偏离页面。

## 4. 指定颜色。输入一个空格，然后是阴影的颜色值。

rgba(0,0,0,.5);

关于关于颜色值的更多信息，请参阅第 7 章中的“选择颜色值”。

- 5. 你可以为任何文本块添加多个阴影（随你需要添加多少个都可以）。要做到这一点，你可以在规则中添加另一个 `text-shadow` 声明，或者在逗号后添加另一个定义。

```
*** CSS VS | 第 6 章 | text-properties. css
```

```css
body {
  line-height: 1.5;
}

h1 {
  letter-spacing: -.05em;
  word-spacing: -1em;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 3px;
}
```

```css
text-shadow: rgba(51,51,51,.9)
  -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
```

```css
h2 {
  letter-spacing: 2px;
  word-spacing: 3px;
  line-height: 1em;
  text-shadow: rgba(0,0,0,.5) 2px 2px 2px;
}
```

> TIP 你可以将值设置为 none 以覆盖之前在 CSS 中设置的阴影。

> TIP 使用 RGBA 处理阴影效果最好。真实的显示。

```css
h2 {
  letter-spacing: 0;
  text-shadow: none;
}
```

> TIP 虽然这是一个“阴影”，但你可以对其使用任何颜色。因此，如果你的文本在深色背景上，请使用浅色来创建“发光”。

```css
p {
  word-spacing: .07em;
  line-height: 24px;
}
```

> TIP 在第 11 章，你将学习如何设置类似于应用到元素盒框的 `box-shadow` 属性。

```css
p {
  text-transform: uppercase;
}

header + p:first-letter {
  letter-spacing: -.05em;
  line-height: 24px;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 1px 3px;
}
```

> TIP 阴影不会影响它们所在文本的位置。

```css
.byline {
  word-spacing: -3em;
}

byline .author {
  word-spacing: 0;
  text-transform: uppercase;
}

.asis {
  text-transform: uppercase;
}
```

> TIP 当配合 `:hover` 伪类使用时，文本阴影可以使链接脱颖而出。

![](img/9cd61ac1d4015ed5688d0c411434a660_184_0.png)

## 水平对齐文本

传统上，文本在左边缘对齐（左对齐）或完全对齐（即在左、右边缘都对齐，通常称为报纸风格）。此外，为了强调或特殊效果，文本可以在屏幕上居中或右对齐。**`text-align` 属性（表 6.6）**让你控制文本的对齐和对齐方式。

表 6.6 Text-Align 值
| 值 | 兼容性 |
|---|---|
| left | IE3, FF1, S1, C1, O3.5, CSS1 |
| right | IE3, FF1, S1, C1, O3.5, CSS1 |
| center | IE3, FF1, S1, C1, O3.5, CSS1 |
| justify | IE4, FF1, S1, C1 |
| inherit | IE4, FF1, S1, O3.5, CSS1 |
| auto | IE4, FF1, S1, O3.5, CSS1 |

## 定义文本对齐：

- 1. 在你的 CSS 中添加 `text-align` 属性。在 CSS 列表中输入 `text-align`，后跟一个冒号（: **代码 6.6**）。

```
text-align:
```

- 2. 指定水平对齐方式。

center:

设置以下对齐样式之一：

- left 让文本在左边缘对齐。
- right 让文本在右边缘对齐。
- center 让文本在其区域内居中。
- justify 让文本在左、右边缘都对齐。
- inherit 让文本继承父元素的对齐方式。
- auto 使用默认对齐方式，通常是左对齐。

![](img/9cd61ac1d4015ed5688d0c411434a660_185_0.png)

> 代码 6.7 应用于代码 6.t：如果由于左、右、居中和完全对齐导致看起来有点参差不齐，我们将在本书后面讨论定位时更改标题和行格式。

## 6.7 text-properties.css—.byline 类已右对齐，而二级标题中的章节标题已居中对齐，正文已完全对齐。

文本默认为左对齐。

完全对齐文本可能会在屏幕上产生一些奇怪的结果，因为必须添加单词来使每行相同。此外，对于完全对齐是有帮助还是阻碍可读性，意见存在分歧。

```
*** CSS3 VOS | 第 6 章 | text-properties.
body {
  line-height: 1.5;
}

h1 {
  letter-spacing: -.05em;
  word-spacing: -1.em;
  text-shadow: rgba(51,51,51,.9) -1px -1px 3px, rgba(203,203,203,.9) 1px 3px;
}
```

