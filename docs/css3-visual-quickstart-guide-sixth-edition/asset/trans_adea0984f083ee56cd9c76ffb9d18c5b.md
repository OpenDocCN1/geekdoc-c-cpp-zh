

![](img/e1ed1e3c1873fa9fc855210fb83699d0_190_0.png)

![](img/e1ed1e3c1873fa9fc855210fb83699d0_190_1.png)

## 压印

压印效果与凸版印刷效果相反，营造出文字从页面上凸起的错觉。

```css
.emboss {
  background-color: #ccc;
  color: #ccc;
  text-shadow: -1px -1px 1px rgba(255, 255, 255, 0.75),
    1px 1px 1px rgba(0, 0, 0, 0.75);
}
```

## 霓虹光晕

霓虹光晕效果为文本增添柔和多彩的光晕，仿佛文字由霓虹灯管制成。要创建此效果，请使用白色文本，然后添加模糊度逐渐增加的投影阴影，从白色开始，过渡到所需的霓虹颜色。

```css
.neon {
  background-color: #000;
  color: #fff;
  text-shadow: 0 0 5px #fff,
    0 0 10px #fff,
    0 0 15px #fff,
    0 0 20px #ff2d95,
    0 0 30px #ff2d95,
    0 0 40px #ff2d95,
    0 0 50px #ff2d95,
    0 0 75px #ff2d95;
  letter-spacing: 5px;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_191_0.png)

## 火焰

火焰效果营造出字母散发热量的错觉。要创建此效果，请从白色文本开始，然后叠加阴影，颜色从白色过渡到黄色、橙色再到红色，同时逐层增加 y 偏移量和模糊度。

```css
.fire {
  background-color: #333;
  color: #fff;
  text-shadow: 0px -1px 4px white,
    0px -2px 10px yellow,
    0px -10px 20px orange,
    0px -18px 40px red;
}
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_191_1.png)

## 3D 文本块

3D 文本块效果营造出字母具有深度和质感的错觉，如同复古科幻电影中的字体。要创建此效果，请从白色文本开始，然后叠加逐渐变暗的阴影，每层递增 1px，叠加层数即可达到所需的深度。偏移量取决于您希望文本倾斜的方向。

```css
.d3 {
  background-color: #ccc;
  color: #fff;
  text-shadow: 0px 1px 0px #999,
    0px 2px 0px #888,
    0px 3px 0px #777,
    0px 4px 0px #666,
    0px 5px 0px #555,
    0px 6px 0px #444,
    0px 7px 0px #333,
    0px 8px 7px #001135;
}
```

| 值 | 图标 |
| --- | --- |
| left | ● ● ● ● ● |
| right | ● ● ● ● ● |
| center | ● ● ● ● ● |
| justify | ● ● ● ● ● |
| inherit | ● ● ● ● ● |
| auto | ● ● ● ● ● |

代码 6.7 添加到 text-properties.css 中——标题中的 h2 为右对齐，而段落为两端对齐。

```css
/*** text-properties.css ***/
body { text-align: left; }
h2 { text-align: center; }
header h2 {
  text-align: right; }
p { text-align: justify;
  text-align-last: left;
  text-justify: distribute; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_192_0.png)

代码 6.7 应用于代码 6.1：虽然左对齐、右对齐、居中和两端对齐的文本看起来有点参差不齐，但我们将在本书后面讨论定位时更改标题和署名的格式。

## 水平对齐文本

传统上，文本按左边距对齐（左对齐）或两端对齐，两端对齐会使文本同时与左边距和右边距对齐（通常称为报纸样式）。此外，为了强调或特殊效果，文本可以在屏幕上居中，甚至右对齐。text-align 属性（表 6.6）让您控制文本的对齐方式和两端对齐。

虽然 text-align 属性未在 CSS3 中更新，但添加了两个可直接影响它的新属性。text-align-last 属性允许您将文本块最后一行的两端对齐方式与其余部分分别处理（表 6.7）。这对于实现有趣的设计效果特别有用，例如通过允许最后一行文本完全两端对齐来创建方形文本块。

此外，在两端对齐文本时，您现在可以指定使用的两端对齐方法，这对于非西方语言的文本尤其有用（表 6.8）。

### 定义文本对齐和间距，并两端对齐文本最后一行：

- 1. 将 text-align 属性添加到您的 CSS 中。在 CSS 声明列表中键入 text-align，后跟冒号 (:)（代码 6.7），然后指定水平对齐方式。

```css
text-align: center
```

- 使用以下任一对齐样式：
  - left 将文本对齐到左边距。
  - right 将文本对齐到右边距。
  - center 在其区域内居中文本。
  - justify 将文本同时对齐到左边距和右边距。
  - inherit 使文本继承其父元素的对齐方式。
  - auto 使用默认对齐方式（通常为左对齐）。

- 2. 如果您希望段落的最后一行与其余文本处理方式不同，请添加 text-align-last 属性。在 CSS 声明列表中键入 text-align-last:，后跟冒号 (:)（代码 6.7），并指定如何处理文本块最后一行中的文本：

```css
text-align-last: center;
```

- 使用以下任一对齐样式：
  - left 将最后一行中的文本对齐到左边距。
  - right 将最后一行中的文本对齐到右边距。
  - center 在文本区域宽度内居中文本。
  - justify 将文本同时对齐到左边距和右边距，在单词和字母之间添加额外空间。
  - inherit 使文本继承其父元素的对齐方式。
  - auto 使用默认对齐方式（通常为左对齐）。

为了完全兼容，还应包含 -moz 扩展版本。

```css
-moz-text-align-last: center;
```

| 值 | | | | | |
| --- | --- | --- | --- | --- | --- |
| left | ● | ◇ | | | |
| right | ● | ◇ | | | |
| center | ● | ◇ | | | |
| justify | ● | ◇ | | | |
| inherit | ● | ◇ | | | |
| auto | ● | ◇ | | | |

### 表 6.8 text-justify 值

| 值 | | | | | |
| :--- | :---: | :---: | :---: | :---: | :---: |
| kashida | ● | ● | ● | ● | ● |
| distribute | ● | ● | ● | ● | ● |
| inter-cluster | ● | ● | ● | ● | ● |
| inter-ideograph | ● | ● | ● | ● | ● |
| inter-word | ● | ● | ● | ● | ● |
| none | ● | ● | ● | ● | ● |
| auto | ● | ● | ● | ● | ● |

- 3. 如果您使用两端对齐文本（text-align: justify），请添加 text-justify 属性。在 CSS 声明列表中键入 text-justify，后跟冒号 (:)（代码 6.7），并指定如何处理两端对齐文本：

```css
text-justify: distribute;
```

- 使用以下任一两端对齐样式：
  - kashida 通过拉伸连笔字的连接来两端对齐文本。
  - distribute 在单词和字母之间添加空间。
  - inter-cluster 在没有单词间距的内容中添加空间，例如许多亚洲语言。
  - inter-ideograph 在单词或块脚本之间添加空间，如某些亚洲脚本。
  - inter-word 仅在单词之间添加空间。
  - none 禁用两端对齐。
  - auto 使用默认对齐方式（通常为左对齐）。

**提示** 文本默认左对齐。

**提示** 完全两端对齐文本在屏幕上可能会产生一些奇怪的结果，因为必须在单词之间添加空格以使每行长度相同。此外，关于完全两端对齐是有助于还是妨碍可读性，意见不一。

## 垂直对齐文本

使用 **vertical-align** 属性，您可以指定一个内联元素相对于其上方或下方元素的垂直位置 ➊。这意味着 **vertical-align** 属性（表 6.9）仅可用于内联标签和表格标签——即前后没有换行的标签，例如锚点 (<a>)、图片（）、强调文本 (<em>)、强文本 (<strong>) 和表格数据 (<td>) 标签。

### 定义垂直对齐方式：

- 1. 将 vertical-align 属性添加到您的规则中。在声明列表中键入 **vertical-align**，后跟冒号 (:)（代码 6.8）。

```css
vertical-align:
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_195_0.png)

ⓐ 不同的对齐类型。这些线仅作为指南显示。

| 值 |
| --- |
| super |
| sub |
| baseline |
| <relative> |
| <length> |
| <percentage> |

代码 6.8 添加到 text-properties.css 中——根据您想要的结果，将 vertical-align 与相对值或绝对值一起使用 ➋。

```css
/* text-properties.css ***/
h2 .chaptertitle {
  vertical-align: super; }
.pageheader h2 cite {
  vertical-align: -.6em; }
```

