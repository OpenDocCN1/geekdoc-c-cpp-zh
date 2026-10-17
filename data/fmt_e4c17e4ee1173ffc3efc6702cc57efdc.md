
| 方法 | 描述 |
| --- | --- |
| `void fillArc(int x, int y, int width, int height, int startAngle, int arcAngle)` | 与其对应的 `draw` 方法相同，但用当前前景色填充。 |
| `Color getColor()` | 返回此图形上下文的前景色。 |
| `void setColor(Color color)` | 将此图形上下文的前景色设置为指定的颜色。 |

**FIGURE 2.12** `Graphics` 类的一些方法

> **KEY CONCEPT** 大多数形状可以填充绘制（不透明）或不填充绘制（轮廓）。

请注意，这些方法还允许我们绘制圆形和正方形，它们只是椭圆和矩形各自的特定类型。我们将在本书的适当位置稍后讨论 `Graphics` 类的其他绘图方法。

`Graphics` 类的方法允许我们指定希望形状是否填充或不填充。不填充的形状仅显示形状的轮廓，其余部分透明（可以看到任何底层图形）。填充的形状在边界之间是实心的，会覆盖任何底层图形。

所有这些方法都依赖于我们在本章前面讨论过的 Java 坐标系统。请回忆，点 (0, 0) 位于左上角，使得 x 值向右移动时变大，y 值向下移动时变大。任何绘制在可见区域外的坐标上的形状都不会被看到。

> **KEY CONCEPT** 使用边界矩形来定义诸如椭圆之类的曲线形状的位置和大小。

`Graphics` 的许多绘图方法都是自解释的，但有些需要更详细的讨论。例如，`drawOval` 方法绘制的椭圆由左上角的坐标和指定边界矩形宽度和高度的尺寸定义。具有曲线的形状，例如椭圆，通常由包围其周边的矩形定义。图 2.13 描绘了椭圆的边界矩形。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_128_0.png)

**FIGURE 2.13** 一个椭圆及其边界矩形

> **KEY CONCEPT** 弧是椭圆的一部分，从特定的起始角度开始，延伸距离由弧角度指定。

弧可以被视为椭圆的一部分。要绘制弧，我们指定弧所属的椭圆以及我们感兴趣的椭圆部分。弧的起点由起始角度定义，弧的终点由弧角度定义。弧角度并不表示弧的结束位置，而是表示其范围。起始角度和弧角度均以度为单位进行测量。起始角度的原点是穿过椭圆中心的一条假想水平线，可称为 0°，如图 2.14 所示。

每个图形上下文都有一个当前前景色，用于在绘制形状或字符串时使用。每个可绘制的表面都有一个背景色。前景色使用 `Graphics` 类的 `setColor` 方法设置，背景色使用我们正在绘制的组件（如 applet）的 `setBackground` 方法设置。

清单 2.11 显示了一个名为 `Snowman` 的 applet。它使用各种绘图和颜色方法绘制一个以雪人为主角的冬季场景。仔细查看代码，注意每个形状是如何绘制来创建整体图像的。

请注意，雪人图形基于两个常量值 `MID` 和 `TOP`，它们定义了雪人的左右中点和顶部。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_128_1.png)

VideoNote: 使用绘制形状的示例。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_128_2.png)

**FIGURE 2.14** 一个由椭圆、起始角度和弧角度定义的弧

### Listing 2.11

```java
//*******************************************************************
//  Snowman.java        Author: Lewis/Loftus
//
//  Demonstrates basic drawing methods and the use of color.
//*******************************************************************

import javax.swing.JApplet;
import java.awt.*;

public class Snowman extends JApplet
{
    //-------------------------------------------------------------
    //  Draws a snowman.
    //-------------------------------------------------------------
    public void paint (Graphics page)
    {
        final int MID = 150;
        final int TOP = 50;

        setBackground (Color.cyan);

        page.setColor (Color.blue);
        page.fillRect (0, 175, 300, 50);  // ground

        page.setColor (Color.yellow);
        page.fillOval (-40, -40, 80, 80);  // sun

        page.setColor (Color.white);
        page.fillOval (MID-20, TOP, 40, 40);        // head
        page.fillOval (MID-35, TOP+35, 70, 50);      // upper torso
        page.fillOval (MID-50, TOP+80, 100, 60);     // lower torso

        page.setColor (Color.black);
        page.fillOval (MID-10, TOP+10, 5, 5);        // left eye
        page.fillOval (MID+5, TOP+10, 5, 5);         // right eye

        page.drawArc (MID-10, TOP+20, 20, 10, 190, 160);  // smile

        page.drawLine (MID-25, TOP+60, MID-50, TOP+40);  // left arm
        page.drawLine (MID+25, TOP+60, MID+55, TOP+60);  // right arm

        page.drawLine (MID-20, TOP+5, MID+20, TOP+5);    // brim of hat
        page.fillRect (MID-15, TOP-20, 30, 25);          // top of hat
    }
}
```

### LISTING 2.11 continued

### DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_130_0.png)

雪人头部。整个雪人图形都是相对于这些值绘制的。使用像这样的常量可以更轻松地创建雪人并在以后进行修改。例如，要将我们图片中的雪人向右或向左移动，只需更改一个常量声明即可。

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 2.45 什么是边界矩形？

+   SR 2.46 假设你有一个名为 `page` 的 `Graphics` 对象，写一条语句将绘制一个边长为 50 的正方形，使其左上角位于点 (16, 12)。

+   SR 2.47 假设你有一个名为 `page` 的 `Graphics` 对象，写一系列语句将绘制一个蓝色矩形，其高度为 20，宽度为 40，使其左上角位于点 (30, 35)。

### SR 2.48 对 `Snowman` 程序分别做出以下每项更改会有什么结果？你可以进行更改，编译并运行程序，并观察和报告结果。简要说明你观察到的现象。

+   a. `MID` 的值设为 120 而不是 150。

+   b. `TOP` 的值设为 25 而不是 50。

+   c. 在程序的最后两条语句之前（绘制帽子的语句）加入语句：

    ```
    page.setColor (Color.blue);
    ```

+   d. 在创建微笑的语句中，190 改为 10。

+   e. 在创建上半身的语句之前，前景色设为青色。在上半身创建后立即将其设置回白色。

## Summary of Key Concepts

- `print` 和 `printLn` 方法代表 `System.out` 对象提供的两种服务。
- 转义序列可用于表示否则会导致编译问题的字符。
- 变量是用于保存特定数据类型值的内存位置的名称。
- 访问数据会使其在内存中保持不变，但赋值语句会覆盖旧数据。
- 我们不能将一种类型的值赋给不兼容类型的变量。
- 常量在其存在期间保持特定值。
- Java 有两种数值类型：整数和浮点数。有四种整数数据类型和两种浮点数据类型。
- Java 使用 16 位 Unicode 字符集来表示字符数据。
- 表达式是用于执行计算的运算符和操作数的组合。
- Java 遵循一套定义良好的优先级规则，该规则规定表达式中运算符的求值顺序。
- 应避免窄化转换，因为它们可能会丢失信息。
- `Scanner` 类提供用于从各种来源读取各种类型输入的方法。
- 图形数据是通过将其划分为许多称为像素的小块来表示的。
- Java 的坐标系统原点位于左上角，所有可见坐标均为正。
- Java 中颜色使用 RGB 值表示——三个值表示原色红、绿、蓝的贡献。
- `Color` 类包含一些常用的预定义颜色，可用于定义许多其他颜色。
- `Applet` 是通常通过网络传输并使用 Web 浏览器执行的 Java 程序。
- 大多数形状可以填充绘制（不透明）或未填充绘制（作为轮廓）。
- 边界矩形用于定义诸如椭圆之类的弯曲形状的位置和大小。
- 弧是椭圆的一部分，从特定起始角度开始，延伸距离由弧角度指定。

## Exercises

*Visit www.myprogramminglab.com to complete many of these Exercises online and get instant feedback.*

**EX 2.1** 用对象及其提供的服务来解释以下编程语句：

```
System.out.println ("I gotta be me!");
```

**EX 2.2** 以下代码片段会产生什么输出？解释。

```
System.out.print ("Here we go!");
System.out.println ("12345");
System.out.print ("Test this if you are not sure.");
System.out.print ("Another.");
System.out.println ();
System.out.println ("All done.");
```

**EX 2.3** 以下程序语句有什么问题？如何修复？

```
System.out.println ("To be or not to be, that
is the question.");
```

**EX 2.4** 以下语句会产生什么输出？解释。

```
System.out.println ("50 plus 25 is " + 50 + 25);
```

**EX 2.5** 以下语句会产生什么输出？解释。

```
System.out.println ("He thrusts his fists\n\tagainst" +
"the post\nand still insists\nthe sees the \"ghost\"");
```

**EX 2.6** 执行以下语句后，整数变量 `size` 中包含什么值？

```
size = 18;
size = size + 12;
size = size * 2;
size = size / 4;
```

**EX 2.7** 执行以下语句后，浮点变量 `depth` 中包含什么值？

```
depth = 2.4;
depth = 20 - depth * 4;
depth = depth / 5;
```

**EX 2.8** 执行以下语句后，整数变量 `length` 中包含什么值？

```
length = 5;
length *= 2;
length *= length;
length /= 100;
```

**EX 2.9** 编写四个不同的程序语句来递增整数变量 `total` 的值。

**EX 2.10** 给出以下声明，在每个列出的赋值语句中存储什么结果？

```
int iResult, num1 = 25, num2 = 40, num3 = 17, num4 = 5;
double fResult, val1 = 17.0, val2 = 12.78;
```

+   a. `iResult = num1 / num4;`

+   b. `fResult = num1 / num4;`

+   c. `iResult = num3 / num4;`

+   d. `fResult = num3 / num4;`

+   e. `fResult = val1 / num4;`

+   f. `fResult = val1 / val2;`

+   g. `iResult = num1 / num2;`

+   h. `fResult = (double) num1 / num2;`

+   i. `fResult = num1 / (double) num2;`

+   j. `fResult = (double) (num1 / num2);`

+   k. `iResult = (int) (val1 / num4);`

+   l. `fResult = (int) (val1 / num4);`

+   m. `fResult = (int) ((double) num1 / num2);`

+   n. `iResult = num3 % num4;`

+   o. `iResult = num2 % num3;`

+   p. `iResult = num3 % num2;`

+   q. `iResult = num2 % num4;`

**EX 2.11** 对于以下每个表达式，通过在每个运算符下方写一个数字来指出运算符的求值顺序。

+   a. `a - b - c - d`

+   b. `a - b + c - d`

+   c. `a + b / c / d`

+   d. `a + b / c * d`

+   e. `a / b * c * d`

+   f. `a % b / c * d`

+   g. `a % b % c % d`

+   h. `a - (b - c) - d`

+   i. `(a - (b - c)) - d`

+   j. `a - ((b - c) - d)`

+   k. `a % (b % c) * d * e`

+   l. `a + (b - c) * d - e`

+   m. `(a + b) * c + d * e`

+   n. `(a + b) * (c / d) % e`

**EX 2.12** Web 在某些 Java 程序的翻译和执行中扮演什么角色？

**EX 2.13** 比较和对比传统坐标系统和 Java 图形组件使用的坐标系统。

**EX 2.14** 存储一张 400 像素宽、250 像素高的彩色图片需要多少位？假设颜色使用本章描述的 RGB 技术表示，并且不进行特殊压缩。

**EX 2.15** 假设你有一个名为 `page` 的 `Graphics` 对象，写一条语句将从点 (20, 30) 绘制一条线到点 (50, 60)。

**EX 2.16** 假设你有一个名为 `page` 的 `Graphics` 对象，写一条语句将绘制一个高度为 70、宽度为 35 的矩形，使其左上角位于点 (10, 15)。

**EX 2.17** 假设你有一个名为 `page` 的 `Graphics` 对象，写一条语句将绘制一个以点 (50, 50) 为中心、半径为 20 像素的圆。

**EX 2.18** 以下代码行绘制 `Snowman` applet 中雪人的眼睛。眼睛绘制时似乎位于脸部中央，但每次调用的第一个参数并未从中点等距偏移。解释。

```
page.fillOval (MID-10, TOP+10, 5, 5);
page.fillOval (MID+5, TOP+10, 5, 5);
```

## Programming Projects

Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.

**PP 2.1** 创建第 1 章中 `Lincoln` 应用的修订版本，使引号出现在引语周围。

**PP 2.2** 编写一个应用程序，读取三个整数并打印它们的平均值。

**PP 2.3** 编写一个应用程序，提示并读取一个人的姓名、年龄、大学和宠物的名字。然后打印以下段落，插入适当的数据：

> Hello, my name is name and I am age years old. I’m enjoying my time at college, though I miss my pet petname very much!

**PP 2.4** 编写一个应用程序，读取两个浮点数并打印它们的和、差和乘积。

**PP 2.5** 创建一个 `TempConverter` 应用程序的版本，将华氏温度转换为摄氏温度。从用户读取华氏温度。

**PP 2.6** 编写一个应用程序，将英里转换为公里。（一英里等于 1.60935 公里。）以浮点值形式从用户读取英里值。

**PP 2.7** 编写一个应用程序，提示并读取速度和行驶距离的整数值，然后以浮点结果打印行程所需的时间。
