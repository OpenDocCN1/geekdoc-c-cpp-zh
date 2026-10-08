
正如我们在之前的示例中所看到的，Java 程序在本质上不必是图形化的。然而，如果它是图形化的，程序中的每个图形组件都有自己的坐标系，原点 `(0, 0)` 位于左上角。这种一致的方法使得管理各种图形元素变得相对容易。

## 表示颜色

彩色图片和黑白图片一样被分为像素。然而，由于每个像素都可能是许多可能的颜色之一，仅用一个位来表示每个像素是不够的。表示像素颜色有多种方法。让我们简要讨论一种流行的技术。

每种颜色都可以表示为三种原色的混合：红、绿、蓝。在 Java 以及许多其他计算机语言中，颜色由三个数字指定，这些数字统称为 RGB 值。RGB 代表红-绿-蓝。每个数字代表一种原色的贡献度。使用一个字节（8 位）来存储三个数字中的每一个，数字的范围可以从 0 到 255。每种原色的水平决定了整体颜色。例如，红色和绿色的高值结合低水平的蓝色会产生一种黄色调。

**核心概念**

Java 中使用 RGB 值表示颜色——即代表红、绿、蓝三种原色贡献的三个值。

| 颜色 | 对象 | RGB 值 |
|---|---|---|
| 黑色 | `Color.black` | 0, 0, 0 |
| 蓝色 | `Color.blue` | 0, 0, 255 |
| 青色 | `Color.cyan` | 0, 255, 255 |
| 灰色 | `Color.gray` | 128, 128, 128 |
| 深灰色 | `Color.darkGray` | 64, 64, 64 |
| 浅灰色 | `Color.lightGray` | 192, 192, 192 |
| 绿色 | `Color.green` | 0, 255, 0 |
| 品红色 | `Color.magenta` | 255, 250, 0 |
| 橙色 | `Color.orange` | 255, 200, 0 |
| 粉色 | `Color.pink` | 255, 175, 175 |
| 红色 | `Color.red` | 255, 0, 0 |
| 白色 | `Color.white` | 255, 255, 255 |
| 黄色 | `Color.yellow` | 255, 255, 0 |

图 2.10 `Color` 类中的预定义颜色

## 2.8 Applet

在 Java 中，程序员使用来自 `java.awt` 包的 `Color` 类来定义和管理颜色。`Color` 类的每个对象代表一种颜色。该类包含了自身的几个实例，以提供一组基本的预定义颜色。图 2.10 列出了 `Color` 类的预定义颜色。它还包含定义和管理许多其他颜色的方法。

> **核心概念**
> `Color` 类包含了一些常用的预定义颜色，并可以使用它们定义许多其他颜色。

## 自习题

- SR 2.38 如何使用 1 和 0 表示黑白图片？
- SR 2.39 使用 Java 坐标系绘制的矩形，三个角的坐标分别为 `(3, 4)`、`(3, 7)` 和 `(8, 7)`。第四个角的坐标是什么？
- SR 2.40 使用 Java 坐标系绘制的正方形，其中两个角的坐标为 `(5, 10)` 和 `(8, 10)`。另外两个角的坐标是什么？
- SR 2.41 存储一张宽 300 像素、高 200 像素的彩色图片需要多少位？假设颜色使用本章描述的 RGB 技术表示，且没有使用特殊的压缩技术。

## 2.8 Applet

Java 程序有两种类型：Java applet 和 Java 应用程序。Java applet 是一种旨在嵌入 HTML 文档中、通过网络传输并使用 Web 浏览器执行的 Java 程序。Java 应用程序是一个可以使用 Java 解释器执行的独立程序。到目前为止书中介绍的所有程序都是 Java 应用程序。

> **核心概念**
> Applet 是通常通过网络传输并使用 Web 浏览器执行的 Java 程序。

Web 允许我们通过一种极其方便易于使用的点击界面来发送和接收各种类型的媒体，如文本、图形和声音。Java applet 是第一种可以通过 Web 软件获取的可执行程序。Java applet 被认为可以在 Web 上交换的另一种媒体类型。

虽然 Java applet 通常旨在通过网络传输，但它们并非如此。它们完全可以使用 Web 浏览器在本地查看。Sun Java 开发工具包中有一个名为 `appletviewer` 的工具，用于解释和执行 applet。我们在书中使用 `appletviewer` 显示 applet。然而，通常制作 Java applet 的目的是在网页上提供链接，允许世界各地的用户获取并执行它。

Java 字节码而不是 Java 源代码链接到 HTML 文档并在网络上传输。一旦 applet 到达目的地，将使用嵌入 Web 浏览器的 Java 解释器版本来执行它。Java applet 在与 Web 使用之前必须编译成字节码格式。

# 第 2 章 数据与表达式

## 使用 Web 运行 Applet

为了让 applet 通过 Web 传输并在浏览器中执行，它必须在超文本标记语言 HTML 文档中引用。HTML 文档包含了指定格式化指令并定义文档中要包含的特殊媒体类型的标签。Java 程序被视为一种特定的媒体类型，就像文本、图形和声音一样。

HTML 标签包含在角括号中。以下是一个 applet 的示例：

```
<applet code="Einstein.class" width="350" height="175">
</applet>
```

该标签标记存储在 `Einstein.class` 文件中的字节码应该通过网络传输，并在查看此特定 HTML 文档的机器上执行。`<applet>` 标签还指示了 applet 的宽度和高度。

还有其他标签可以在 HTML 文件中引用 applet，包括 `<object>` 标签和 `<embed>` 标签。根据世界维网联盟 W3C 的规定，应该使用 `<object>` 标签。然而，浏览器对 `<object>` 标签的支持并不一致。目前，最可靠的解决方案是使用 `<applet>` 标签。

注意，applet 指向的是 Einstein applet 的字节码文件，而不是源代码文件。在 applet 通过 Web 传输之前，必须先将其编译为字节码格式。然后，如图 2.11 所示，可以使用 Web 浏览器加载文档，它将自动解释并执行 applet。

![](img/7f8e069c1898b741edc17dfeed34b0c1_125_0.png)

图 2.11 Java 的翻译与执行过程，包括 applets

## 2.9 绘制形状

### 自测题

- SR 2.42 Java 应用程序和 Java applet 之间有什么区别？
- SR 2.43 Applet 的 `paint` 方法是什么被调用的？
- SR 2.44 下面的 HTML applet 标签有什么错误？请解释。

```
<applet code="DrawHouse.java" width="400" height="300">
</applet>
```

Java 标准类库提供了许多类，让我们能够展示和操纵图形信息。`Graphics` 类是所有此类处理的基础。

### Graphics 类

`Graphics` 类定义在 `java.awt` 包中。它包含了用于绘制形状的各种方法，包括线、矩形和椭圆。图 2.12 列出了 `Graphics` 类的一些基本绘制方法。

注意，这些方法也绘制圆和正方形，它们分别仅仅是椭圆和矩形的特殊类型。我们将在书的后续适当时候讨论 `Graphics` 类的其他绘制方法。

`Graphics` 类的方法允许我们指定是想要填充的还是未填充的形状。未填充的形状只显示形状的轮廓且是透明的。填充的形状在其边界之间是实心的，并会覆盖任何底层的图形。

所有这些方法都依赖于 Java 坐标系，我们在在本章早些时候讨论过。记住 `(0,0)` 是左上角，向右移动时 x 值增大，向下移动时 y 值增大。在可见区域之外坐标上绘制的任何内容都将不可见。

许多 `Graphics` 绘制方法是显而易懂的，但有些需要更多的讨论。例如，注意通过 `drawOval` 方法绘制的椭圆是由左上角的坐标以及指定边界矩形宽度和高度的尺寸定义的。

> 核心概念
> 大多数形状可以绘制填充或未填充绘制。

> 核心概念
> 边界矩形用于定义作为椭圆的曲线形状的位置和大小。

```
void drawLine(int x1, int y1, int x2, int y2)
从点 (x1, y1) 到点 (x2, y2) 绘制一条线。
```

```
void drawRect(int x, int y, int width, int height)
绘制一个左上角为 (x, y)、尺寸为 width 和 height 的矩形。
```

```
void drawOval(int x, int y, int width, int height)
绘制一个由左上角为 (x, y)、尺寸为 width 和 height 的矩形边界的椭圆。
```

```
void drawString(String str, int x, int y)
在点 (x, y) 处绘制字符 str，向右延伸。
```

```
void drawArc(int x, int y, int width, int height, startAngle, arcAngle)
沿着由 x, y, height 定义的矩形边界的椭圆绘制圆弧。圆弧从 startAngle 开始，延伸 arcAngle 定义的距离。
```

```
void fillRect(int x, int y, int width, int height)
与其对应的 draw 方法相同，但用当前前景颜色填充。
```

```
void fillOval(int x, int y, int width, int height)
```

```
void fillArc(int x, int y, int width, int height, startAngle, arcAngle)
```

```
void getColor()
返回此图形的前景颜色。
```

```
void setColor(Color color)
将此上下文的前景颜色设置为指定的颜色。
```

图 2.12 `Graphics` 类的一些方法

> 核心概念
> 通过 `drawOval` 方法绘制的椭圆是由左上角的坐标以及指定边界矩形宽度和高度的尺寸定义的。

![](img/7f8e069c1898b741edc17dfeed34b0c1_125_0.png)

图 2.13 椭圆和边界矩形

## 2.9 绘制形状

> 核心概念
> 边界矩形用于定义作为椭圆的曲线形状的位置和大小。

> 核心概念
> 大多数形状可以绘制填充或未填充绘制。

> 核心概念
> 通过 `drawOval` 方法绘制的椭圆是由左上角的坐标以及指定边界矩形宽度和高度的尺寸定义的。
