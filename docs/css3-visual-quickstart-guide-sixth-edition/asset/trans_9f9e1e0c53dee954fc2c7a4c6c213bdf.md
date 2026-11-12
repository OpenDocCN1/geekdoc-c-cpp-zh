

| CSS 属性 | 过渡内容 | CSS 属性 | 过渡内容 |
| :--- | :--- | :--- | :--- |
| background-color | 颜色 | margin-left | 长度 |
| background-image | 仅渐变 | margin-right | 长度 |
| background-position | 百分比, 长度 | margin-top | 长度 |
| border-bottom-color | 颜色 | max-height | 长度, 百分比 |
| border-bottom-width | 长度 | max-width | 长度, 百分比 |
| border-color | 颜色 | min-height | 长度, 百分比 |
| border-left-color | 颜色 | min-width | 长度, 百分比 |
| border-left-width | 长度 | opacity | Alpha值 |
| border-right-color | 颜色 | outline-color | 颜色 |
| border-right-width | 长度 | outline-offset | 整数 |
| border-spacing | 长度 | outline-width | 长度 |
| border-top-color | 颜色 | padding-bottom | 长度 |
| border-top-width | 长度 | padding-left | 长度 |
| border-width | 长度 | padding-right | 长度 |
| bottom | 长度, 百分比 | padding-top | 长度 |
| color | 颜色 | right | 长度, 百分比 |
| clip | 矩形 | text-indent | 长度, 百分比 |
| font-size | 长度, 百分比 | text-shadow | 阴影 |
| font-weight | 数值 | top | 长度, 百分比 |
| grid | 各种 | vertical-align | 关键字, 长度, 百分比 |
| height | 长度, 百分比 | visibility | 可见性 |
| left | 长度, 百分比 | width | 长度, 百分比 |
| letter-spacing | 长度 | word-spacing | 长度, 百分比 |
| line-height | 数值, 长度, 百分比 | z-index | 整数 |
| margin-bottom | 长度 | zoom | 数值 |

## 在状态之间添加过渡效果：

- 1. 添加过渡属性。
- -webkit-transition:
- -moz-transition:
- -o-transition:
- transition:

包括Webkit、Mozilla、Opera浏览器扩展以及标准CSS3的版本，列表底部包含标准属性（代码12.4）。

代码12.4 添加到 transition-properties.css 中——当应用于代码12.1时，过渡现在应用于颜色、不透明度和变换，从而实现渐变而非即时变化。请注意，我还为图形添加了悬停状态。没有样式变化就不可能有过渡，添加变化的最简单方法是使用 :hover 伪类。

```css
/** transition-properties.css ***/
aside, figure, a {
-webkit-transition: color .25s ease-in,
opacity .5s ease, -webkit-transform
.25s ease-in-out 0;
-moz-transition: color .25s ease-in,
opacity .5s ease, -moz-transform .25s
ease-in-out 0;
-o-transition: color .25s ease-in,
opacity .5s ease, -o-transform .25s
ease-in-out 0;
transition: color .25s ease-in,
opacity .5s ease, transform .25s
ease-in-out 0; }
div.gallery figure#f1:hover, div.gallery
figure#f2:hover, div.gallery figure#f3:hover {
-webkit-transform: rotate(0);
-moz-transform: rotate(0);
-o-transform: rotate(0);
transform: rotate(0);
cursor: pointer; }
```

![](img/e1ed1e3c1873fa9fc855210fb83699d0_343_0.png)

使用缩放变换时，过渡是通过尺寸进行的。

## 表12.10 过渡值

| Value | |
|---|---|
| <transition-property> | ●10 ◇16 ◇ ◇ ◇ |
| <transition-duration> | ●10 ◇16 ◇ ◇ ◇ |
| <transition-timing-function> | ●10 ◇16 ◇ ◇ ◇ |
| <transition-delay> | ●10 ◇16 ◇ ◇ ◇ |

## 表12.11 过渡属性值

| Value | |
|---|---|
| <CSSPropertyTransition>* | ●10 ◇16 ◇ ◇ ◇ |
| none | ●10 ◇16 ◇ ◇ ◇ |
| all | ●10 ◇16 ◇ ◇ ◇ |

*参见表12.9*

## 表12.12 过渡持续时间值

| Value | |
|---|---|
| <time> | ●10 ◇16 ◇ ◇ ◇12.5 |

## 表12.13 过渡计时函数值

| Value | 工作原理 |
|---|---|
| cubic-bezier (<number>...) | X和Y值在0到1之间，用于定义计时函数所用的贝塞尔曲线形状。 |
| linear | 恒定速度 |
| ease | 逐渐减速 |
| ease-in | 加速 |
| ease-out | 减速 |
| ease-in-out | 先加速后减速 |

## 2. 为每个过渡添加值。

```
color .25s ease-in
```

从以下值中选择（表12.10）：

- > 来自表12.11的过渡属性指示受影响的特定CSS属性。
- > transition-duration 设置过渡从开始到结束应花费的时间，通常以秒为单位（表12.12）。这是可选的，默认值为0。
- > transition-timing-function 定义过渡进行时的速度行为（表12.13）。此值不是必需的，未设置时默认为 linear。
- > transition-delay 指定持续时间在开始前应暂停多久（表12.14）。这是可选的，未设置时默认为0。

## 表12.14 过渡延迟值

| Value | |
|---|---|
| <time> | ●10 ◇16 ◇ ◇ ◇12.5 |

## 3. 根据需要添加更多过渡。

```
, opacity .5s ease, transform .25s ease-in-out 0;
```

你可以添加任意数量的过渡，用逗号分隔。如果你为 transform 值设置过渡，请务必使用带有正确过渡浏览器扩展的浏览器扩展版本，如所示。

本节所示示例使用了过渡简写，但每个属性都可以单独设置，使用 transition-property、transition-duration、transition-timing-function 和 transition-delay 属性。当然，你需要为所有三个浏览器扩展以及标准CSS版本独立设置所有这些属性，这可能会导致大量代码。不过，使用这些属性可以用于覆盖特定值。

## 通用过渡

我向通用选择器添加了默认过渡，将这些样式应用到屏幕上的每个元素。这确保了设计中一致的过渡，并减少了所需代码量，因为我只应用一次。然后可根据需要覆盖过渡。

## 综合起来

transition-properties.css 的完成代码应类似于代码12.5。

代码12.5 最终的 transition-properties.css

```css
/*** transition-properties.css ***/

aside, figure, a {
    -webkit-transition: color .25s ease-out, opacity .5s ease .1s, -webkit-transform .25s ease-in-out;
    -moz-transition: color .25s ease-out, opacity .5s ease .1s, -moz-transform .25s ease-in-out;
    -o-transition: color .25s ease-out, opacity .5s ease .1s, -o-transform .25s ease-in-out;
    transition: color .25s ease-out, opacity .5s ease .1s, transform .25s ease-in-out;
}
aside {
    -webkit-transform: rotate(-2deg);
    -moz-transform: rotate(-2deg);
    -o-transform: rotate(-2deg);
    transform: rotate(-2deg);
}
div.gallery {
    position: relative;
    width: 100%;
    display: block;
    overflow: visible;
    height: 300px;
}
div.gallery figure:hover {
    opacity: 1;
    z-index: 999;
}
div.gallery figure {
    position: absolute;
    opacity: .5;
    z-index: 0;
    width: auto;
    -webkit-transform-origin: left 25%;
    -moz-transform-origin: left 25%;
    transform-origin: left 25%;
    -webkit-transform-style: flat;
    -moz-transform-style: flat;
    transform-style: flat;
    -webkit-perspective: 5000;
    -moz-perspective: 5000;
    perspective: 5000;
    -webkit-perspective-origin: 25% 25%;
    -moz-perspective-origin: 25% 25%;
    perspective-origin: 25% 25%;
    -webkit-backface-visibility: visible;
    -moz-backface-visibility: visible;
    backface-visibility: visible;
}
div.gallery figure#f1 {
    top: -60px;
    left: -5%;
    -webkit-transform: scale(.5) rotate(10deg);
    -moz-transform: scale(.5) rotate(10deg);
    -o-transform: scale(.5) rotate(10deg);
    transform: scale(.5) rotate(10deg); }
div.gallery figure#f2 {
    top: 60px;
    left: 25%;
    -webkit-transform: perspective(250px) scale3d(.5,.75,1.5) rotate3d(-3,-3,-8,18deg);
    -moz-transform: perspective(250px) scale3d(.5,.75,1.5) rotate3d(-3,-3,-8,18deg);
    -o-transform: perspective(250px) scale3d(.5,.75,1.5) rotate3d(-3,-3,-8,18deg);
    transform: perspective(250px) scale3d(.5,.75,1.5) rotate3d(-3,-3,-8,18deg); }
div.gallery figure#f3 {
    right: -10%;
    -webkit-transform: scale(.75)rotate(3deg);
    -moz-transform: scale(.75)rotate(3deg);
    -o-transform: scale(.75) rotate(3deg);}
    transform: scale(.75) rotate(3deg); }
div.gallery figure#f1:hover, div.gallery figure#f2:hover, div.gallery figure#f3:hover {
    -webkit-transform: rotate(0);
    -moz-transform: rotate(0);
    -o-transform: rotate(0);
    transform: rotate(0);
    cursor: pointer;}
aside, figure, a {
    -webkit-transition: color .25s ease-in, opacity .5s ease, -webkit-transform .25s ease-in-out 0;
    -moz-transition: color .25s ease-in, opacity .5s ease, -moz-transform .25s ease-in-out 0;
    -o-transition: color .25s ease-in, opacity .5s ease, -o-transform .25s ease-in-out 0;
    transition: color .25s ease-in, opacity .5s ease, transform .25s ease-in-out 0; }
div.gallery figure#f1:hover, div.gallery figure#f2:hover, div.gallery figure#f3:hover {
    -webkit-transform: rotate(0);
    -moz-transform: rotate(0);
    -o-transform: rotate(0);
    transform: rotate(0);
    cursor: pointer; }
```

## 为什么要添加所有浏览器扩展？

请注意，代码12.5相当详尽，主要是因为我们不得不添加多个浏览器扩展。许多开发者认为，“没有人使用Opera或 Firefox，所以何必费心？我只使用Webkit。”事实是，Opera和 Firefox 都有受众，忽略它们很不礼貌。然而，浏览器忽视已成为一个足够大的问题，以至于 Mozilla、Opera 甚至 Microsoft 都在为 Webkit 扩展添加支持。从他们的角度来看可以理解，但对开发者来说是坏消息，他们现在不知道自己的代码是否在正确的浏览器中使用。

添加完全兼容的代码只需几秒钟。不要偷懒。总有一天，所有这些代码都将在没有浏览器扩展的情况下可用。在此之前，请使用它们！

