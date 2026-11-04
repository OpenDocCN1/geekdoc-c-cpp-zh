```
```csharp
    )

    // Make a VisualBrush holding an image of the Window's contents.
    VisualBrush vis_br = new VisualBrush(win);

    // Make a rectangle the size of the Window.
    Rectangle win_rect = new Rectangle();
    view_box.Child = win_rect;
    win_rect.Width = win.Width;
    win_rect.Height = win.Height;
    win_rect.Fill = vis_br;
    win_rect.Stroke = Brushes.Black;
    win_rect.BitmapEffect = new DropShadowBitmapEffect();

    // Arrange to produce output.
    Rect rect = new Rect(0, 0,
        pd.PrintableAreaWidth, pd.PrintableAreaHeight);
    drawing_area.Arrange(rect);

    // Print it.
    pd.PrintVisual(drawing_area, title);
}
```
```

# WPF Programmer's Reference 9780470477229 PrintWindow

The next figure shows the result when the program's window is stretched and printed using the Microsoft XPS Document Writer with preferences set to landscape orientation and displayed in XPS Viewer.

![](bbox=[0.24, 0.532, 0.62, 0.761])