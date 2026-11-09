
```css
a:link {
    color: rgb(6,69,173);
    text-decoration: none;
}
a:visited {
    color: rgb(11,0,128);
}
a:hover {
    text-decoration: underline;
}
a:active {
    color: rgb(250,167,0);
}
```

![](img/5a907eb39993e80f28c82efc2e4632b3_100_0.png)

记住在 a 选择器和链接状态之间要包含冒号。

![](img/5a907eb39993e80f28c82efc2e4632b3_100_1.png)

尽管解释原因超出了本书的范围，但 CSS 规范坚持要求你按照这里显示的顺序定义各种链接状态——link、visited、hover，然后是 active。不过，只要保留此顺序，不定义某个链接状态也是可以接受的。

各种链接状态称为*伪类选择器*。伪类选择器向 CSS 选择器添加关键字，并允许你为所选元素的特殊状态设置样式。

![](img/5a907eb39993e80f28c82efc2e4632b3_100_2.png)

**图 6-6：** Wikipedia.org 页面显示 link、visited、hover 和 active 状态。

## 添加背景图像并设置前景图像样式

你可以使用 CSS 在 HTML 元素后面添加背景图像。最常见的是，background-image 属性用于向 div、table 和 p 等单个 HTML 元素添加背景图像，或者（当应用于 body 元素时）向整个网页添加背景图像。

![](img/5a907eb39993e80f28c82efc2e4632b3_101_0.png)

文件大小较小的背景图像比更大的图像加载得更快。如果你的访问者经常使用移动手机浏览你的网站，而移动手机通常数据连接较慢，这一点尤其重要。

表 6-3 中的属性和值显示了添加背景图像的选项。

| 属性名 | 可能的值 | 描述 |
|---|---|---|
| `background-image` | `url("URL")` | 从 URL 指定的图像链接添加背景图像。 |
| `background-size` | `auto`<br>`contain`<br>`cover`<br>`width`<br>`height`<br>`(#px, %)` | 根据值设置背景尺寸：<br><br>`auto`（默认值）按图像原始尺寸显示图像。<br><br>`contain` 缩放图像的宽度和高度，使其适合元素内部。<br><br>`cover` 缩放图像，使整个背景图像无法全部显示。<br><br>还可以通过指定像素或百分比形式的宽度和高度来设置背景尺寸。 |
| `background-position` | `keywords`<br><br>`position`<br>(#px, %) | 使用关键字或精确位置在元素中定位背景。`Keywords` 由水平关键字（`left`、`right`、`center`）和垂直关键字（`top`、`center` 和 `bottom`）组成。还可以使用像素或百分比精确地定义背景的位置，以描述相对于元素的水平和垂直位置。 |
| `background-repeat` | `repeat`<br>`repeat-x`<br>`repeat-y`<br>`no-repeat` | 设置背景图像平铺（或重复）的方式如下：<br>水平方向（repeat-x）<br>垂直方向（repeat-y）<br>水平和垂直方向（repeat）<br>完全不重复（no-repeat）。 |
| `background-attachment` | `scroll`<br>`fixed` | 设置背景随其他内容滚动（scroll），或保持固定（fixed）。 |

### 设置背景图像

如下例所示，background-image 属性可以为整个网页或特定元素设置背景图像。

```css
body {
    background-image:
        url("http://upload.wikimedia.org/wikipedia/commons/e/e5/Chrysler_Building_Midtown_Manhattan_New_York_City_1932.jpg");
}
```

![](img/5a907eb39993e80f28c82efc2e4632b3_102_0.png)

你可以在 images.google.com、www.flickr.com 或 publicdomainarchive.com 等网站上找到背景图像。

![](img/5a907eb39993e80f28c82efc2e4632b3_102_1.png)

检查图像版权信息，确认你是否有权使用该图像，并遵守图像的许可条款，其中可能包括署名或标明作者。此外，直接链接到其他服务器上的图像称为热链接。最好下载图像，并在自己的服务器上托管和链接该图像。

![](img/5a907eb39993e80f28c82efc2e4632b3_102_2.png)

如果你希望使用单色背景而不是图像，请使用 background-color 属性。此属性的定义方式与 background-image 属性大致相同。只需将其设置为颜色名称、RGB 值或十六进制代码，如我在本章前面“设置颜色”一节中所述。

### 设置背景尺寸

通过使用像素或百分比指定精确尺寸，background-size 属性可以根据需要将背景图像缩放到更小或更大。此外，此属性有三个网页中常用的尺寸值，如下所示（见图 6-7）：

- **auto:** 此值保持图像的原始尺寸。
- **cover:** 此值缩放图像，使所有尺寸大于或等于容器或 HTML 元素的尺寸。
- **contain:** 此值缩放图像，使所有尺寸小于或等于容器或 HTML 元素的尺寸。

![](img/5a907eb39993e80f28c82efc2e4632b3_103_0.png)

**图 6-7：** 将背景尺寸设置为三个不同的值。

### 设置背景位置

background-position 设置背景图像的初始位置。默认初始位置位于网页或特定元素的左上角。你可以通过指定一对关键字或位置值来更改默认位置，如下所示：

- **Keywords:** 第一个关键字*（left、center 或 right）*表示水平位置，第二个关键字*（top、center 或 bottom）*表示垂直位置。
- **Position:** 第一个位置值表示水平位置，第二个值表示垂直位置。每个值使用像素或百分比定义，表示距浏览器或指定元素左上角的距离。例如，`background-position: center center` 等于 `background-position: 50% 50%`。（见图 6-8。）

### 设置背景重复

background-repeat 属性设置背景平铺的方向，如下所示：

- **repeat:** 此值（默认值）在水平和垂直方向重复背景图像。
- **repeat-x:** 此值仅在水平方向重复背景图像。
- **repeat-y:** 此值仅在垂直方向重复背景图像。
- **no-repeat:** 此值完全阻止背景重复。

![](img/5a907eb39993e80f28c82efc2e4632b3_104_0.png)

**图 6-8：** 使用关键字或位置指定的初始背景图像位置。

### 设置背景附着

background-attachment 属性设置当用户滚动页面内容时背景图像是否移动。该属性可以设置为：

- **scroll:** 用户滚动时背景图像移动。
- **fixed:** 用户滚动时背景图像不移动。

以下代码段使用前面讨论的几个属性来添加背景图像，该图像拉伸覆盖整个网页、居中对齐、不重复，并且用户滚动时不移动。（见图 6-9。）

```css
body {
    background-image: url("http://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/USMC-090807-M-8097K-022.jpg/640px-USMC-090807-M-8097K-022.jpg");
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
    background-attachment: fixed;
}
```

![](img/5a907eb39993e80f28c82efc2e4632b3_105_0.png)

**图 6-9：** 设置为整个页面背景的图像。

## 美化网页

本章讨论的 CSS 规则让你初步了解一些常见的样式属性和值。尽管你不太可能记住每一个属性和值，但通过练习，属性和值的名称会自然地浮现在你脑海中。理解基本语法后，下一步就是实际将 CSS 纳入你的网页，并尝试为 HTML 元素设置样式。

### 将 CSS 添加到 HTML 中

有三种方法可将 CSS 应用于网站，以为 HTML 元素设置样式：

- **内联 CSS:** CSS 可以在 HTML 文件中、在与它所设置样式的 HTML 元素相同的行上指定。此方法需要将 `style` 属性放在开始 HTML 标签内。通常，内联 CSS 是网站样式设置中最不受欢迎的方式，因为样式规则经常重复。以下是内联 CSS 的示例：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Record IPOs</title>
</head>
<body>
```
