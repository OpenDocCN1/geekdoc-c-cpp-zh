
- `void setIconImage(Image image)`
  获取或设置 iconImage 属性，该属性决定框架的图标。窗口系统可能会将图标显示为框架装饰的一部分，或显示在其他位置。

### java.awt.Toolkit 1.0
- `static Toolkit getDefaultToolkit()`
  返回默认工具包。
- `Dimension getScreenSize()`
  获取用户屏幕的大小。

### javax.swing.ImageIcon 1.2
- `ImageIcon(String filename)`
  构造一个图标，其图像存储在文件中。
- `Image getImage()`
  获取此图标的图像。

## 10.3 在组件中显示信息

在本节中，我将展示如何在框架内显示信息（[图 10.3](#)）。

你可以将消息字符串直接绘制到框架上，但这不被认为是良好的编程实践。在 Java 中，框架实际上被设计为组件的容器，例如菜单栏和其他用户界面元素。通常，你在添加到框架中的另一个组件上绘制。

![](img/0e7b74ef51a065c077b42cd87b362288_835_0.png)

**图 10.3** 一个显示信息的框架

`JFrame` 的结构出奇地复杂。请看图 10.4，它展示了 `JFrame` 的组成。如你所见，`JFrame` 中分层放置了四个窗格。根窗格、分层窗格和玻璃窗格与我们无关；它们用于组织菜单栏和内容窗格，并实现外观与感觉。最让 Swing 程序员关心的是*内容窗格*。你添加到框架中的任何组件都会自动放入内容窗格：

```java
Component c = ...;
frame.add(c); // added to the content pane
```

在我们的例子中，我们想向框架添加一个组件，并在该组件上绘制消息。要在组件上绘制，你需要定义一个扩展 `JComponent` 的类，并重写该类中的 `paintComponent` 方法。

`paintComponent` 方法接受一个 `Graphics` 类型的参数。`Graphics` 对象保存用于绘制图像和文本的一组设置，例如你设置的字体或当前颜色。Java 中的所有绘制都必须通过 `Graphics` 对象进行。它具有绘制图案、图像和文本的方法。

下面说明如何创建一个可在其上绘制的组件：

```java
class MyComponent extends JComponent
{
    public void paintComponent(Graphics g)
    {
        code for drawing
    }
}
```

![](img/0e7b74ef51a065c077b42cd87b362288_836_0.png)

**图 10.4** JFrame 的内部结构

绝不要自己调用 `paintComponent` 方法。当应用程序的某一部分需要重绘时，它会被自动调用，你不应干预这个自动过程。

哪些操作会触发这种自动响应？例如，当用户增大窗口尺寸，或最小化然后还原窗口时，就会发生绘制。如果用户弹出了另一个窗口，覆盖了现有窗口，然后让覆盖的窗口消失，那么被覆盖的窗口现在已损坏，需要重绘。（图形系统不会保存下面的像素。）当然，当窗口第一次显示时，它需要执行代码来指定如何以及在哪里绘制初始元素。

![](img/0e7b74ef51a065c077b42cd87b362288_837_0.png)

> **提示：**
>
> 如果需要强制重绘屏幕，请调用 `repaint` 方法而不是 `paintComponent`。repaint 方法会使所有组件调用 `paintComponent`，并传入配置正确的 `Graphics` 对象。

如你在上面的代码片段中所见，`paintComponent` 方法接受一个 `Graphics` 类型的参数。在 `Graphics` 对象上为屏幕显示进行度量时，以像素为单位。(0, 0) 坐标表示你正在其表面绘制的组件的左上角。

`Graphics` 类有各种绘图方法，而显示文本被视为一种特殊的绘图。我们的 `paintComponent` 方法如下所示：

```java
public class NotHelloWorldComponent extends JComponent
{
    public static final int MESSAGE_X = 75;
    public static final int MESSAGE_Y = 100;
    public void paintComponent(Graphics g)
    {
        g.drawString("Not a Hello, World program", MESSAGE_X,
                     MESSAGE_Y);
    }
  . . .
}
```

最后，组件应告诉用户它希望有多大。重写 `getPreferredSize` 方法，并返回一个具有首选宽度和高度的 `Dimension` 类对象：

```java
public class NotHelloWorldComponent extends JComponent
{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 200;
    . . .
    public Dimension getPreferredSize()
    {
        return new Dimension(DEFAULT_WIDTH, DEFAULT_HEIGHT);
    }
}
```

当你用一个或多个组件填充框架，并且只想使用它们的首选大小时，请调用 `pack` 方法而不是 `setSize` 方法：

```java
class NotHelloWorldFrame extends JFrame
{
    public NotHelloWorldFrame()
    {
        add(new NotHelloWorldComponent());
        pack();
    }
}
```

[代码清单 10.2]() 显示了完整代码。

### 代码清单 10.2 notHelloWorld/NotHelloWorld.java

```java
package notHelloWorld;

import javax.swing.*;
import java.awt.*;

/**
 * @version 1.34 2018-04-10
 * @author Cay Horstmann
 */
public class NotHelloWorld
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
        {
            var frame = new NotHelloWorldFrame();
            frame.setTitle("NotHelloWorld");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }
}

/**
 * A frame that contains a message panel.
 */
class NotHelloWorldFrame extends JFrame
{
    public NotHelloWorldFrame()
    {
        add(new NotHelloWorldComponent());
        pack();
    }
}

/**
 * A component that displays a message.
 */
```

### javax.swing.JComponent 1.2
- `void paintComponent(Graphics g)`
  是要重写的方法，用于描述组件需要如何绘制。

### java.awt.Window 1.0
- `void pack()`
  调整此窗口的大小，同时考虑其组件的首选大小。

### 10.3.1 处理二维形状

从 Java 1.0 开始，`Graphics` 类具有绘制线条、矩形、椭圆等的方法。但这些绘图操作非常有限。我们将改用 *Java 2D* 库中的形状类。

要使用此库，你需要获取一个 `Graphics2D` 类的对象。该类是 `Graphics` 类的子类。从 Java 1.2 起，诸如 `paintComponent` 之类的方法会自动接收一个 `Graphics2D` 类的对象。只需使用强制类型转换，如下所示：

```java
public void paintComponent(Graphics g)
{
    Graphics2D g2 = (Graphics2D) g;
    . . .
}
```

*Java 2D* 库以面向对象的方式组织几何形状。特别是，有一些类用于表示线条、矩形和椭圆：

- `Line2D`
- `Rectangle2D`
- `Ellipse2D`

这些类都实现 `Shape` 接口。Java 2D 库支持更复杂的形状——弧、二次和三次曲线以及通用路径——本章不讨论这些内容。

要绘制形状，首先创建实现 `Shape` 接口的类的对象，然后调用 `Graphics2D` 类的 `draw` 方法。例如：

```java
Rectangle2D rect = . . .;
g2.draw(rect);
```

Java 2D 库使用浮点坐标而非整数坐标来表示像素。内部计算使用单精度 `float` 值进行。单精度已经足够——毕竟，几何计算的最终目的是在屏幕或打印机上设置像素。只要任何舍入误差保持在一个像素以内，视觉结果就不会受到影响。

然而，操作 `float` 值有时对程序员不方便，因为 Java 坚持在将 double 值转换为 float 值时要求进行强制类型转换。例如，考虑以下语句：

```java
float f = 1.2; // ERROR--possible loss of precision
```

这条语句无法编译，因为常量 1.2 的类型是 double，而编译器担心精度损失。解决办法是在浮点常量后添加 f 后缀：

```java
float f = 1.2F; // OK
```

