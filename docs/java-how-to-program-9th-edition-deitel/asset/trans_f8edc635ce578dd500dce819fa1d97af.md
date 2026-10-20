
# 4.13 基本类型

附录 D 中的表格列出了 Java 的 8 种基本类型。与其前身语言 C 和 C++ 一样，Java 要求所有变量都必须具有类型。因此，Java 被称为强类型语言。

在 C 和 C++ 中，由于基本类型在不同计算机上无法保证完全相同，程序员常常不得不为不同的计算机平台编写不同版本的程序。例如，`int` 值在一台机器上可能用 16 位（2 字节）内存表示，在第二台机器上用 32 位（4 字节）表示，在另一台机器上用 64 位（8 字节）表示。而在 Java 中，`int` 值始终是 32 位（4 字节）。

## 可移植性提示 4.1

> Java 中的基本类型在所有支持 Java 的计算机平台上都是可移植的。

附录 D 中的每种类型都列出了其以位为单位的大小（8 位等于 1 字节）及其取值范围。由于 Java 的设计者希望确保可移植性，他们采用了国际上公认的字符格式标准（Unicode；更多信息请访问 www.unicode.org）和浮点数标准（IEEE 754；更多信息请访问 grouper.ieee.org/groups/754/）。

回顾第 3.4 节：在方法外部声明为类的字段的基本类型变量，除非显式初始化，否则会自动赋默认值。类型为 `char`、`byte`、`short`、`int`、`long`、`float` 和 `double` 的实例变量默认都会被赋值为 0。类型为 `boolean` 的实例变量默认为 `false`。引用类型的实例变量默认初始化为 `null`。

# 4.14（可选）GUI 与图形案例研究：创建简单绘图

Java 的一个吸引人的特性是它的图形支持，它使你可以通过可视化方式增强应用程序。现在我们介绍 Java 的一项图形能力——绘制直线。本节还涵盖创建窗口以在计算机屏幕上显示图形的基础知识。

## Java 坐标系

要在 Java 中绘图，你必须理解 Java 坐标系（图 4.17），这是一种用于标识屏幕上点的方案。默认情况下，GUI 组件的左上角

![](img/009e962758dcc71dbc43a493362e6dc0_171_0.png)

图 4.17 | Java 坐标系。单位以像素计量。

的坐标为 (0, 0)。一个坐标对由 x 坐标（水平坐标）和 y 坐标（垂直坐标）组成。x 坐标是从左到右的水平位置，y 坐标是从上到下的垂直位置。x 轴描述所有水平坐标，y 轴描述所有垂直坐标。

坐标指明图形在屏幕上的显示位置。坐标单位以像素计量。术语 pixel 代表“picture element”（图像元素）。像素是显示器的最小分辨率单位。

## 第一个绘图应用程序

我们的第一个绘图应用程序只绘制两条直线。类 DrawPanel（图 4.18）执行实际的绘图，而类 DrawPanelTest（图 4.19）创建窗口来显示该图形。在 DrawPanel 类中，第 3～4 行的 import 语句使我们能够使用 Graphics 类（来自 java.awt 包，它提供了各种在屏幕上绘制文本和形状的方法）和 JPanel 类（来自 javax.swing 包，它提供了一个可供我们绘图的区域）。

```
1  // Fig. 4.18: DrawPanel.java
2  // Using drawLine to connect the corners of a panel.
3  import java.awt.Graphics;
4  import javax.swing.JPanel;
5
6  public class DrawPanel extends JPanel
7  {
8      // draws an X from the corners of the panel
9      public void paintComponent( Graphics g )
10     {
11         // call paintComponent to ensure the panel displays correctly
12         super.paintComponent( g );
13
14         int width = getWidth(); // total width
15         int height = getHeight(); // total height
16
17         // draw a line from the upper-left to the lower-right
18         g.drawLine( 0, 0, width, height );
19
20         // draw a line from the lower-left to the upper-right
21         g.drawLine( 0, height, width, 0 );
22     } // end method paintComponent
23  } // end class DrawPanel
```

图 4.18 | 使用 drawLine 连接面板的各个角。

```
1  // Fig. 4.19: DrawPanelTest.java
2  // Application to display a DrawPanel.
3  import javax.swing.JFrame;
4
5  public class DrawPanelTest
6  {
```

图 4.19 | 创建用于显示 DrawPanel 的 JFrame。（第 1 部分，共 2 部分。）

这可以确保我们在面板上开始绘图之前，面板已被正确渲染。接下来，第 14～15 行调用 DrawPanel 类从 JPanel 继承的方法。由于 DrawPanel 继承自 JPanel，因此 DrawPanel 可以使用 JPanel 的任何公有方法。getWidth 和 getHeight 方法分别返回 JPanel 的宽度和高度。第 14～15 行将这些值存储在局部变量 width 和 height 中。最后，第 18 行和第 21 行使用 Graphics 变量 g 调用 drawLine 方法来绘制两条直线。drawLine 方法在其四个参数表示的两个点之间绘制一条直线。前两个参数是一个端点的 x 和 y 坐标，后两个参数是另一个端点的坐标。如果调整窗口大小，这些直线会相应缩放，因为参数是基于面板的宽度和高度计算的。在此应用程序中调整窗口大小会导致系统调用 paintComponent 来重新绘制 DrawPanel 的内容。

## DrawPanelTest 类

要在屏幕上显示 DrawPanel，你必须将它放入一个窗口中。你可以使用 JFrame 类的对象创建窗口。在 DrawPanelTest.java（图 4.19）中，第 3 行从 javax.swing 包中导入 JFrame 类。main 中的第 10 行创建了一个包含我们绘图的 DrawPanel 对象，第 13 行创建了一个可以容纳并显示面板的新 JFrame。第 16 行以参数 JFrame.EXIT_ON_CLOSE 调用 JFrame 的 setDefaultCloseOperation 方法，以表示当用户关闭窗口时应用程序应终止。第 18 行使用 JFrame 类的 add 方法将 DrawPanel 添加到 JFrame。第 19 行设置 JFrame 的大小。setSize 方法接受两个参数，分别表示 JFrame 的宽度和高度。最后，第 20 行调用 JFrame 的 setVisible 方法并传入参数 true 来显示 JFrame。当 JFrame 显示时，系统会隐式调用 DrawPanel 的 paintComponent 方法（图 4.18 的第 9～22 行），并绘制出这两条直线（参见图 4.19 中的示例输出）。尝试调整窗口大小，可以看到直线始终根据窗口当前的宽度和高度绘制。

## GUI 与图形案例研究练习

- 4.1 使用循环和控制语句绘制直线可以产生许多有趣的设计。
  - a) 创建图 4.20 左侧屏幕截图中的设计。该设计从左上角开始绘制直线，使其呈扇形展开，直到覆盖面板的左上半个区域。一种方法是将宽度和高度分成相等的步数（我们发现 15 步效果不错）。每条直线的第一个端点始终位于左上角 (0, 0)。第二个端点可以从左下角开始，向上移动一个垂直步长、向右移动一个水平步长来确定。在两个端点之间绘制一条直线。继续向上并向右移动一步，以找到后续每个端点。调整窗口大小时，图形应相应缩放。
  - b) 修改第 (a) 部分，使直线从四个角呈扇形展开，如图 4.20 右侧屏幕截图所示。来自相对角的直线应沿中间相交。
- 4.2 图 4.21 显示了另外两个使用 while 循环和 drawLine 创建的设计。
  - a) 创建图 4.21 左侧屏幕截图中的设计。首先将每条边分成相等的增量数（我们再次选择 15）。第一条直线从左上角开始，在底边向右一个步长处结束。对于后续每一条直线，在左边向下移动一个增量，并在底边向右移动一个增量。继续绘制直线，直到到达右下角。调整窗口大小时，图形应缩放，使端点始终接触边缘。
  - b) 修改第 (a) 部分的答案，使该设计在四个角上镜像显示，如图 4.21 右侧屏幕截图所示。

