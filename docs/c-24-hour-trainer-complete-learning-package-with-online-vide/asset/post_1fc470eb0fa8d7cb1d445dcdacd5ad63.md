
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

Figure 30-4 shows a preview of the result. To make this figure, I printed the Window into an XML Paper Specification (XPS) file by selecting the Microsoft XPS Document Writer from the PrintDialog. I then double-clicked the XPS file to display it in the XPS Viewer shown in Figure 30-4. You can see in the figure that the Window's image is centered.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_468_0.png)

FIGURE 30-4

In Figure 30-4 the image of the window looks a bit grainy and pixelated, but that's caused by the way the XPS Viewer displays the document. The document itself was generated at a very high resolution. In Figure 30-5 the viewer has enlarged the document by 265 percent, so you can see that the result is actually very smooth and the final printout can take advantage of the printer's relatively high resolution.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_468_1.png)

FIGURE 30-5

The Print Window Enlarged example program is similar to the Print Window Centered program except it uses the following code to pass a Thickness object to the PrintWindowCentered method to use as a margin. That makes the method stretch the Window's image to fill the printable area minus a 50-pixel margin.

```csharp
// Print an image of the window centered and stretched to fill the page.
private void printButton_Click(object sender, RoutedEventArgs e)
{
    PrintDialog printDialog = new PrintDialog();
    if (printDialog.ShowDialog() == true)
    {
        PrintWindowCentered(printDialog, this, "New Customer",
            new Thickness(50));
    }
}
```

Figure 30-6 shows the result. Notice that the Window's image is centered and enlarged to fill most of the printable area.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_469_0.png)

## FIGURE 30-6

In addition to the PrintVisual method, the PrintDialog class provides a PrintDocument method that prints multipage output or document objects such as FlowDocuments or FixedDocuments. Unfortunately these topics are fairly complex, so they're not described here. If you need those capabilities, you can find more information online at:

- PrintDocument—msdn.microsoft.com/library/system.windows.controls.printdialog.printdocument.aspx
- FixedDocument—msdn.microsoft.com/library/system.windows.documents.fixeddocument.aspx
- FlowDocument—msdn.microsoft.com/library/system.windows.documents.flowdocument.aspx

## TRY IT

In this Try It, you build a program that prints and displays a preview of the table shown in Figure 30-7. You build an array of student objects and then loop through them, displaying their values as shown in the figure.

![](img/d5be6ade75773ca6cec5c78f96a98bb1_470_0.png)

| Name | Test 1 | Test 2 | Test 3 | Test 4 |
|---|---|---|---|---|
| Ann Archer | 91 | 92 | 93 | 94 |
| Bob Blarth | 81 | 82 | 83 | 84 |
| Cyd Carter | 71 | 72 | 73 | 74 |
| Dan Deever | 61 | 62 | 63 | 64 |

FIGURE 30-7

## Lesson Requirements

In this lesson, you:

- Start a new Windows Forms project and create the program's main form. Add PrintDocument and PrintPreviewDialog components to do the printing and previewing.
- Add Print and Preview buttons with appropriate event handlers.
- Add a Student class with FirstName and LastName properties. Also give it a TestScores property that is an array of integers
- Create the PrintPage event handler.
  - Create an array of Student objects. Initialize them using array and object initializers.
  - Loop through the Student objects, printing them.
  - Draw a rectangle around the table.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

## Hints

- Don't forget to set the PrintPreviewDialog's Document property, to the PrintDocument component.
- This example doesn't do anything fancy with Student properties, so they can be auto-implemented.

```
TestScores=new int[] {81, 82, 83, 84}),
new Student() {FirstName="Cyd", LastName="Carter",
TestScores=new int[] {71, 72, 73, 74}},
new Student() {FirstName="Dan", LastName="Deever",
TestScores=new int[] {61, 62, 63, 64}};
};

// Set the coordinates for the first row and the columns.
int y = e.MarginBounds.Top;
int x0 = e.MarginBounds.Left;
int x1 = x0 + 200;
int x2 = x1 + 100;
int x3 = x2 + 100;
int x4 = x3 + 100;

// Make a font to use.
using (Font font = new Font("Times New Roman", 20))
{
    // Draw column headers.
    e.Graphics.DrawString("Name", font, Brushes.Black, x0, y);
    e.Graphics.DrawString("Test 1", font, Brushes.Black, x1, y);
    e.Graphics.DrawString("Test 2", font, Brushes.Black, x2, y);
    e.Graphics.DrawString("Test 3", font, Brushes.Black, x3, y);
    e.Graphics.DrawString("Test 4", font, Brushes.Black, x4, y);
    // Move Y down for the first row.
    y += 30;

    // Loop through the Students displaying their data.
    foreach (Student student in students)
    {
        // Display the Student's values.
        e.Graphics.DrawString(student.FirstName + " " +
        student.LastName, font, Brushes.Black, x0, y);
        e.Graphics.DrawString(student.TestScores[0].ToString(),
        font, Brushes.Black, x1, y);
        e.Graphics.DrawString(student.TestScores[1].ToString(),
        font, Brushes.Black, x2, y);
        e.Graphics.DrawString(student.TestScores[2].ToString(),
        font, Brushes.Black, x3, y);
        e.Graphics.DrawString(student.TestScores[3].ToString(),
        font, Brushes.Black, x4, y);

        // Move Y down for the next row.
        y += 30;
    }
}

// Draw a box around it all.
e.Graphics.DrawRectangle(Pens.Black,
    x0, e.MarginBounds.Top,
    x4 - x0 + 100,
    y - e.MarginBounds.Top);

// We're only printing one page.
e.HasMorePages = false;
}
```
