

```
16      frame.setSize( 420, 150 ); // set frame size
17      frame.setVisible( true ); // display frame
18  } // end main
19 } // end class Fonts
```

![](img/009e962758dcc71dbc43a493362e6dc0_682_0.png)

Fig. 15.12 | Creating a JFrame to display fonts. (Part 2 of 2.)

## Font Metrics

有时需要获取有关当前绘图字体的信息，例如其名称、样式和大小。用于获取字体信息的若干 Font 方法已在图 15.10 中进行了总结。方法 getStyle 返回表示当前样式的整数值。返回的整数值要么是 Font.PLAIN、Font.ITALIC、Font.BOLD，要么是 Font.ITALIC 和 Font.BOLD 的组合。方法 getFamily 返回当前字体所属的字体族的名称。字体族的名称是平台相关的。Font 方法还可用于测试当前字体的样式，这些方法也在图 15.10 中进行了总结。方法 isPlain、isBold 和 isItalic 分别在当前字体样式为普通、粗体或斜体时返回 true。

图 15.13 说明了一些常见的字体度量，它们提供了有关字体的精确信息，例如高度、下降部（字符低于基线的量）、上升部（字符高于基线的量）和行距（即一行文本的下降部与下一行文本的上升部之间的差值——即行间间距）。

![](img/009e962758dcc71dbc43a493362e6dc0_682_1.png)

Fig. 15.13 | Font metrics.

类 FontMetrics 声明了若干用于获取字体度量的 方法。这些方法和 Graphics 方法 getFontMetrics 已在图 15.14 中进行了总结。图 15.15–15.16 的应用程序使用图 15.14 中的方法为两种字体获取字体度量信息。

| Method | Description |
|---|---|
| *FontMetrics methods* | |
| public int getAscent() | Returns the ascent of a font in points. |
| public int getDescent() | Returns the descent of a font in points. |
| public int getLeading() | Returns the leading of a font in points. |
| public int getHeight() | Returns the height of a font in points. |
| *Graphics methods for getting a Font's FontMetrics* | |
| public FontMetrics getFontMetrics() | Returns the FontMetrics object for the current drawing Font. |
| public FontMetrics getFontMetrics( Font f ) | Returns the FontMetrics object for the specified Font argument. |

Fig. 15.14 | FontMetrics and Graphics methods for obtaining font metrics.

```
1  // Fig. 15.15: MetricsJPanel.java
2  // FontMetrics and Graphics methods useful for obtaining font metrics.
3  import java.awt.Font;
4  import java.awt.FontMetrics;
5  import java.awt.Graphics;
6  import javax.swing.JPanel;
7
8  public class MetricsJPanel extends JPanel
9  {
10     // display font metrics
11     public void paintComponent( Graphics g )
12     {
13         super.paintComponent( g ); // call superclass's paintComponent
14
15         g.setFont( new Font( "SansSerif", Font.BOLD, 12 ) );
16         FontMetrics metrics = g.getFontMetrics();
17         g.drawString( "Current font: " + g.getFont(), 10, 30 );
18         g.drawString( "Ascent: " + metrics.getAscent(), 10, 45 );
19         g.drawString( "Descent: " + metrics.getDescent(), 10, 60 );
20         g.drawString( "Height: " + metrics.getHeight(), 10, 75 );
21         g.drawString( "Leading: " + metrics.getLeading(), 10, 90 );
22
23         Font font = new Font( "Serif", Font.ITALIC, 14 );
24         metrics = g.getFontMetrics( font );
25         g.setFont( font );
26         g.drawString( "Current font: " + font, 10, 120 );
27         g.drawString( "Ascent: " + metrics.getAscent(), 10, 135 );
28         g.drawString( "Descent: " + metrics.getDescent(), 10, 150 );
29         g.drawString( "Height: " + metrics.getHeight(), 10, 165 );
30         g.drawString( "Leading: " + metrics.getLeading(), 10, 180 );
31     } // end method paintComponent
32 } // end class MetricsJPanel
```

Fig. 15.15 | Font metrics.

图 15.18–15.19 的应用程序演示了绘制各种线条、矩形、三维矩形、圆角矩形和椭圆。在图 15.18 中，第 17 行绘制了一条红色线条，第 20 行绘制了一个空心蓝色矩形，第 21 行绘制了一个填充的蓝色矩形。方法 fillRoundRect（第 24 行）和 drawRoundRect（第 25 行）绘制具有圆角的矩形。它们的前两个参数指定包围矩形的左上角坐标——即圆角矩形将被绘制的区域。左上角坐标不是圆角矩形的边缘，而是矩形如果具有方形角落时边缘所在的位置。第三个和第四个参数指定矩形的宽度和高度。最后两个参数决定用于表示角落的弧的水平直径和垂直直径（即弧宽和弧高）。

图 15.20 标记了圆角矩形的弧宽、弧高、宽度和高度。使用相同的值作为弧宽和弧高会在每个角落产生四分之一圆。当弧宽、弧高、宽度和高度具有相同的值时，结果是一个圆。如果宽度和高度的值相同且 arcWidth 和 arcHeight 的值为 0，则结果是一个正方形。

方法 draw3DRect（第 28 行）和 fill3DRect（第 29 行）接受相同的参数。前两个参数指定矩形的左上角。接下来的两个参数分别指定矩形的宽度和高度。最后一个参数决定矩形是凸起（true）还是凹下（false）。draw3DRect 的三维效果表现为矩形的两条边为原始颜色，两条边为稍暗的颜色。fill3DRect 的三维效果表现为矩形的两条边为原始绘图颜色和填充色，另外两条边为稍暗的颜色。凸起的矩形在矩形的顶部和左侧具有原始绘图颜色的边。凹下的矩形在矩形的底部和右侧具有原始绘图颜色的边。在某些颜色中，三维效果很难看到。

方法 drawOval 和 fillOval（图 15.18，第 32–33 行）接受相同的四个参数。前两个参数指定包含椭圆的包围矩形的左上角坐标。最后两个参数分别指定包围矩形的宽度和高度。图 15.21 显示了一个由矩形包围的椭圆。椭圆触及包围矩形四条边的中心。（包围矩形不会在屏幕上显示。）

![](img/009e962758dcc71dbc43a493362e6dc0_688_0.png)

Fig. 15.21 | Oval bounded by a rectangle.

## 15.6 Drawing Arcs

弧是作为椭圆的一部分绘制的。弧的角度以度为单位测量。弧从起始角度开始沿曲线移动，通过其弧角度指定的度数。起始角度以度表示弧的开始位置。弧角度指定弧扫过的总度数。图 15.22 说明了两个弧。左侧的坐标轴显示了一个从零度扫到大约 110 度的弧。逆时针扫过的弧以正度数测量。右侧的坐标轴显示了一个从零度扫到大约 −110 度的弧。顺时针扫过的弧以负度数测量。请注意图 15.22 中弧周围的虚线框。绘制弧时，我们指定一个用于椭圆的包围矩形。弧将沿椭圆的一部分扫过。用于绘制弧的 Graphics 方法 drawArc 和 fillArc 已在图 15.23 中进行了总结。

```
// Fig. 15.18: LinesRectsOvalsJPanel.java
// Drawing lines, rectangles and ovals.
import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JPanel;

public class LinesRectsOvalsJPanel extends JPanel
{
    // display various lines, rectangles and ovals
    public void paintComponent( Graphics g )
    {
        super.paintComponent( g ); // call superclass's paint method

        this.setBackground( Color.WHITE );

        g.setColor( Color.RED );
        g.drawLine( 5, 30, 380, 30 );

        g.setColor( Color.BLUE );
        g.drawRect( 5, 40, 90, 55 );
        g.fillRect( 100, 40, 90, 55 );

        g.setColor( Color.CYAN );
        g.fillRoundRect( 195, 40, 90, 55, 50, 50 );
        g.drawRoundRect( 290, 40, 90, 55, 20, 20 );

        g.setColor( Color.GREEN );
        g.draw3DRect( 5, 100, 90, 55, true );
        g.fill3DRect( 100, 100, 90, 55, false );

        g.setColor( Color.MAGENTA );
        g.drawOval( 195, 100, 90, 55 );
        g.fillOval( 290, 100, 90, 55 );
    } // end method paintComponent
} // end class LinesRectsOvalsJPanel
```

```
// Fig. 15.19: LinesRectsOvals.java
// Drawing lines, rectangles and ovals.
import java.awt.Color;
import javax.swing.JFrame;

public class LinesRectsOvals
{
    // execute application
    public static void main( String[] args )
    {
        // create frame for LinesRectsOvalsJPanel
        JFrame frame =
            new JFrame( "Drawing lines, rectangles and ovals" );
        frame.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );

        LinesRectsOvalsJPanel linesRectsOvalsJPanel =
            new LinesRectsOvalsJPanel();
        linesRectsOvalsJPanel.setBackground( Color.WHITE );
        frame.add( linesRectsOvalsJPanel ); // add panel to frame
        frame.setSize( 400, 210 ); // set frame size
        frame.setVisible( true ); // display frame
    } // end main
} // end class LinesRectsOvals
```

![](img/009e962758dcc71dbc43a493362e6dc0_687_0.png)

Fig. 15.19 | Creating JFrame to display lines, rectangles and ovals.

![](img/009e962758dcc71dbc43a493362e6dc0_687_1.png)

Fig. 15.20 | Arc width and arc height for rounded rectangles.

