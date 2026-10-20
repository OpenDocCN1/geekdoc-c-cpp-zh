
显示由参数 xValues2、yValues2 和 7（点的数量）指定的连接线系列。

第26–27行创建了两个 int 数组，并使用它们来指定多边形的点。数组 xValues3 包含每个点的 x 坐标，数组 yValues3 包含每个点的 y 坐标。第28行通过向 Graphics 的 fillPolygon 方法传递这两个数组（xValues3 和 yValues3）以及要绘制的点的数量（4）来显示一个多边形。

> **常见编程错误 15.1**
>
> *如果将 drawPolygon 方法或 fillPolygon 方法的第三个参数中指定的点的数量大于用于指定要显示多边形的坐标数组中的元素数量，则抛出 ArrayIndexOutOfBoundsException。*

第31行创建了一个没有点的 Polygon polygon2。第32–36行使用 Polygon 的 **addPoint** 方法将 x 和 y 坐标对添加到该 Polygon。第37行通过将 Polygon polygon2 传递给 Graphics 的 fillPolygon 方法来显示它。

## 15.8 Java 2D API

Java 2D API 为需要详细且复杂图形操作的程序员提供了高级二维图形功能。该 API 包含在 java.awt、java.awt.image、java.awt.color、java.awt.font、java.awt.geom、java.awt.print 和 java.awt.image.renderable 包中处理线条图、文本和图像的特性。该 API 的功能过于广泛，本教材无法全部覆盖。有关概述，请参阅 Java 2D 演示（在第23章“小程序与 Java Web Start”中讨论）或访问 download.oracle.com/javase/6/docs/technotes/guides/2d/。在本节中，我们概述几个 Java 2D 功能。

使用 Java 2D API 绘图是通过 **Graphics2D** 引用（包 java.awt）实现的。Graphics2D 是 Graphics 类的抽象子类，因此它拥有本章先前演示的所有图形功能。实际上，每个 paintComponent 方法中用于绘制的实际对象是 Graphics2D 的一个子类的实例，该实例被传递给 paintComponent 方法，并通过超类 Graphics 进行访问。要访问 Graphics2D 的功能，我们必须将传递给 paintComponent 的 Graphics 引用（g）转换为 Graphics2D 引用，使用的语句如下：

```java
Graphics2D g2d = ( Graphics2D ) g;
```

接下来的两个示例使用了这一技术。

### 线条、矩形、圆角矩形、弧和椭圆

此示例演示了来自 java.awt.geom 包中的几个 Java 2D 形状，包括 **Line2D.Double、Rectangle2D.Double、RoundRectangle2D.Double、Arc2D.Double** 和 **Ellipse2D.Double**。注意每个类名的语法。每个类表示一个尺寸以 double 值指定的形状。还有一个以 float 值表示的单独版本（例如，**Ellipse2D.Float**）。在每种情况下，Double 都是点左侧指定类的公共静态嵌套类（例如 Ellipse2D）。要使用静态嵌套类，我们只需用外部类名限定其名称。

在图15.29–15.30中，我们绘制了 Java 2D 形状并修改了它们的绘制特性，例如更改线条粗细、用图案填充形状以及绘制虚线。这些只是 Java 2D 提供的众多功能中的一小部分。

图15.29的第25行将 paintComponent 收到的 Graphics 引用转换为 Graphics2D 引用，并将其赋值给 g2d，以便访问 Java 2D 功能。

```java
// Fig. 15.29: ShapesJPanel.java
// Demonstrating some Java 2D shapes.
import java.awt.Color;
import java.awt.Graphics;
import java.awt.BasicStroke;
import java.awt.GradientPaint;
import java.awt.TexturePaint;
import java.awt.Rectangle;
import java.awt.Graphics2D;
import java.awt.geom.Ellipse2D;
import java.awt.geom.Rectangle2D;
import java.awt.geom.RoundRectangle2D;
import java.awt.geom.Arc2D;
import java.awt.geom.Line2D;
import java.awt.image.BufferedImage;
import javax.swing.JPanel;

public class ShapesJPanel extends JPanel
{
    // draw shapes with Java 2D API
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g ); // call superclass's paintComponent

        Graphics2D g2d = ( Graphics2D ) g; // cast g to Graphics2D

        // draw 2D ellipse filled with a blue-yellow gradient
        g2d.setPaint( new GradientPaint( 5, 30, Color.BLUE, 35, 100, Color.YELLOW, true ) );
        g2d.fill( new Ellipse2D.Double( 5, 30, 65, 100 ) );

        // draw 2D rectangle in red
        g2d.setPaint( Color.RED );
        g2d.setStroke( new BasicStroke( 10.0f ) );
        g2d.draw( new Rectangle2D.Double( 80, 30, 65, 100 ) );

        // draw 2D rounded rectangle with a buffered background
        BufferedImage buffImage = new BufferedImage( 10, 10, BufferedImage.TYPE_INT_RGB );

        // obtain Graphics2D from buffImage and draw on it
        Graphics2D gg = buffImage.createGraphics();
        gg.setColor( Color.YELLOW ); // draw in yellow
        gg.fillRect( 0, 0, 10, 10 ); // draw a filled rectangle
        gg.setColor( Color.BLACK ); // draw in black
        gg.drawRect( 1, 1, 6, 6 ); // draw a rectangle
        gg.setColor( Color.BLUE ); // draw in blue
        gg.fillRect( 1, 1, 3, 3 ); // draw a filled rectangle
        gg.setColor( Color.RED ); // draw in red
        gg.fillRect( 4, 4, 3, 3 ); // draw a filled rectangle

        // paint buffImage onto the JFrame
        g2d.setPaint( new TexturePaint( buffImage,
            new Rectangle( 10, 10 ) ) );
        g2d.fill(
            new RoundRectangle2D.Double( 155, 30, 75, 100, 50, 50 ) );

        // draw 2D pie-shaped arc in white
        g2d.setPaint( Color.WHITE );
        g2d.setStroke( new BasicStroke( 6.0F ) );
        g2d.draw(
            new Arc2D.Double( 240, 30, 75, 100, 0, 270, Arc2D.PIE ) );

        // draw 2D lines in green and yellow
        g2d.setPaint( Color.GREEN );
        g2d.draw( new Line2D.Double( 395, 30, 320, 150 ) );

        // draw 2D line using stroke
        float[] dashes = { 10 }; // specify dash pattern
        g2d.setPaint( Color.YELLOW );
        g2d.setStroke( new BasicStroke( 4, BasicStroke.CAP_ROUND,
            BasicStroke.JOIN_ROUND, 10, dashes, 0 ) );
        g2d.draw( new Line2D.Double( 320, 30, 395, 150 ) );
    } // end method paintComponent
} // end class ShapesJPanel
```

图15.29 | Java 2D 形状。（第2部分，共2部分。）

```java
// Fig. 15.30: Shapes.java
// Demonstrating some Java 2D shapes.
import javax.swing.JFrame;

public class Shapes
{
    // execute application
    public static void main( String[] args )
    {
        // create frame for ShapesJPanel
        JFrame frame = new JFrame( "Drawing 2D shapes" );
        frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );

        // create ShapesJPanel
        ShapesJPanel shapesJPanel = new ShapesJPanel();

        frame.add( shapesJPanel ); // add shapesJPanel to frame
        frame.setSize( 425, 200 ); // set frame size
        frame.setVisible( true ); // display frame
    } // end main
} // end class Shapes
```

图15.30 | 创建 JFrame 以显示形状。（第1部分，共2部分。）

![](img/009e962758dcc71dbc43a493362e6dc0_697_0.png)

图15.30 | 创建 JFrame 以显示形状。（第2部分，共2部分。）

### 椭圆、渐变填充和 Paint 对象

我们绘制的第一个形状是一个以逐渐变化颜色填充的椭圆。第28–29行调用 Graphics2D 的 setPaint 方法来设置 Paint 对象，该对象决定要显示形状的颜色。Paint 对象实现 java.awt.Paint 接口。它可以像15.3节中引入的预声明 Color 对象一样简单（Color 类实现了 Paint），也可以是 Java 2D API 的 GradientPaint、SystemColor、TexturePaint、LinearGradientPaint 或 RadialGradientPaint 类的一个实例。在本例中，我们使用了一个 GradientPaint 对象。

GradientPaint 类有助于以逐渐变化的颜色绘制形状——称为渐变。此处使用的 GradientPaint 构造函数需要七个参数。前两个指定渐变的起始坐标。第三个指定渐变的起始颜色。第四和第五个指定渐变的结束坐标。第六个指定渐变的结束颜色。最后一个参数指定渐变是循环的（true）还是非循环的（false）。这两组坐标决定了渐变的方向。由于第二个坐标（35, 100）位于第一个坐标（5, 30）的右下方，渐变以一定角度向右下方延伸。由于此渐变是循环的（true），颜色从蓝色开始，逐渐变为黄色，然后逐渐变回蓝色。如果渐变是非循环的，颜色从指定的第一种颜色（例如蓝色）过渡到第二种颜色（例如黄色）。

第30行使用 Graphics2D 的 fill 方法来绘制一个填充的 Shape 对象——即实现 Shape 接口（包 java.awt）的对象。在本例中，我们显示一个 Ellipse2D.Double 对象。Ellipse2D.Double 构造函数接收四个参数，指定要显示椭圆的边界矩形。

### 矩形与描边

接下来我们绘制一个带粗边框的红色矩形。第33行调用 setPaint 将 Paint 对象设置为 Color.RED。第34行使用 Graphics2D 的 setStroke 方法来设置矩形边框（或任何其他形状的线条）的特性。setStroke 方法要求其参数为实现 Stroke 接口（包 java.awt）的对象。在本例中，我们使用了 BasicStroke 类的一个实例。BasicStroke 类提供了多个构造函数，用于指定线条的宽度、线条的端部样式（称为端帽）、线条的连接方式（称为线条连接）以及线条的虚线属性（如果是虚线的话）。此处的构造函数指定线条宽度应为10像素。

第35行使用 Graphics2D 的 draw 方法绘制一个 Shape 对象——本例中是一个 Rectangle2D.Double。Rectangle2D.Double 构造函数接收的参数指定矩形的左上角 x 坐标、左上角 y 坐标、宽度和高度。
