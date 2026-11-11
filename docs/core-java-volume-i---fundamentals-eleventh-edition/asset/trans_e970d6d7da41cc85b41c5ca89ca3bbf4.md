
显示是以像素为单位完成的。(0, 0) 坐标表示你正在其表面绘制的组件的左上角。

Graphics 类有多种绘制方法，而显示文本被视为一种特殊的绘制。我们的 paintComponent 方法如下所示：

```java
public class NotHelloWorldComponent extends JComponent
{
   public static final int MESSAGE_X = 75;
   public static final int MESSAGE_Y = 100;

   public void paintComponent(Graphics g)
   {
      g.drawString("Not a Hello, World program", MESSAGE_X, MESSAGE_Y);
   }
   . . .
}
```

最后，组件应让用户知道它希望有多大。重写 getPreferredSize 方法，并返回一个 Dimension 类对象，其中包含首选宽度和高度：

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

当你用一个或多个组件填充框架，并且只想使用它们的首选尺寸时，应调用 pack 方法而不是 setSize 方法：

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

代码清单 10.2 显示了完整代码。

## 代码清单 10.2 `notHelloWorld/NotHelloWorld.java`

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
class NotHelloWorldComponent extends JComponent
{
   public static final int MESSAGE_X = 75;
   public static final int MESSAGE_Y = 100;

   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;

   public void paintComponent(Graphics g)
   {
      g.drawString("Not a Hello, World program", MESSAGE_X, MESSAGE_Y);
   }

   public Dimension getPreferredSize()
   {
      return new Dimension(DEFAULT_WIDTH, DEFAULT_HEIGHT);
   }
}
```

| javax.swing.JFrame 1.2 |
| --- |
| • `Component add(Component c)`<br>将给定组件添加到此框架的内容窗格并返回该组件。 |

| java.awt.Component 1.0 |
| --- |
| • `void repaint()`<br>使组件“尽快”重绘。<br><br>• `Dimension getPreferredSize()`<br>是要重写以返回此组件首选尺寸的方法。 |

| javax.swing.JComponent 1.2 |
| --- |
| • `void paintComponent(Graphics g)`<br>是要重写以描述组件需要如何绘制的方法。 |

| java.awt.Window 1.0 |
| --- |
| • `void pack()`<br>调整此窗口大小，同时考虑其各组件的首选尺寸。 |

### 10.3.1 使用 2D 形状

从 Java 1.0 开始，Graphics 类就有绘制线条、矩形、椭圆等的方法。但这些绘制操作非常有限。我们将改用 Java 2D 库中的形状类。

要使用此库，你需要获得一个 Graphics2D 类的对象。这个类是 Graphics 类的子类。从 Java 1.2 开始，诸如 paintComponent 之类的方法会自动接收一个 Graphics2D 类的对象。只需按如下方式进行强制转换：

```java
public void paintComponent(Graphics g)
{
    Graphics2D g2 = (Graphics2D) g;
    . . .
}
```

Java 2D 库以面向对象的方式组织几何形状。特别地，有一些类用于表示线条、矩形和椭圆：

- `Line2D`
- `Rectangle2D`
- `Ellipse2D`

这些类都实现了 Shape 接口。Java 2D 库支持更复杂的形状——弧线、二次和三次曲线以及一般路径——本章不讨论这些内容。

要绘制形状，首先创建实现 Shape 接口的类的对象，然后调用 Graphics2D 类的 draw 方法。例如：

```java
Rectangle2D rect = . . .;
g2.draw(rect);
```

Java 2D 库使用浮点坐标（而不是整数）表示像素。内部计算使用单精度 float 数值进行。单精度已经足够——毕竟，几何计算的最终目的是在屏幕或打印机上设置像素。只要任何舍入误差保持在一个像素以内，视觉结果就不会受到影响。

然而，操作 float 值有时对程序员来说不太方便，因为 Java 在将 double 值转换为 float 值时会坚持要求强制转换。例如，考虑以下语句：

```java
float f = 1.2; // ERROR--possible loss of precision
```

这条语句无法编译，因为常量 1.2 的类型是 double，编译器担心精度损失。解决办法是为浮点常量添加 F 后缀：

```java
float f = 1.2F; // OK
```

现在考虑这条语句：

```java
float f = r.getWidth(); // ERROR
```

由于同样的原因，这条语句也无法编译。getWidth 方法返回 double。这一次，解决办法是提供强制转换：

```java
float f = (float) r.getWidth(); // OK
```

这些后缀和强制转换有点麻烦，因此 2D 库的设计者决定为每个形状类提供*两个版本*：一个使用 `float` 坐标，供注重节省的程序员使用；另一个使用 `double` 坐标，供图省事的程序员使用。（在本书中，我们属于后一阵营，尽可能使用 `double` 坐标。）

库设计者选择了一种奇特的方式来封装这些选择。考虑 `Rectangle2D` 类。这是一个抽象类，有两个具体子类，它们也是静态内部类：

- `Rectangle2D.Float`
- `Rectangle2D.Double`

图 10.5 显示了继承关系图。

![](img/127bccebb2cfadea3f02579edaad63c3_607_0.png)

**图 10.5** 2D 矩形类

最好忽略这两个具体类是静态内部类这一事实——这只是一个避免使用 `FloatRectangle2D` 和 `DoubleRectangle2D` 之类名称的小花招。

构造 `Rectangle2D.Float` 对象时，需要以 `float` 数值提供坐标。对于 `Rectangle2D.Double` 对象，则以 `double` 数值提供坐标。

```java
var floatRect = new Rectangle2D.Float(10.0F, 25.0F, 22.5F, 20.0F);
var doubleRect = new Rectangle2D.Double(10.0, 25.0, 22.5, 20.0);
```

构造参数表示矩形的左上角、宽度和高度。

`Rectangle2D` 的方法使用 `double` 参数和返回值。例如，即使宽度在 `Rectangle2D.Float` 对象中以 `float` 存储，`getWidth` 方法仍返回 `double` 值。

> **提示：** 直接使用 `Double` 形状类，以完全避免处理 `float` 值。但是，如果你要构造数千个形状对象，请考虑使用 `Float` 类以节省内存。

我们刚刚讨论的 `Rectangle2D` 类的情况也适用于其他形状类。此外，还有一个 `Point2D` 类，其子类为 `Point2D.Float` 和 `Point2D.Double`。下面是创建点对象的方法：

```java
var p = new Point2D.Double(10, 20);
```

`Rectangle2D` 和 `Ellipse2D` 类都继承自共同的超类 `RectangularShape`。诚然，椭圆并不是矩形，但它们有一个*边界矩形*（见图 10.6）。

![](img/127bccebb2cfadea3f02579edaad63c3_608_0.png)

**图 10.6** 椭圆的边界矩形

`RectangularShape` 类定义了 20 多个这些形状共有的方法，其中包括 `getWidth`、`getHeight`、`getCenterX` 和 `getCenterY` 等有用方法（但遗憾的是，在撰写本书时，还没有一个能将中心作为 `Point2D` 对象返回的 `getCenter` 方法）。

最后，Java 1.0 中的几个遗留类也被纳入形状类层次结构中。`Rectangle` 和 `Point` 类分别存储具有整数坐标的矩形和点，它们扩展了 `Rectangle2D` 和 `Point2D` 类。图 10.7 显示了形状类之间的关系。但是，省略了 `Double` 和 `Float` 子类。遗留类用灰色填充标记。
