Before we leave the subject of drawing simple objects, this section rounds off with a simple example that demonstrates the kinds of visual effects you can achieve using brushes. The example is called ScrollMoreShapes, and it is essentially a revision of ScrollShapes. Besides the rectangle and ellipse, you will add a thick line and fill in the shapes with various custom brushes. You have already learned the principles of drawing, so the code speaks for itself. First, because of your new brushes, you need to indicate that you are using the System.Drawing.Drawing2D namespace:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Text;
using System.Windows.Forms;
```

Next are some extra fields in your Form1 class, which contain details of the locations where the shapes are to be drawn, as well as various pens and brushes you will use:

```
private Rectangle rectangleBounds = new Rectangle(new Point(0,0),
    new Size(200,200));
private Rectangle ellipseBounds = new Rectangle(new Point(50,200),
    new Size(200,150));
private readonly Pen bluePen = new Pen(Color.Blue, 3);
private readonly Pen redPen = new Pen(Color.Red, 2);
private readonly Brush solidAzureBrush = Brushes.Azure;
private readonly Brush solidYellowBrush = new SolidBrush(Color.Yellow);
private static readonly Brush brickBrush = new
    HatchBrush(HatchStyle.DiagonalBrick, Color.DarkGoldenrod, Color.Cyan);
private readonly Pen brickWidePen = new Pen(brickBrush, 10);
```

The brickBrush field has been declared as static so that you can use its value to initialize the brickWidePen field. C# will not let you use one instance field to initialize another instance field because it has not defined which one will be initialized first. However, declaring the field as static solves the problem. Because only one instance of the Form1 class will be instantiated, it is immaterial whether the fields are static or instance fields.

The following is the OnPaint() override:

```
protected override void OnPaint( PaintEventArgs e )
{
    base.OnPaint(e);
    Graphics dc = e.Graphics;
    Point scrollOffset = AutoScrollPosition;
    dc.TranslateTransform(scrollOffset.X, scrollOffset.Y);
    if (e.ClipRectangle.Top+scrollOffset.X < 350 ||
        e.ClipRectangle.Left+scrollOffset.Y < 250)
    {
        dc.DrawRectangle(bluePen, rectangleBounds);
        dc.FillRectangle(solidYellowBrush, rectangleBounds);
        dc.DrawEllipse(redPen, ellipseBounds);
        dc.FillEllipse(solidAzureBrush, ellipseBounds);
        dc.DrawLine(brickWidePen, rectangleBounds.Location,
            ellipseBounds.Location+ellipseBounds.Size);
    }
}
```

code download ScrollMoreShapes.sln

code download ScrollMoreShapes.sln