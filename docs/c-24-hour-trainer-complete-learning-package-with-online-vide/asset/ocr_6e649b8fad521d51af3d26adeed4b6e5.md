```
viewbox.Stretch = Stretch.Uniform;
}
// Make a VisualBrush holding an image of the Window's contents.
VisualBrush br = new VisualBrush(win);

// Make a Rectangle the size of the Window.
Rectangle windowRect = new Rectangle();
viewbox.Child = windowRect;
windowRect.Width = win.Width;
windowRect.Height = win.Height;
windowRect.Fill = br;
windowRect.Stroke = Brushes.Black;
windowRect.Effect = new DropShadowEffect();

// Arrange to produce output.
Rect rect = new Rect(0, 0,
printDialog.PrintableAreaWidth, printDialog.PrintableAreaHeight);
drawingGrid.Arrange(rect);

// Print it.
printDialog.PrintVisual(drawingGrid, title);
}
```

> NOTE This code adds a DropShadowEffect behind the grid. That class is defined in the System.Windows.Media.Effects namespace, so to make using it easier, the program includes the following using directive:
> 
> using System.Windows.Media.Effects;

When you click the Print button, the program displays a PrintDialog as before. If you select a printer and click Print, the program calls the PrintWindowCentered method, passing it the PrintDialog object and the Window to print. It also passes the method a title to use for the printout and a margin (which can be null).

The PrintWindowCentered method makes a Grid that fills the printer's printable area. Inside the Grid it places a Viewbox named viewbox. A Viewbox displays a single object that it can optionally stretch in various ways.

If the method receives a margin parameter, the program sets the Viewbox's margin appropriately and makes the control stretch its contents so they are as large as possible without changing shape. If the margin parameter is null, the code makes the Viewbox not stretch its contents.

Next the code makes a VisualBrush from the Window. A VisualBrush fills an area with the image of some visual object such as a control or, in this case, the program's main Window. The code creates a Rectangle, places it inside the Viewbox, and fills it with the brush.

At this point, all of the objects needed to display the Window appropriately sized and centered on the printed page are in place. The code only needs to perform two more steps.

First, it calls the Grid's Arrange method to make its children arrange themselves. Second, the code calls the PrintDialog's PrintVisual method to print the Grid.