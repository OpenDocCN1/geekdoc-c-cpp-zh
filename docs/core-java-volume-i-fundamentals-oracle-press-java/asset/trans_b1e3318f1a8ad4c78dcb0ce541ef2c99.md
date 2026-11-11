

### 注意：

填充方法向右和向下会少绘制一个像素。例如，如果你绘制一个新的 `Rectangle2D.Double(0, 0, 10, 20)`，那么绘制会包含 x = 10 和 y = 20 的像素。如果你填充同一个矩形，这些像素不会被绘制。

用 Color 类定义颜色。java.awt.Color 类为以下 13 种标准颜色提供了预定义常量：

```
BLACK, BLUE, CYAN, DARK_GRAY, GRAY, GREEN, LIGHT_GRAY,
MAGENTA, ORANGE, PINK, RED, WHITE, YELLOW
```

你可以通过其红、绿、蓝分量创建 Color 对象来指定自定义颜色，每个分量的值介于 0 和 255 之间：

```java
g2.setPaint(new Color(0, 128, 128)); // a dull blue-green
g2.drawString("Welcome!", 75, 125);
```

### 注意：

除了纯色之外，你还可以使用实现了 Paint 接口的类的实例来调用 setPaint。这样就可以使用渐变和纹理进行绘制。

要设置*背景*颜色，可以使用 Component 类的 setBackground 方法，该类是 JComponent 的祖先类。

```java
var component = new MyComponent();
component.setBackground(Color.PINK);
```

还有一个 `setForeground` 方法。它指定在组件上绘制时使用的默认颜色。

### **java.awt.Color** 1.0

- `Color(int r, int g, int b)`  
  创建具有给定红、绿、蓝分量的颜色对象，分量值介于 0 和 255 之间。

### **java.awt.Graphics2D** 1.2

- `Paint getPaint()`
- `void setPaint(Paint p)`  
  获取或设置此图形上下文的 paint 属性。Color 类实现了 Paint 接口。因此，你可以使用此方法将 paint 属性设置为纯色。
- `void fill(Shape s)`  
  使用当前 paint 填充该形状。

### **java.awt.Component** 1.0

- `Color getForeground()`
- `Color getBackground()`
- `void setForeground(Color c)`
- `void setBackground(Color c)`  
  获取或设置前景色或背景色。

## 10.3.3 使用字体

本章开头展示的“不是 Hello World”程序以默认字体显示了一个字符串。有时，你会希望用不同的字体来显示文本。你可以通过*字体外观名称*来指定字体。字体外观名称由*字体族名称*（如“Helvetica”）和可选后缀（如“Bold”）组成。例如，字体外观“Helvetica”和“Helvetica Bold”都被视为名为“Helvetica”的字体族的一部分。

要查看特定计算机上有哪些可用字体，可以调用 `GraphicsEnvironment` 类的 `getAvailableFontFamilyNames` 方法。该方法返回一个字符串数组，其中包含所有可用字体的名称。要获得描述用户系统图形环境的 `GraphicsEnvironment` 类实例，可以使用静态的 `getLocalGraphicsEnvironment` 方法。下面的程序会打印你系统上所有字体的名称：

```java
import java.awt.*;
public class ListFonts
{
    public static void main(String[] args)
    {
        String[] fontNames = GraphicsEnvironment
            .getLocalGraphicsEnvironment()
            .getAvailableFontFamilyNames();
        for (String fontName : fontNames)
            System.out.println(fontName);
    }
}
```

AWT 定义了五个*逻辑*字体名称：

- SansSerif
- Serif
- Monospaced
- Dialog
- DialogInput

这些名称总是映射到客户端机器上实际存在的某些字体。例如，在 Windows 系统上，SansSerif 映射到 Arial。

此外，Oracle JDK 始终包含三个字体族，分别是“Lucida Sans”、“Lucida Bright”和“Lucida Sans Typewriter”。

要以某种字体绘制字符，必须首先创建一个 `Font` 类的对象。指定字体外观名称、字体样式和磅值。下面是一个如何构造 Font 对象的示例：

```java
var sansbold14 = new Font("SansSerif", Font.BOLD, 14);
```

第三个参数是磅值。磅是排版中常用的字体大小单位。每英寸有 72 磅。

在 `Font` 构造方法中，你可以使用逻辑字体名称代替字体外观名称。通过将 Font 构造方法的第二个参数设置为以下值之一来指定样式（常规、**粗体**、*斜体*或***粗斜体***）：

- `Font.PLAIN`
- `Font.BOLD`
- `Font.ITALIC`
- `Font.BOLD + Font.ITALIC`

该字体是常规字体，字号为 1 磅。使用 `deriveFont` 方法可以获得所需大小的字体：

![](img/0e7b74ef51a065c077b42cd87b362288_856_0.png)

### 警告：

deriveFont 方法有两个重载版本。其中一个（带 float 参数）设置字体大小，另一个（带 int 参数）设置字体样式。因此，`f1.deriveFont(14)` 设置的是样式而不是大小！（结果是*斜体*字体，因为 14 的二进制表示恰好设置了 ITALIC 位但没有设置 BOLD 位。）

下面的代码以系统上的标准无衬线字体显示字符串“Hello, World!”，使用 14 磅粗体：

```java
var sansbold14 = new Font("SansSerif", Font.BOLD, 14);
g2.setFont(sansbold14);
var message = "Hello, World!";
g2.drawString(message, 75, 100);
```

接下来，让我们将字符串*居中*显示在组件中，而不是绘制在任意位置。我们需要知道字符串的像素宽度和高度。这些尺寸取决于三个因素：

- 所使用的字体（在此例中为无衬线、粗体、14 磅）；
- 字符串（在此例中为“Hello, World!”）；以及
- 绘制字体所用的设备（在此例中为用户的屏幕）。

要获得表示屏幕设备字体特征的对象，可以调用 `Graphics2D` 类的 `getFontRenderContext` 方法。它返回一个 `FontRenderContext` 类的对象。将该对象传递给 `Font` 类的 `getStringBounds` 方法即可：

```java
FontRenderContext context = g2.getFontRenderContext();
Rectangle2D bounds = sansbold14.getStringBounds(message, context);
```

`getStringBounds` 方法返回一个包围该字符串的矩形。

要理解该矩形的尺寸，你需要了解一些基本的排版术语（参见图 10.9）。*基线*是一条假想的线，例如像 'e' 这样的字符的底部就在这条线上。*上升距离*是从基线到*上升部*顶部的距离，上升部是像 'b' 或 'k' 这样的字母或大写字母的上半部分。*下降距离*是从基线到*下降部*的距离，下降部是像 'p' 或 'g' 这样的字母的下半部分。

![](img/0e7b74ef51a065c077b42cd87b362288_858_0.png)

**图 10.9** 排版术语图示

*行距*是一行的下降距离与下一行的上升距离之间的空间。（该术语源于排版工人用来分隔线条的铅条。）字体的*高度*是连续基线之间的距离，等于下降距离 + 行距 + 上升距离。

`getStringBounds` 方法返回的矩形的宽度是字符串的水平范围。矩形的高度是上升距离、下降距离和行距之和。矩形的原点位于字符串的基线处。矩形的顶部 y 坐标为负数。因此，你可以按如下方式获得字符串的宽度、高度和上升距离：

```java
double stringWidth = bounds.getWidth();
double stringHeight = bounds.getHeight();
double ascent = -bounds.getY();
```

如果你需要知道下降距离或行距，可以使用 Font 类的 `getLineMetrics` 方法。该方法返回一个 `LineMetrics` 类的对象，该对象包含获取下降距离和行距的方法：

```java
LineMetrics metrics = f.getLineMetrics(message, context);
float descent = metrics.getDescent();
float leading = metrics.getLeading();
```

```java
6  import javax.swing.*;
7
8  /**
9   * @version 1.35 2018-04-10
10  * @author Cay Horstmann
11  */
12 public class FontTest
13 {
14    public static void main(String[] args)
15    {
16       EventQueue.invokeLater(() ->
17          {
18             var frame = new FontFrame();
19             frame.setTitle("FontTest");
20             frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
21             frame.setVisible(true);
22          });
23    }
24 }
25
26 /**
27  * A frame with a text message component.
28  */
29 class FontFrame extends JFrame
30 {
31    public FontFrame()
32    {
33       add(new FontComponent());
34       pack();
35    }
36 }
37
38 /**
39  * A component that shows a centered message in a box.
40  */
41 class FontComponent extends JComponent
42 {
43    private static final int DEFAULT_WIDTH = 300;
```

