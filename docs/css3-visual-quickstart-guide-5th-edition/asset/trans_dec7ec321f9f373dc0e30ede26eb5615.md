
## Mozilla 渐变

在 Firefox 或使用 -moz 扩展的浏览器中，你可以使用 `-moz-linear-gradient` 或 `-moz-repeating-linear-gradient` 属性创建线性渐变，或者使用 `-moz-radial-gradient` 或 `-moz-repeating-radial-gradient` 创建圆形渐变。重复渐变将根据其大小进行平铺。

-moz 渐变扩展使用以下值：

- * Point-一个或两个用空格分隔的关键字值，定义渐变开始的侧边或角。值可以包括 top、right、bottom 和（或或）left。如果使用两个值（用空格分隔），则指定一个角，例如 `top left`。

- * Position-背景位置，与本章稍后显示的背景图像设置（表 7.10）相同，用于径向渐变的中心点，例如 `center`。

- * Angle-渐变以度 (deg)、梯度度 (grad) 或弧度 (rad) 为单位的角度，例如 `45deg`。

- * Shape-径向渐变的形状，圆形 (circle) 或椭圆 (ellipse)。

![](img/9cd61ac1d4015ed5688d0c411434a660_211_0.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_211_1.png)

Mozilla 增加了多个选项，允许创建简单和复杂的渐变。

![](img/9cd61ac1d4015ed5688d0c411434a660_211_2.png)

![](img/9cd61ac1d4015ed5688d0c411434a660_211_3.png)

Mozilla 径向渐变允许你设置大小、角度和形状。

## 表 7.3 -moz-gradient 大值

| Value | 描述 |
| --- | --- |
| closest-side | 渐变形状为遇到与其中心最近的侧边 |
| closest-corner | 渐变形状为遇到与其中心最近的角 |
| farthest-side | 渐变形状为遇到与其中心最远的侧边 |
| farthest-corner | 渐变形状为遇到与其中心最远的角 |
| contain | 与 farthest-side 相同 |

- - Size—作为关键字形式的径向渐变大小（表 7.3）。
- Stop—渐变沿线特定点的颜色。这必须包含一个颜色值（表 7.1）以及可选的百分比或长度值，用于设置颜色在渐变轴上的位置，例如 `orange 60%`。

## Webkit 渐变

Safari、Chrome 以及任何使用 -webkit-gradient 扩展的浏览器使用 `-webkit-gradient-property` 属性来添加渐变。该属性有多个选项，取决于你想创建线性渐变还是径向渐变：

- - Type—线性 (linear) 或径向 (radial)
- Start—一个或两个用空格分隔的长度或关键字值，定义线性渐变开始的位置、侧边或角。值可以包括 top、right、bottom 和（或）left。如果使用两个值（用空格分隔），则指定一个角，例如 `top`。
- End—一个或两个用空格分隔的长度或关键字值，定义线性渐变结束的位置、侧边或角。值可以包括 top、right、bottom 和（或）left。如果使用两个值（用空格分隔），则指定一个角，例如 `top`。
- Angle—渐变以度 (deg)、梯度度 (grad) 或弧度 (rad) 为单位的角度，例如 `45deg`。
- Shape—径向渐变的形状，圆形 (circle) 或椭圆 (ellipse)。
- Size—作为关键字形式的径向渐变大小（表 7.3）。

（注：原文中存在大量重复的段落，已按要求进行去重）
