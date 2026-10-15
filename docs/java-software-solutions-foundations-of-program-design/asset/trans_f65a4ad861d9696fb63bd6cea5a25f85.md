

正如我们在之前的示例中看到的，Java 程序不必具有图形性质。然而，如果它具有图形性质，程序中的每个图形组件都有自己的坐标系统，原点 (0, 0) 位于左上角。这种一致的方法使得管理各种图形元素相对容易。

## 表示颜色

彩色图片与黑白图片一样被划分为像素。然而，由于每个像素可以是多种可能颜色中的一种，仅用一个比特来表示每个像素是不够的。表示像素颜色有各种方法。让我们简要讨论一种流行的技术。

KEY CONCEPT
Java 中颜色使用 RGB 值表示——三个值代表原色红、绿、蓝的贡献。

每种颜色都可以表示为三种原色的混合：红、绿、蓝。在 Java 中，与许多其他计算机语言一样，颜色由三个数字指定，统称为 RGB 值。RGB 代表 Red-Green-Blue。每个数字代表一种原色的贡献。使用一个字节（八位）存储三个数字中的每一个，这些数字的范围可以从 0 到 255。每种原色的级别决定了整体颜色。例如，红色和绿色值高而蓝色水平低会产生黄色色调。

| Color | Object | RGB Value |
|---|---|---|
| black | Color.black | 0, 0, 0 |
| blue | Color.blue | 0, 0, 255 |
| cyan | Color.cyan | 0, 255, 255 |
| gray | Color.gray | 128, 128, 128 |
| dark gray | Color.darkGray | 64, 64, 64 |
| light gray | Color.lightGray | 192, 192, 192 |
| green | Color.green | 0, 255, 0 |
| magenta | Color.magenta | 255, 0, 255 |
| orange | Color.orange | 255, 200, 0 |
| pink | Color.pink | 255, 175, 175 |
| red | Color.red | 255, 0, 0 |
| white | Color.white | 255, 255, 255 |
| yellow | Color.yellow | 255, 255, 0 |

FIGURE 2.10 Predefined colors in the Color class

在 Java 中，程序员使用 Color 类来定义和管理颜色，该类是 java.awt 包的一部分。Color 类的每个对象代表一种颜色。该类包含其自身的几个实例，以提供一组基本预定义颜色。图 2.10 列出了 Color 类的预定义颜色。它还包含用于定义和管理许多其他颜色的方法。

> KEY CONCEPT
> Color 类包含一些常用的预定义颜色，可用于定义许多其他颜色。

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

+ SR 2.38 如何使用 1 和 0 表示黑白图片？
+ SR 2.39 使用 Java 坐标系统绘制的矩形的三个角坐标为 (3, 4)、(3, 7) 和 (8, 7)。第四个角的坐标是什么？
+ SR 2.40 使用 Java 坐标系统绘制的正方形的两个角坐标为 (5, 10) 和 (8, 10)。另外两个角的坐标是什么？
+ SR 2.41 需要多少位来存储一张宽 300 像素、高 200 像素的彩色图片？假设颜色使用本章描述的 RGB 技术表示，并且不使用任何特殊压缩技术。

## 2.8 Applets

Java 程序有两种：Java 小程序和 Java 应用程序。Java 小程序是一种旨在嵌入 HTML 文档、通过网络传输并使用 Web 浏览器执行的 Java 程序。Java 应用程序是可使用 Java 解释器执行的独立程序。本书迄今为止介绍的所有程序都是 Java 应用程序。

> KEY CONCEPT
> 小程序是通常通过网络传输并使用 Web 浏览器执行的 Java 程序。

Web 使用户能够使用极其方便易用的点按界面发送和接收各种类型的媒体，如文本、图形和声音。Java 小程序是可通过 Web 软件检索的第一种可执行程序。Java 小程序被视为可通过 Web 交换的另一种媒体类型。

尽管 Java 小程序通常旨在通过网络传输，但它们不必如此。它们可以使用 Web 浏览器在本地查看。就此而言，它们甚至不必通过 Web 浏览器执行。Sun 的 Java 软件开发工具包中的一个工具 appletviewer 可用于解释和执行小程序。我们在本书中使用 appletviewer 来显示小程序。然而，

通常制作 Java 小程序的目的是在网页上提供指向它的链接，并允许世界各地的 Web 用户检索和执行它。

Java 字节码（不是 Java 源代码）链接到 HTML 文档并通过 Web 发送。嵌入在 Web 浏览器中的 Java 解释器版本用于在小程序到达目的地后执行它。在与 Web 一起使用之前，Java 小程序必须编译为字节码格式。

Java 小程序的结构与 Java 应用程序的结构有一些重要区别。因为执行小程序的 Web 浏览器已经在运行，所以小程序可以被视为更大程序的一部分。因此它们没有执行开始的主方法。Applet 中的 paint 方法会被自动调用。请考虑清单 2.10 中的程序，其中 paint 方法用于绘制一些形状并将阿尔伯特·爱因斯坦的一句名言写到屏幕上。

程序开头的两个 import 语句明确指出了程序中使用的包。在此示例中，我们需要 javax.swing 包中的 JApplet 类，以及 java.awt 包中定义的各种图形功能。第 3 章将进一步探讨 import 语句。

### LISTING 2.10

```
//****************************************************************
// Einstein.java      Author: Lewis/Loftus
// Demonstrates a basic applet.
//****************************************************************

import javax.swing.JApplet;
import java.awt.*;

public class Einstein extends JApplet
{
    //-------------------------------------------------------------
    // Draws a quotation by Albert Einstein among some shapes.
    //-------------------------------------------------------------
    public void paint (Graphics page)
    {
        page.drawRect (50, 50, 40, 40);    // square
        page.drawRect (60, 80, 225, 30);   // rectangle
        page.drawOval (75, 65, 20, 20);    // circle
        page.drawLine (35, 60, 100, 120);  // line

        page.drawString ("Out of clutter, find simplicity.", 110, 70);
        page.drawString ("-- Albert Einstein", 130, 100);
    }
}
```

类定义小程序的类扩展 JApplet 类，如类声明的头行所示。此过程使用了我们曾在第 1 章讨论并将在本书后面更详细探讨的面向对象概念继承。Applet 类还必须声明为 public。

paint 方法是几个具有特定意义的小程序方法之一。它会在小程序的图形元素需要绘制到屏幕上时自动调用，例如小程序首次运行时或覆盖它的另一个窗口被移动时。

请注意，paint 方法接受 Graphics 对象作为参数。Graphics 对象定义了我们可以交互的特定图形上下文。传递给小程序 paint 方法的图形上下文代表整个小程序窗口。每个图形上下文都有自己的坐标系统。在后面的示例中，我们将有多个组件，每个组件都有自己的图形上下文。

Graphics 对象允许我们使用 drawRect、drawOval、drawLine 和 drawString 等方法绘制各种形状。传递给绘图方法的参数指定要绘制的形状的坐标和大小。我们将在下一节中探讨这些和其他绘制形状的方法。

### LISTING 2.10 continued
DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_124_0.png)

