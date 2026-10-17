
color:(102,0,0);

```
2. 指定颜色值。根据表 7.5 中的颜色值输入颜色值。这包括 RGB、HSL、transparent 或当前颜色。
3. 根据需要添加带有通道道的颜色。如果你想让颜色部分透明，可以在颜色值下方再次添加 RGBA 或 HSVA 值。对于不支持 alpha 值的浏览器，第一个颜色
```

*** CSS ***

```
body {

  color: (102,0,0);

}

h1 {

  color: (102,0,0);

}

h2 {

  color: (102,0,0);

}

article p {

  color: (102,0,0);

}

a {

  color: (102,0,0);

}

a:visited {

  color: (102,0,0);

}

a:hover {

  color: (102,0,0);

}

a:active {

  color: (102,0,0);

}

byline {

  color: (102,0,0);

}

byline .author {

  color: (102,0,0);

}
```

### 表 7.5 颜色值

| 值 | 兼容性 |
|---|---|
| `<color>` | IE3, FF1, O3 |
| `<inherit>` | IE3, FF1, O3 |

> TIP 为 `body` 标签设置默认颜色是一个好习惯，以确保跨页面颜色的一致性。

> TIP 在选择前景颜色时要小心——前景和背景亮度差异越小，读者的眼睛就越累。

![](img/9cd61ac1d4015ed688d0c41143a660_220.png)

> TIP 颜色变化是显示超链接状态的一种重要方式，但绝不是链接的唯一样式。第 14 章将向你展示链接、导航和控件的最佳实践。

## 设置背景颜色

在 HTML 页面上设置背景色的功能几乎从第一代 Web 浏览器出现起就有了。然而，通过 CSS，你不仅可以为整个页面定义背景，还可以使用 `background-color` 属性为单个元素定义背景（表 7.6）。不过，与 `color` 属性不同，背景颜色仅应用于元素本身，而不会被其子元素直接继承。尽管如此，由于它们位于父元素内部这一事实，它们将显示在那个背景之上。

代码示例 7.3 color-background-properties。
- css—背景颜色可以设置为实色、透明色或使用渐变。

```css
*** CSS3 V8 | Chapter 7 |
- color-background-properties.css ***
{
  padding: 0;
  margin: 0;
  border: none;
}
body {
  color: rgb(51,51,51);
  background-color: rgb(85,85,85);
}
```

```css
header.page {
  display: block;
  background-color: rgb(102,0,0);
}
```

## 定义元素的背景颜色：

```css
h1 {
  color: rgb(255,225,225);
  background-color: rgba(255,225,225,65);
}
```

- 1. 添加 `background-color` 属性。通过在声明中设置颜色，可以设置背景（代码 7.3）。

```css
div {
  background-color: rgb(85,85,85);
}
```

- 2. 指定颜色值。颜色可以使用名称、RGB、RGBA 或十六进制值。

```css
div {
  background-color: transparent;
}
```

- 3. 根据需要添加背景渐变。针对不同的浏览器（Internet Explorer、Webkit、Mozilla）使用不同的声明。

```css
div {
  background: linear-gradient(to bottom, #555, #333);
}
/* Webkit 浏览器 */
div {
  background: -webkit-linear-gradient(to bottom, #555, #333);
}
/* Mozilla 浏览器 */
div {
  background: -moz-linear-gradient(to bottom, #555, #333);
}
```

```css
background-image: url(../images/alice02b.png);
background-repeat: no-repeat;
background-position: center center;
-o-background-size: contain;
-moz-background-size: contain;
webkit-background-size: contain;
background-size: contain;
-o-background-clip: padding-box;
-moz-background-clip: padding;
webkit-background-clip: padding-box;
background-size: padding-box;
-o-background-origin: padding-box;
-moz-background-origin: padding;
webkit-background-origin: padding-box;
background-origin: padding-box; }
footer {
display: block;
background: rgb(153,153,153);
filter: progid:ImageTransform.Microsoft.gradient(startColor="#ffffff",endColor="#000000");
background: -webkit-background-gradient(linear, left top, left bottom, from(rgba(0,0,0,0)), to(rgba(0,0,0,.5)));
background: -moz-linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,.5)); }
a:link {
color: rgb(204,0,0) }
a:visited {
color: rgb(153,0,0) }
a:hover {
color: rgb(255,0,0) }
a:active {
color: rgb(153,153,153) }
.byline {
color: rgba(255,255,255,.5); }
.byline .author {
color: rgba(255,255,255,.75) }
```

## 表 7.8 背景重复值 (Background-Repeat Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| repeat | IE4, FF1, S1, C1, O3, CSS1 |
| repeat-x | IE4, FF1, S1, C1, O3, CSS1 |
| repeat-y | IE4, FF1, S1, C1, O3, CSS1 |
| no-repeat | IE4, FF1, S1, C1, O3, CSS1 |
| space | FF3.6, CSS3 |
| round | FF3.6, CSS3 |

2. 添加背景重复属性，并指定背景应如何平铺（或不进行平铺）。输入 `background-repeat`，后跟一个冒号 (:)：

```css
background-repeat: repeat;
```

然后，通过输入以下选项之一（表 7.8）来定义你希望背景如何重复：

-   *repeat* 指令浏览器在水平方向和垂直方向上在整个背景中平铺该图形。如果省略该属性，则为默认值。
-   *repeat-x* 指令浏览器仅在水平方向上平铺背景图形，使图形在元素顶部沿一条平直的水平线重复。
-   *repeat-y* 指令浏览器仅在垂直方向上平铺背景图形，使图形在元素左侧沿一条平直的垂直线重复。
-   *no-repeat* 使背景图形仅出现一次（不进行平铺）。

3. 添加背景附加属性（background-attachment），并指定背景应如何随元素滚动。输入 `background-attachment`，后跟一个冒号 (:)：

```css
background-attachment: fixed;
```

然后，通过输入以下选项之一（表 7.9）来定义你希望在页面滚动时如何处理背景：

-   *scroll* 指令背景图形随元素一起滚动。如果省略该属性，则为默认值。
-   *fixed* 指令浏览器不要随元素的其余部分滚动背景内容。然而，它会随父元素滚动。
-   *local* 与 *fixed* 类似，但背景固定在元素的内容上，而不是元素本身。

4. 添加背景位置属性（background-position），并指定背景的位置。输入 `background-position`，后跟一个冒号 (:)：

```css
background-position: -10px;
```

然后，输入一个值或两个用空格分隔的值，以指示你希望背景相对于元素左上角出现的位置。如果输入一个值，则用于 x 轴，而 y 轴将居中。使用以下之一（表 7.10）：

## 表 7.9 背景附加值 (Background-Attachment Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| scroll | IE4, FF1, S1, C1, O3, CSS1 |
| fixed | IE4, FF1, S1, C1, O3, CSS1 |
| local | S2, C1, O3.5, CSS3 |

## 表 7.10 背景位置值 (Background-Position Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| <length> | IE4, FF1, S1, C1, O3, CSS1 |
| <percentage> | IE4, FF1, S1, C1, O3, CSS1 |
| top | IE4, FF1, S1, C1, O3, CSS1 |
| bottom | IE4, FF1, S1, C1, O3, CSS1 |
| left | IE4, FF1, S1, C1, O3, CSS1 |
| right | IE4, FF1, S1, C1, O3, CSS1 |
| center | |

## 表 7.11 背景尺寸值 (Background-Size Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| <length> | IE4, FF1, S1, C1, O3, CSS1 |
| <percentage> | IE4, FF1, S1, C1, O3, CSS1 |
| cover | FF3.6, CSS3 |
| contain | FF3.6, CSS3 |

Safari 5 支持背景-size size -webkit-size
Firefox 支持 -moz-size
Safari 4 和 Chrome 3 支持 -webkit-size

-   长度值，例如 10px。
-   百分比值，例如 25%。第一个百分比指示元素宽度，第二个百分比指示元素的高度。
-   *cover* 按比例缩放背景以覆盖整个区域。
-   *contain* 按比例缩放背景以适应区域并保持完整显示。

5. 添加背景尺寸属性（background-size），并指定精确尺寸、百分比或方法。输入 `background-size`，后跟一个冒号 (:)：

```css
background-size: contain;
-moz-background-size: contain;
-webkit-background-size: contain;
```

然后，输入表 7.11 中的值。可以包含两个值以定义不同的 x 和 y 尺寸：

-   百分比值，例如 25%。第一个百分比指示元素宽度，第二个百分比指示元素的高度。
-   英语关键字，如：`top`、`bottom`、`left`、`right` 或 `center`。

6. 添加背景裁剪属性（background-clip），并指定裁剪方法。输入 `background-clip`，后跟一个冒号 (:)：

```css
-o-background-clip: padding-box;
-moz-background-clip: padding;
-webkit-background-clip: padding-box;
background-clip: padding-box;
```

然后，输入表 7.12 中的值。可以包含两个值以定义不同的 x 和 y 尺寸。Mozilla 和 Webkit 的语法与标准略有不同：

-   *border/border-box* 将图像裁剪到边框边缘。
-   *padding/padding-box* 将图像裁剪到内边框边缘。
-   *content/content-box* 将图像裁剪到内容边缘。

## 表 7.12 背景裁剪值 (Background-Clip Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| padding | IE4, FF1, S1, C1, O3, CSS1 |
| border | IE4, FF1, S1, C1, O3, CSS1 |
| content | S3, C3 |
| padding-box | S3/S5, C3, O10.5 |
| border-box | S3/S5, C3, O10.5 |

Firefox -moz-clip
Safari 4 和 Chrome 3 支持 -webkit-clip
Safari 5 支持背景-clip

## 表 7.13 背景起始值 (Background-Origin Values)

| 值 (Value) | 兼容性 (Compatibility) |
|--- |--- |
| padding | IE4, FF1, S1, C1, O3, CSS1 |
| border | IE4, FF1, S1, C1, O3, CSS1 |
| content | IE4, FF1, S1, C1, O3, CSS1 |
| padding-box | S3/S5, C3, O10.5 |
| border-box | S3/S5, C3, O10.5 |
| content-box | S3/S5, C3, O10.5 |

7. 添加背景起始属性（background-origin），并指定起始方法。输入 `background-origin`，后跟一个冒号 (:)：

```css
-o-background-origin: padding-box;
-moz-background-origin: padding;
-webkit-background-origin: padding-box;
background-origin: padding-box;
```

Firefox -moz-background-origin
Safari 4 和 Chrome 3 支持 -webkit-background-origin
Safari 5 支持背景-origin

然后输入表 7.13 中的值。可以包含两个值以定义不同的 x 和 y 尺寸。

8. 最后，指定应用上述属性的背景图像。要分层背景图像，请在逗号分隔的列表中添加每个值。列表中的图像将放在之前图像下方，所有图像下方都有背景颜色。请确保根据需要为所有属性添加所有值。

```css
background-image: url(../images/embellish-01.png), url(../images/paper-01.jpg);
```

# 使用背景简写属性

背景简写属性（表 7.14）允许你为整个页面或单个元素定义背景图像和颜色，将许多背景属性合并为一个单一、快速且压缩的声明。从编码的角度来看，这种方法更优，因为它占用的空间更少，但它要求你记住列表中每个值的用途。

```css
Code 7.5 color-background-properties.css
尽管结果与代码 7.4 相同，但这个版本更加紧凑，更容易扫描，并减小了文件大小。如果你想查看页面的外观，请查看前面的节。
```

```css
*** 第 7 章 | color-background-properties.css ***
body {
  color: rgb(51,51,51);
  background: rgb(85,85,85) url(../images/dark-victorian.jpg) repeat fixed;
}
```

定义背景：
- 向你的 CSS 规则声明中添加 `background` 属性。通过输入 `background` 开始声明，后跟一个冒号（:)：然后定义一个背景值（代码 7.5）。

```css
header {
  display: block;
  background: url(../images/bg-spine.png) no-repeat center top,
  rgb(102,0,0) url(../images/bg-spine.jpg) repeat-x 0;
}
```

```css
h1 {
  color: rgb(255,225,215);
