
![](img/5a907eb39993e80f28c82efc2e4632b3_94_0.png)

图 6-4：为《赫芬顿邮报》网站设置样式的 CSS 规则。

![](img/5a907eb39993e80f28c82efc2e4632b3_94_1.png)

图 6-5：更改 CSS 会改变标题的颜色。

## 常见 CSS 任务和选择器

尽管 CSS 包含 150 多个属性，每个属性又有许多值，但在现代网站上，少数 CSS 属性和值完成了大部分工作。在上一节中，当你“修改”一个在线网站的 CSS 时，你更改了标题颜色——这是 CSS 中的常见任务。使用 CSS 执行的其他常见任务包括：

- 更改字体大小、样式、字体族和装饰
- 自定义链接，包括颜色、背景颜色和链接状态
- 添加背景图像并格式化前景图像

## 字体体操：大小、颜色、样式、字体族和装饰

CSS 让你可以控制许多 HTML 元素中的文本。表 6-1 显示了最常见的与文本相关的 CSS 属性和值。我将在后续各节中更全面地描述这些属性和值。

**表 6-1. 用于设置文本样式的常见 CSS 属性及值**

| 属性名 | 可能的值 | 描述 |
|---|---|---|
| `font-size` | `pixels (#px)`<br>`%`<br>`em (#em)` | 指定文本大小，可以用像素、包含元素字体大小的百分比，或用 em 值来度量；em 值通过所需像素值除以包含元素的字体大小（以像素为单位）计算得出。示例：`font-size: 16px;` |
| `color` | `name`<br>`hex code`<br>`rgb value` | 使用名称（`color: blue;`）、十六进制代码（`color: #0000FF;`）或 RGB（红、绿、蓝）值（`color: rgb(0,0,255);`）更改文本颜色。 |
| `font-style` | `normal`<br>`italic` | 将字体设置为斜体（或不设置）。 |
| `font-weight` | `normal`<br>`bold` | 将字体设置为粗体（或不设置）。 |
| `font-family` | `font name` | 设置字体字样。示例：`font-family: "serif";` |
| `text-decoration` | `none`<br>`underline`<br>`line-through` | 设置字体是否带下划线或删除线。 |

```css
:root {
  --c-brand: #3081d0;
  --c-brand-light: #509acd;
  --c-border: #eee;
  --c-bg: #ffffff;
  --c-bg-dark: #1e1e1e;
  --c-scrollbar: #ddd;
  --c-text: #2c3e50;
  --c-text-light: #476582;
  --c-text-lighter: #8e9bab;
  --c-code-bg: #f7f7f7;
  --c-code-text: #2c3e50;
}

.dark {
  --c-brand: #3081d0;
  --c-brand-light: #509acd;
  --c-border: #444;
  --c-bg: #1e1e1e;
  --c-bg-dark: #1e1e1e;
  --c-scrollbar: #444;
  --c-text: #cfd3dc;
  --c-text-light: #9a9a9a;
  --c-text-lighter: #8e9bab;
  --c-code-bg: #282c34;
  --c-code-text: #cfd3dc;
}
```

- **十六进制代码：** 颜色可以由红、绿、蓝分量来定义，使用十六进制代码时可引用超过 1600 万种颜色。在代码示例中，我将 `h1` 的颜色设置为 `#FF0000`。在井号之后，前两位（`FF`）表示颜色中的红色，接下来两位（`00`）表示绿色，最后两位（`00`）表示蓝色。
- **RGB 值：** 与十六进制代码一样，RGB 值指定超过 1600 万种颜色的红、绿、蓝分量。RGB 值是与十六进制值等价的十进制表示。

![](img/5a907eb39993e80f28c82efc2e4632b3_97_0.png)

不必担心要记住十六进制代码或 RGB 值。你可以使用在线颜色选择器轻松识别颜色，例如 www.w3schools.com/tags/ref_colorpicker.asp 上的选择器。

以下示例显示了全部三种颜色更改方式：

```css
p {
  color: red
}
h1 {
  color: #FF0000
}
li {
  color: rgb(255,0,0)
}
```

`li` 是有序列表或无序列表中列表项的元素名称。

![](img/5a907eb39993e80f28c82efc2e4632b3_97_1.png)

上面代码示例中的三种颜色都引用同一种红色色调。有关可按名称引用的颜色完整列表，请参见：www.w3.org/TR/css3-color/#svg-color。

![](img/5a907eb39993e80f28c82efc2e4632b3_97_2.png)

### 设置 font-style 和 font-weight

`font-style` 属性可将文本设置为斜体，`font-weight` 属性可将文本设置为粗体。对于这些属性中的每一个，默认值都是 normal，无需指定。在下面的示例中，段落被设置为字体呈斜体且粗体。以下是每个属性的示例：

```css
p {
  font-style: italic;
  font-weight: bold;
}
```

### 设置 font-family

`font-family` 属性设置用于文本的字体字样。该属性可设置为一个字体，或设置为以逗号分隔的字体列表。你的网站访问者的计算机上会安装各种不同的字体，但 `font-family` 属性仅当指定字体已安装在他们的系统上时才显示该字体。

`font-family` 属性可设置为两类值：

- **字体名称：** 特定字体名称，如 Times New Roman、Arial 和 Courier。
- **通用字体族：** 现代浏览器通常为每个通用字体族定义一种已安装字体。这五个通用字体族包括：
  - `serif` (Times New Roman, Palatino)
  - `sans-serif` (Helvetica, Verdana)
  - `monospace` (Courier, Andale Mono)
  - `cursive` (Comic Sans, Florence)
  - `fantasy` (Impact, Oldtown)

使用 `font-family` 时，最好定义两到三种特定字体，后跟一个通用字体族作为回退，以防指定的字体未安装，如下例所示：

```css
p {
    font-family: "Times New Roman", Helvetica, serif;
}
```

在此示例中，段落的字体族定义为 Times New Roman。如果用户的计算机上未安装 Times New Roman，浏览器会使用 Helvetica。如果未安装 Helvetica，浏览器将使用通用 serif 字体族中任何可用的字体。

![](img/5a907eb39993e80f28c82efc2e4632b3_98_0.png)

当使用包含多个单词的字体名称（如 Times New Roman）时，请将字体名称括在引号中。

### 设置 text-decoration

`text-decoration` 属性设置字体的任何下划线或删除线。默认情况下，该属性等于 none，无需指定。在以下示例中，任何带有 h1 标题的文本都会加下划线，而段落标签内的任何文本都会添加删除线：

```css
h1 {
    text-decoration: underline;
}
p {
    text-decoration: line-through;
}
```

## 自定义链接

通常，浏览器将链接显示为蓝色带下划线文本。最初，这种默认行为最大程度地减少了页面内容与交互式链接之间的混淆。如今，几乎所有网站都以自己的方式设置链接样式。有些网站不给链接加下划线；另一些网站保留下划线，但使用蓝色以外的颜色设置链接样式，等等。

![](img/5a907eb39993e80f28c82efc2e4632b3_99_0.png)

HTML 锚元素（a）用于创建链接。开始和结束锚标签之间的文本是链接描述，而 `href` 属性中设置的 URL 是单击链接时浏览器访问的地址。

锚标签随时间演变，如今有四种状态：

- **链接：** 用户尚未单击或访问过的链接。
- **已访问：** 用户已单击或访问过的链接。
- **悬停：** 用户将鼠标光标悬停在其上但未单击的链接。
- **活动：** 用户已开始单击但尚未释放鼠标按钮的链接。

CSS 可以为这四种状态分别设置样式，最常使用表 6-2 中显示的属性和值。

**表 6-2. 用于设置链接样式的常见 CSS 属性及值**

| 属性名 | 可能的值 | 描述 |
|---|---|---|
| `color` | `name`<br>`hex code`<br>`rgb value` | 使用名称（`color: blue;`）、十六进制代码（`color: #0000FF;`）或 RGB 值（`color: rgb(0,0,255);`）指定链接颜色。 |
| `text-decoration` | `none`<br>`underline` | 设置链接是否带下划线。 |

以下示例以类似于维基百科文章中链接样式的方式设置链接：默认情况下链接显示为蓝色，鼠标悬停时加下划线，活动时显示为橙色。如图 6-6 所示，第一个指向美国首席技术官的链接显示为下划线，就像我的鼠标正悬停在其上一样。此外，指向 Google 的链接显示为橙色，就像它处于活动状态且我的鼠标正在单击它一样。

