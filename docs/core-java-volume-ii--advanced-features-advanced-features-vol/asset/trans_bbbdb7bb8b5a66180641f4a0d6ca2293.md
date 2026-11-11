
![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_727_0.png)

## 代码清单 11.15 shape/ShapeTest.java

```java
package shape;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import java.util.*;
import javax.swing.*;

/**
 * This program demonstrates the various 2D shapes.
 * @version 1.04 2018-05-01
 * @author Cay Horstmann
 */
public class ShapeTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new ShapeTestFrame();
            frame.setTitle("ShapeTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains a combo box to select a shape and a component to draw it.
 */
class ShapeTestFrame extends JFrame
{
   public ShapeTestFrame()
   {
      var comp = new ShapeComponent();
      add(comp, BorderLayout.CENTER);
      var comboBox = new JComboBox<ShapeMaker>();
      comboBox.addItem(new LineMaker());
      comboBox.addItem(new RectangleMaker());
      comboBox.addItem(new RoundRectangleMaker());
      comboBox.addItem(new EllipseMaker());
      comboBox.addItem(new ArcMaker());
      comboBox.addItem(new PolygonMaker());
      comboBox.addItem(new QuadCurveMaker());
      comboBox.addItem(new CubicCurveMaker());
      comboBox.addActionListener(event ->
         {
            ShapeMaker shapeMaker = comboBox.getItemAt(comboBox.getSelectedIndex());
            comp.setShapeMaker(shapeMaker);
         });
      add(comboBox, BorderLayout.NORTH);
      comp.setShapeMaker((ShapeMaker) comboBox.getItemAt(0));
      pack();
   }
}

/**
 * This component draws a shape and allows the user to move the points that define it.
 */
class ShapeComponent extends JComponent
{
   private static final Dimension PREFERRED_SIZE = new Dimension(300, 200);
   private Point2D[] points;
   private static final Random generator = new Random();
   private static int SIZE = 10;
   private int current;
   private ShapeMaker shapeMaker;

   public ShapeComponent()
   {
      addMouseListener(new MouseAdapter()
         {
            public void mousePressed(MouseEvent event)
            {
               Point p = event.getPoint();
               for (int i = 0; i < points.length; i++)
               {
                  double x = points[i].getX() - SIZE / 2;
                  double y = points[i].getY() - SIZE / 2;
                  var r = new Rectangle2D.Double(x, y, SIZE, SIZE);
                  if (r.contains(p))
                  {
                     current = i;
                     return;
                  }
               }
            }

            public void mouseReleased(MouseEvent event)
            {
               current = -1;
            }
         });
      addMouseMotionListener(new MouseMotionAdapter()
         {
            public void mouseDragged(MouseEvent event)
            {
               if (current == -1) return;
               points[current] = event.getPoint();
               repaint();
            }
         });
      current = -1;
   }

   /**
    * Set a shape maker and initialize it with a random point set.
    * @param aShapeMaker a shape maker that defines a shape from a point set
    */
   public void setShapeMaker(ShapeMaker aShapeMaker)
   {
      shapeMaker = aShapeMaker;
      int n = shapeMaker.getPointCount();
      points = new Point2D[n];
      for (int i = 0; i < n; i++)
      {
         double x = generator.nextDouble() * getWidth();
         double y = generator.nextDouble() * getHeight();
         points[i] = new Point2D.Double(x, y);
      }
      repaint();
   }
}
```

```java
public abstract Shape makeShape(Point2D[] p);
public String toString()
{
   return getClass().getName();
}
}

/**
 * Makes a line that joins two given points.
 */
class LineMaker extends ShapeMaker
{
   public LineMaker()
   {
      super(2);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new Line2D.Double(p[0], p[1]);
   }
}

/**
 * Makes a rectangle that joins two given corner points.
 */
class RectangleMaker extends ShapeMaker
{
   public RectangleMaker()
   {
      super(2);
   }

   public Shape makeShape(Point2D[] p)
   {
      var s = new Rectangle2D.Double();
      s.setFrameFromDiagonal(p[0], p[1]);
      return s;
   }
}

/**
 * Makes a round rectangle that joins two given corner points.
 */
class RoundRectangleMaker extends ShapeMaker
{
   public RoundRectangleMaker()
   {
```

```java
double width = Math.abs(p[1].getX() - p[0].getX());
double height = Math.abs(p[1].getY() - p[0].getY());

double skewedStartAngle = Math.toDegrees(Math.atan2(-(p[2].getY() - centerY) * width,
   (p[2].getX() - centerX) * height));
double skewedEndAngle = Math.toDegrees(Math.atan2(-(p[3].getY() - centerY) * width,
   (p[3].getX() - centerX) * height));
double skewedAngleDifference = skewedEndAngle - skewedStartAngle;
if (skewedStartAngle < 0) skewedStartAngle += 360;
if (skewedAngleDifference < 0) skewedAngleDifference += 360;

var s = new Arc2D.Double(0, 0, 0, 0,
   skewedStartAngle, skewedAngleDifference, Arc2D.OPEN);
s.setFrameFromDiagonal(p[0], p[1]);

var g = new GeneralPath();
g.append(s, false);
var r = new Rectangle2D.Double();
r.setFrameFromDiagonal(p[0], p[1]);
g.append(r, false);
var center = new Point2D.Double(centerX, centerY);
g.append(new Line2D.Double(center, p[2]), false);
g.append(new Line2D.Double(center, p[3]), false);
return g;
}
}

/**
 * Makes a polygon defined by six corner points.
 */
class PolygonMaker extends ShapeMaker
{
   public PolygonMaker()
   {
      super(6);
   }

   public Shape makeShape(Point2D[] p)
   {
      var s = new GeneralPath();
      s.moveTo((float) p[0].getX(), (float) p[0].getY());
      for (int i = 1; i < p.length; i++)
         s.lineTo((float) p[i].getX(), (float) p[i].getY());
      s.closePath();
      return s;
   }
}

/**
 * Makes a quad curve defined by two end points and a control point.
 */
class QuadCurveMaker extends ShapeMaker
{
   public QuadCurveMaker()
   {
      super(3);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new QuadCurve2D.Double(p[0].getX(), p[0].getY(), p[1].getX(), p[1].getY(),
         p[2].getX(), p[2].getY());
   }
}

/**
 * Makes a cubic curve defined by two end points and two control points.
 */
class CubicCurveMaker extends ShapeMaker
{
   public CubicCurveMaker()
   {
      super(4);
   }

   public Shape makeShape(Point2D[] p)
   {
      return new CubicCurve2D.Double(p[0].getX(), p[0].getY(), p[1].getX(), p[1].getY(),
         p[2].getX(), p[2].getY(), p[3].getX(), p[3].getY());
   }
}
```

- **java.awt.geom.RoundRectangle2D.Double** 1.2
  - `RoundRectangle2D.Double(double x, double y, double width, double height, double arcWidth, double arcHeight)` 使用给定的边界矩形和弧尺寸构造一个圆角矩形。arcWidth 和 arcHeight 参数的解释见图 11.34。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_737_0.png)

**图 11.40** 构造区域几何操作

Area 类实现了 Shape 接口。可以使用 Graphics2D 类的 draw 方法描边区域边界，或使用 fill 方法填充内部。

| `java.awt.geom.Area` |
|---|
| - `void add(Area other)`<br>- `void subtract(Area other)`<br>- `void intersect(Area other)`<br>- `void exclusiveOr(Area other)`<br><br>使用此区域和另一个区域执行构造区域几何操作，并将此区域设置为结果。 |

### 11.3.4 描边

Graphics2D 类的 draw 操作使用当前选定的描边绘制形状边界。默认情况下，描边是宽度为 1 像素的实线。可以通过调用 setStroke 方法并提供实现 Stroke 接口的类的对象来选择不同的描边。Java 2D API 只定义了一个这样的类，称为 BasicStroke。本节将介绍 BasicStroke 类的功能。

