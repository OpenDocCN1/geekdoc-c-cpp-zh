
- `Duration`（时长）设置了过渡从开始到结束所需的时间，通常以秒为单位（表 12.12）。这是可选的，默认值为 0。
- `Timing Function`（计时函数）定义了过渡速度随进度变化的行为（表 12.13）。该值不是必须的，未设置时默认为线性（`linear`）。
- `Delay`（延迟）指定在开始之前应暂停多长时间（表 12.14）。这是可选的，未设置时默认为 0。

见下一页

| Value | 兼容性 |
| --- | --- |
| `<time>` | FF4, S3.1, C10.5, CSS3 |

# 表 12.12 过渡时长值

![](img/9cd61ac1d4015ed5688d0c411434a660_342_0.png)

| Value | 工作原理 |
| --- | --- |
| `cubic-bezier(<number>x)` | X 和 Y 值在 0 到 1 之间变化，以定义计时函数的贝塞尔曲线形状。 |
| `linear` | 恒速 |
| `ease` | 逐渐减速 |
| `ease-in` | 加速 |
| `ease-out` | 减速 |
| `ease-in-out` | 加速后减速 |

# 表 12.13 过渡计时函数值

当用户将指针悬停在图像上时，它会随时间过渡，并从缩略图位置动画到全屏展示。这包含了旋转、颜色和透明度的变化。

| Value | 兼容性 |
| --- | --- |
| `<time>` | FF4, S3.1, C10.5, CSS3 |

# 表 12.14 过渡延迟值

当用户将指针悬停在图像上时，它会随时间过渡，并从缩略图位置动画到全屏展示。这包含了旋转、颜色和透明度的变化。

# 通用选择器

# 带有过渡效果的属性

> 示例使用了通用选择器，但你可以根据需要添加。

# CSS3 新特性：在元素状态之间添加过渡 ★

尽管人们期望屏幕上会有变化和移动，但 CSS 和 HTML 很少有允许你设计交互的控制手段，而现有的手段到为止都是二元化的：

- 链接要么是一种颜色，要么是另一种颜色。
- 文本框要么是某种尺寸，要么是另一种。
- 照片要么是透明的，要么是不透明的。

过去，从一个状态到另一个状态没有任何中间过程。没有过渡效果。
这导致大多数网页在视觉上非常突兀，元素的移动和变化方式非常不优雅。

我们需要一种快速简便的方法来为页面添加简单的过渡效果，这正是 CSS 过渡（CSS transitions）大显身场的地方。

## 什么可以过渡？

几乎任何具有颜色、长度或位置组件的 CSS 属性——包括许多新的 CSS3 属性——都可以设置过渡，使其随时间推移从一种样式变为另一种样式。

表 12.9 显示了可用的 CSS 属性列表以及可以过渡的值。唯一的例外是盒投影（`box-shadows`）。

要发生过渡，元素必须发生状态变化，即使用第 3 章讨论的链接伪类或动态伪类。过渡的实现原理是在一段时间内改变不同元素状态之间的样式。例如，元素默认状态的颜色值在显示为悬停（`hover`）状态的颜色值之前，会经过光谱中的中间色值。

![](img/9cd61ac1d4015ed5688d0c411434a660_339_0.png)

> 过渡就像电影中的几帧，随着时间逐渐变化，而不是瞬间完成。

# 表 12.9 带有过渡效果的 CSS 属性

| CSS 属性 | 可过渡类型 | CSS 属性 | 可过渡类型 |
| :--- | :--- | :--- | :--- |
| `background-color` | 颜色 | `margin-right` | 长度 |
| `background-image` | 仅渐变 | `margin-top` | 长度 |
| `background-position` | 百比、长度 | `max-height` | 长度、百分比 |
| `border-bottom-color` | 颜色 | `max-width` | 长度、百分比 |
| `border-bottom-width` | 长度 | `min-height` | 长度、百分比 |
| `border-color` | 颜色 | `min-width` | 长度、百分比 |
| `border-left-color` | 颜色 | `opacity` | 数字 |
| `border-left-width` | 长度 | `outline-color` | 颜色 |
| `border-right-color` | 颜色 | `outline-offset` | 整数 |
| `border-right-width` | 长度 | `outline-width` | 长度 |
| `border-spacing` | 长度 | `padding-bottom` | 长度 |
| `border-top-color` | 颜色 | `padding-left` | 长度 |
| `border-top-width` | 长度 | `padding-right` | 长度 |
| `border-width` | 长度 | `padding-top` | 长度 |
| `bottom` | 长度、百分比 | `right` | 长度、百分比 |
| `color` | 颜色 | `text-indent` | 长度、百分比 |
| `crop` | 矩形 | `text-shadow` | 投影 |
| `font-size` | 长度、百分比 | `top` | 长度、百分比 |
| `font-weight` | 数字 | `transform` | 数字、角度、宽度 |
| `grid-*` | 各种 | `vertical-align` | 关键字、长度、百分比 |
| `height` | 长度、百分比 | `visibility` | 可性 |
| `left` | 长度、百分比 | `width` | 长度、百分比 |
| `letter-spacing` | 长度 | `word-spacing` | 长度、百分比 |
| `line-height` | 数字、百分比 | `z-index` | 整数 |
| `margin-bottom` | 长度 | `zoom` | 数字 |
| `margin-left` | 长度 | | |

*表 12.9

# 代码 12.4 续

```
-o-transform: scale(.75) rotate(10deg);

transform: scale(.75) rotate(10deg);

#f2 {

  -webkit-transform: perspective(250)

  scale3d(5,75,1.5) rotate3d(-3,10,-8,18deg);

  -moz-transform: scale(.75) rotate(-8deg);

  -o-transform: scale(.75) rotate(-8deg);

  transform: scale(.75) rotate(-8deg);

}

#f3 {

  -webkit-transform: perspective(250)

  scale3d(1,5,5) rotate3d(3,6,10,20deg);

  -moz-transform: scale(.75) rotate(3deg);

  -o-transform: scale(.75) rotate(3deg);

  transform: scale(.75) rotate(3deg);

}

#f1:hover, #f2:hover, #f3:hover {

  opacity: 1;

  -webkit-transform: rotate(0);

  -moz-transform: rotate(0);

  -o-transform: rotate(0);

transform: rotate(0);

  cursor: pointer;

  clip: auto;

  z-index: 9999;

}
```

- `Duration`（时长）设置了过渡从开始到结束所需的时间，通常以秒为单位（表 12.12）。这是可选的，默认值为 0。
- `Timing Function`（计时函数）定义了过渡速度随进度变化的行为（表 12.13）。该值不是必须的，未设置时默认为线性（`linear`）。
- `Delay`（延迟）指定在开始之前应暂停多长时间（表 12.14）。这是可选的，未设置时默认为 0。

见下一页

| Value | 兼容性 |
| --- | --- |
| `<time>` | FF4, S3.1, C10.5, CSS3 |

# 表 12.12 过渡时长值

![](img/9cd61ac1d4015ed5688d0c411434a660_342_0.png)

| Value | 工作原理 |
| --- | --- |
| `cubic-bezier(<number>x)` | X 和 Y 值在 0 到 1 之间变化，以定义计时函数的贝塞尔曲线形状。 |
| `linear` | 恒速 |
| `ease` | 逐渐减速 |
| `ease-in` | 加速 |
| `ease-out` | 减速 |
| `ease-in-out` | 加速后减速 |

# 表 12.13 过渡计时函数值

当用户将指针悬停在图像上时，它会随时间过渡，并从缩略图位置动画到全屏展示。这包含了旋转、颜色和透明度的变化。

| Value | 兼容性 |
| --- | --- |
| `<time>` | FF4, S3.1, C10.5, CSS3 |

# 表 12.14 过渡延迟值

当用户将指针悬停在图像上时，它会随时间过渡，并从缩略图位置动画到全屏展示。这包含了旋转、颜色和透明度的变化。

# 通用选择器

> 示例使用了通用选择器，但你可以根据需要添加。

# 下划线技巧 (The underscore hack)

所谓的 hack 是指那些本不应该起作用但在某些情况下确实有效，并且可以被利用来解决特定问题的代码。虽然有几种 hack 允许我们包含仅在 Internet Explorer 中生效的 CSS，但我认为最易用且最可靠的 hack 是下划线技巧。

# 使用渐进增强进行设计

显而易见，并非所有浏览器都是平等的，那么我们为什么要期望所有网站都那样对待它们呢？多年来，Web 设计师一直尝试按照最低标准（IE）进行设计，忽略了可用的新功能，因为他们认为必须在所有浏览器中创建完全相同的体验。只要网站运行良好并且尽可能地完美，为什么不利用新功能呢？这是一个 Web 设计师多年来一直反复争论的问题。使用渐进增强最好的理由可以归结为客户的期望：

- 1. 开发更快——与其花时间拼凑大量图像来实现圆角、阴影和其他效果，只需几行代码就能搞定。
- 2. 维护成本更低——修改代码比重新制作、重新裁剪和重新部署图像有效得多。
- 3. 视觉效果更好——由于样式是浏览器原生的，它们的显示会比硬塞进去图像更精确。

如果这些论点不能说服你的客户，就向他们展示使用渐进增强的对比。通常这足以说服即使是最固执的客户。下划线技巧是为 Internet Explorer 浏览器包含 CSS 的简单方法，它利用了 CSS 声明开头处理方式上的一个错误。根据标准，任何以下划线开头的声明都应该被忽略，就像被注释掉一样。然而，微软创建早期版本的 Internet Explorer 时显然没有收到通知，任何处于兼容模式下的 Internet Explorer 版本都会关注此声明。我们可以利用这一点来修复。

# 下划线

下划线技巧的通用语法。位于 Internet Explorer 之外的浏览器会忽略同一行的 CSS。符合标准的浏览器将根据浏览器使用 640px 到 980px 之间的范围，而 IE 将始终使用 800px，因为它不支持 max/min-width。这可以应用于任何需要不同属性或取值的场景。

# 如何使用 IE 下划线技巧：

- 1. 在 CSS 规则中添加符合标准的声明。
- 2. 添加带有前下划线 (`_`) 的 IE 特有声明。该值将覆盖任何浏览器中该属性之前的值。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>爱丽丝在仙境游</title>
  <style type="css">
    {
      padding: 10px;
      margin: 10px auto;
      max-width: 980px;
      min-width: 640px;
      width: 100%;
      _width: 800px;
      outline: 1px solid red;
      border: 1px solid red;
    }
  </style>
</head>
<body>
  <p>她突然来到,...</p>
  <p>爱丽丝打开门,...</p>
  <p>那里似乎有...</p>
</body>
</html>
```

她突然看到一张三条腿的桌子，全由实心玻璃制成；上面除了一把金钥匙外，什么也没有，爱丽丝的第一反应是这钥匙属于大厅里的某扇门之一；但遗憾的是，要么锁太大，要么钥匙太小，无论如何都打不开其中任何一扇。然而，在第二轮寻找中，她发现了一道之前没有注意到的帘子，后面是一扇约十五英寸高的小门；她尝试将金钥匙插入锁中，让她非常高兴的是，钥匙契合了！

爱丽丝打开门，发现它通向一条狭窄的走廊，没鼠洞大不了；她蹲下身，顺着走廊望去，那里有一个她见过最美丽的花园。她多想离开那个阴暗的大厅，在那些花朵和凉爽的喷泉间漫步，但她的头无法穿过门框；爱丽丝想，即使她能过去，没有肩膀也大派不上用。噢，我多希望我能像折叠远镜一样收起来啊，我希望我能，只要我不知道从何开始。因为，你知道，最近发生了这么多奇怪的事情，爱丽丝已经开始认为没有什么是不可能的。

看来对那扇小门许愿没用，她回到桌子旁，半希望能在上面找到另一把钥匙，或者至少找到一本能像折叠远镜一样把人收起来的规则书，这次她在桌上发现一个小瓶子（这让爱丽丝非常惊讶），瓶颈上贴着纸标签，上面漂亮地印着大号的“喝掉我”字样。

Firefox 中的代码 13.1。使用 `width` 将扩展和收缩宽度。

她突然看到一张三条腿的桌子，全由实心玻璃制成；上面除了一把金钥匙外，什么也没有，爱丽丝的第一反应是这钥匙属于大厅里的某扇门之一；但，遗憾的是，要么锁太大，要么钥匙太小，无论如何都打不开其中任何一扇。然而，在第二轮寻找中，她发现了一道之前没有注意到的帘子，后面是一扇约十五英寸高的小门；她尝试将金钥匙插入锁中，让她非常高兴的是，钥匙契合了！

爱丽丝打开门，发现它通向一条狭窄的走廊，没鼠洞大不了；她蹲下身，顺着走廊望去，那里有一个她见过最美丽的花园。她多想离开那个阴暗的大厅，在那些花朵和凉爽的喷泉间漫步，但她的头无法穿过门框；爱丽丝想，即使她能过去，没有肩膀也大派不上用。噢，我多希望我能像折叠远镜一样收起来啊，我希望我能，只要我不知道从何开始。因为，你知道，最近发生了这么多奇怪的事情，爱丽丝已经开始认为没有什么是不可能的。

# IE 条件 CSS

Internet Explorer（仅限 Internet Explorer）具有解释条件语句（如果这个……那么那个）的能力，而其他浏览器会忽略这些语句。这允许你插入样式表链接，为任何版本定制你的 CSS。要为 Internet Explorer 设置条件样式：

- 1. 添加你符合标准的 CSS。这可以嵌入文档头部的 `<style>` 标签中，或者使用 `<link>` 标签或 `@import` 规则导入（代码 13.2）：
- 2. 添加条件注释，指定你想针对 IE 版本。

```html
<!-- IE 版本 -->
<!--[if IE]>
<link href="ie.css" rel="stylesheet">
<!--[endif]-->
```

表 13.1 IE 条件

| IE | 任何版本的 IE |
|---|---|
| IE `<version>` | 小于版本的 IE |
| lte IE `<version>` | 小于等于版本的 IE |
| IE `<version>` | 特定版本 |
| gte IE `<version>` | 大于等于版本的 IE |
| gt IE `<version>` | 大于版本的 IE |

仅使用 IE 将适用于任何版本的 Internet Explorer。在空格后加一个数字将指定版本号。例如，IE 6 无论文档类型如何，都允许在 Internet Explorer 6 中使用 CSS。

328 第 13 章

3. 按照浏览器版本（或多个版本）添加 IE 特有的 CSS。此值将覆盖标准 CSS 中该属性的先前值。可以使用 `<style>` 标签将其嵌入文档的头部中，或者使用 `<link>` 标签或 `@import url(ie-fix.css);` 进行导入。

提示：由于 IE9 对 HTML5 和 CSS3 具有很好的兼容性，我建议将您的 IE 条件设置为“直到 IE 8”，这将使覆盖设置仅适用于小于或等于 8 的 Internet Explorer 版本。

提示：虽然你可以为不同版本的 Internet Explorer 添加特定代码，但请尝试尽量将链接和导入的数量减少到最低。引入的额外文件越多，您的网页加载时间就越长。

4. 关闭条件注释。使用带括号的 `endif` 关闭您的条件注释：`[endif]-->`

代码 13.2 来源于第 12 章的最终 HTML 现在包含一个指向为 Internet Explorer 定制的特殊 CSS 文件的链接 (12.3) 只有当浏览器版本为 IE8 或更低时才会添加。`library.css` 文件（未显示）将第 5-12 章的所有 CSS 合并到了一个文件中。

```html
<!-- HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http="Content-Type" content="text/html; charset=UTF-8">
  <title>爱丽丝梦仙游</title>
  <link href="../library.css" type="text/css" rel="stylesheet">
  <!--[if IE 8]-->
  <script src="../script/HTML5.js" type="text/javascript"></script>
```
