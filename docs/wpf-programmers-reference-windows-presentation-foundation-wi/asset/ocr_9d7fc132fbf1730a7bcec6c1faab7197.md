# 308 | CHAPTER 17 PRINTING

```
} else
{
    // Resize to fit the margin.
    view_box.Margin = margin.Value;
    view_box.Stretch = Stretch.Uniform;
}

// Make a VisualBrush hold an image of the Window's contents.
    VisualBrush vis_br = new VisualBrush(win);

// Make a rectangle the size of the Window.
    Rectangle win_rect = new Rectangle();
    view_box.Child = win_rect;
    win_rect.Width = min.Width;
    win_rect.Height = min.Height;
    win_rect.Fill = vis_br;
    win_rect.Stroke = Brushes.Black;
    win_rect.BitmapEffect = new DropShadowBitmapEffect();

// Arrange to produce output.
    Rect = new Rect(0, 0,
    pd.PrintableAreaWidth, pd.PrintableAreaHeight);
    drawing_area.Arrange(rect);

// Print it.
    pd.PrintVisual(drawing_area, title);
```

The function uses Grid, Viewbox, and Rectangle controls to display a window centered on the printed page. It takes four parameters:

+   - The PrintDialog to use. This object holds information about the printer that the user selected.
- The window to print
- A title for the print job
- A Thickness value to use as a margin around the printed window. The question mark in the parameter's declaration means it is a nullable type, so the program can pass the value null for this parameter. If value is null, the routine prints the window at its normal size centered on the printout. If this is not null, the routine enlarges the window as much as possible while still allowing this margin around it.

The code starts by creating a Grid control. It uses the PrintDialog's PrintableAreaWidth and PrintableAreaHeight properties to see how big the printer's page is, and it makes the Grid fill the page.