
> PointF and SizeF are used to indicate floating point values, which are necessary when drawing with pixels.

## Brushes & Pens

We can also use what are known as brushes and pens to enhance graphics and text-supported displays. Brushes and pens are declared and accessed in basically the same manner, with brushes being used for text and to fill, rather than to draw shapes. Brushes are also abstract by definition and hence cannot be instantiated. There are, however, five derived classes used to create different types of brushes: HatchBrush, LinearGradientBrush, PathGradientBrush, SolidBrush, and TextureBrush. Pen is also derived from the abstract brush class; it can be written to take advantage of all five of the derived classes, but it has a constant color rather than a gradient. For our purposes, we'll want to look at how to declare and reference both the basic SolidBrush and the pen (see Example F.2).

### Example F.2.

```
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_F {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {}
        protected override void OnPaint(PaintEventArgs e) {
            Graphics Figures = this.CreateGraphics();
            Brush RedBrush = new SolidBrush(Color.Red);
            Pen BluePen = new Pen(Color.Blue, 3);
            Figures.FillRectangle(RedBrush, 10, 10, 25, 25);
            Figures.DrawRectangle(BluePen, 20, 20, 25, 25);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```

> The second value associated with the pen statement, Pen(Color, int), is used to reference its width.

## Lines

Now that we have some basic points to reference and our pen in hand, the next logical step is to learn how to link those points to create lines and, of course, curves. Lines are straightforward enough, with four basic references: DrawLine(Color, Point1, Point2), DrawLine(Color, int x, int y, int x2, int y2), DrawLine(Color, PointF1, PointF2), and DrawLine(Color, float x, float y, float x2, float y2)—see Example F.3.

### Example F.3.

```
~~~csharp
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_F {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {}
        protected override void OnPaint(PaintEventArgs e) {
            Point point1 = new Point(10, 10);
            Point point2 = new Point(250, 250);
            PointF pointF1 = new PointF(125F, 10F);
            PointF pointF2 = new PointF(125F, 250F);

            Graphics Figures = this.CreateGraphics();
            Pen RedPen = new Pen(Color.Red);
            Pen GreenPen = new Pen(Color.Green);
            Pen BluePen = new Pen(Color.Blue);
            Pen YellowPen = new Pen(Color.Yellow);

            Figures.DrawLine(RedPen, point1, point2);
            Figures.DrawLine(GreenPen, 250, 10, 10, 250);
            Figures.DrawLine(BluePen, pointF1, pointF2);
            Figures.DrawLine(YellowPen, 10F, 125F, 250F, 125F);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
~~~
```

## Curves

Curves are a bit more complex with seven, potential references: DrawCurve(Color, ArrayOfPoints, Offset, Segment, Tension); DrawCurve(Color, ArrayOfPoints, Tension); DrawCurve(Color, ArrayOfPoints); DrawCurve(Color, ArrayOfPoints, Offset, Segment, Tension); DrawCurve(Color, ArrayOfPoints, Offset, Segment); DrawCurve(Color, ArrayOfPoints, Tension); and DrawCurve(Color, ArrayOfPoints)—see Example F.4.

### Example F.4.

```
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_F {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {}
        protected override void OnPaint(PaintEventArgs e) {
            PointF pointF1 = new PointF(125F, 10F);
            PointF pointF2 = new PointF(125F, 125F);
            PointF pointF3 = new PointF(250F, 250F);
            PointF pointF4 = new PointF(250F, 150F);
            PointF pointF5 = new PointF(150F, 100F);
            PointF pointF6 = new PointF(250F, 200F);
            PointF pointF7 = new PointF(125F, 125F);

            PointF[] ArrayOfPoints = {pointF1, pointF2, pointF3, pointF4, pointF5, pointF6, pointF7};

            Graphics Figures = this.CreateGraphics();
            Pen RedPen = new Pen(Color.Red);

            Figures.DrawCurve(RedPen, ArrayOfPoints, 2, 4, 1.0F);
            Figures.DrawCurve(RedPen, ArrayOfPoints, 0);
            Figures.DrawCurve(RedPen, ArrayOfPoints);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```

## Drawing Shapes

We'll definitely want to take advantage of all the potential shapes stored in the Windows Forms. We'll look at the basic ellipse, polygon, and rectangle. We'll also want to have a look at the FillPolygon and FillPie (see Example F.5).

### Example F.5.

```
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_F {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {}
        protected override void OnPaint(PaintEventArgs e) {
            Point point1 = new Point(10, 10);
            Point point2 = new Point(250, 250);
            PointF pointF1 = new PointF(125F, 10F);
            PointF pointF2 = new PointF(125F, 125F);
            PointF pointF3 = new PointF(250F, 250F);
            PointF pointF4 = new PointF(250.0F, 150.0F);
            PointF pointF5 = new PointF(150F, 100F);
            PointF pointF6 = new PointF(250F, 200F);
            PointF pointF7 = new PointF(125F, 125F);
            PointF[] ArrayOfPoints = {pointF1, pointF2, pointF3, pointF4, pointF5, pointF6, pointF7};
            Graphics Figures = this.CreateGraphics();
            Pen RedPen = new Pen(Color.Red);
            Pen GreenPen = new Pen(Color.Green);
            Pen BluePen = new Pen(Color.Blue);
            Brush YellowBrush = Brushes.Yellow;
            Brush OrangeBrush = Brushes.Orange;
            Figures.DrawRectangle(RedPen, 10, 10, 100, 100);
            Figures.DrawEllipse(GreenPen, 25, 25, 50, 50);
            Figures.DrawPolygon(BluePen, ArrayOfPoints);
            Figures.FillPolygon(YellowBrush, ArrayOfPoints);
            Figures.FillPie(OrangeBrush, 40, 150, 70, 70, 40, 50);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```

Diagonal lines can also be created using DrawLine, but if the line is asymmetrical it will appear coarse or jagged. In GDI+, a solution known as anti-aliasing is used. Anti-aliasing is a smoothing technique, based on shading, which is used to reduce sharpness. To the artist this would mean including a softer shade of the line's color that surrounds the line; thus, to the programmer this will mean adding additional lines.

Once we have the basic shapes, creating complex designs becomes nothing more than a question of ingenuity. Here, we'll combine a triangle, three rectangles, and a few area fills to create a small house and a garden (see Example F.6).

### Example F.6.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Chapter3 {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {}
        protected override void OnPaint(PaintEventArgs e) {
            //Triangle
            PointF pointf1 = new PointF(125F, 50F);
            PointF pointf2 = new PointF(50F, 110F);
            PointF pointf3 = new PointF(200F, 110F);
            PointF[] ArrayOfPoints = {pointf1, pointf2, pointf3};

            Graphics Figures = this.CreateGraphics();
            Brush GreenBrush = Brushes.Green;
            Brush BlueBrush = Brushes.Aqua;
            Brush BrownBrush = Brushes.Brown;
            Brush BurlyWoodBrush = Brushes.BurlyWood;
            Figures.FillRectangle(BlueBrush, 0, 0, 300, 175);
            Figures.FillRectangle(BurlyWoodBrush, 75, 90, 100, 85);
            Figures.FillRectangle(BrownBrush, 90, 140, 20, 35);
            Figures.FillRectangle(BrownBrush, 130, 130, 30, 30);
            Figures.FillRectangle(GreenBrush, 0, 175, 300, 175);
            Figures.FillPolygon(BrownBrush, ArrayOfPoints);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```
