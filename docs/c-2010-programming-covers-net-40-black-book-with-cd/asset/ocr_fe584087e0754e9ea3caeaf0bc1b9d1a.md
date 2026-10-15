The GridSplitter control is provided by the GridSplitter class, which exists in the System.Windows.Controls.dll assembly in the System.Windows.Controls namespace. The class hierarchy of the GridSplitter class is:

```
System.Object
  System.Windows.DependencyObject
    System.Windows.UIElement
      System.Windows.FrameworkElement
        System.Windows.Controls.Control
          System.Windows.Controls.GridSplitter
```

The GridSplitter class has various properties that you can use to work with the GridSplitter control. Table 17.7 lists the noteworthy properties of the GridSplitter class:

| Table 17.7: Noteworthy Properties of the GridSplitter Class |
| Property | Description |
| IsEnabled | Allows you to specify whether the GridSplitter control is enabled or disabled in the Silverlight application |
| PreviewStyle | Sets or retrieves the style used for previewing the changes in rows and columns |
| ShowsPreview | Allows you to specify whether to display preview in the GridSplitter control |

Note that the GridSplitter class primarily uses the attached properties of the Grid control to specify the rows and columns that are movable. For example, you can use the Grid.Row, Grid.RowSpan, Grid.Column, and Grid.ColumnSpan attached properties with the GridSplitter control. The direction in which the GridSplitter control adjusts the rows and columns is determined by the HorizontalAlignment and/or VerticalAlignment properties of the GridSplitter.

# The HyperlinkButton Control

The HyperlinkButton control is a button containing a hyperlink. The HyperlinkButton control combines the features of a hyperlink as well as a button. When you click the HyperlinkButton control, you are redirected to a Web page either in the current Web application or a different Web application. You can specify the name of a particular window or frame where you can redirect users. Figure 17.12 shows a HyperlinkButton control:

![](bbox=[0.35, 0.62, 0.65, 0.71])

Figure 17.12: A HyperlinkButton Control in Silverlight 3.0

The HyperlinkButton control is an instance of the HyperlinkButton class, which exists in the System.Windows.Controls.dll assembly in the System.Windows.Controls namespace. The class hierarchy of the HyperlinkButton class is:

```
System.Object
  System.Windows.DependencyObject
    System.Windows.UIElement
      System.Windows.FrameworkElement
        System.Windows.Controls.Control
          System.Windows.Controls.ContentControl
            System.Windows.Controls.Primitives.ButtonBase
              System.Windows.Controls.HyperlinkButton
```

The HyperlinkButton class has some properties that you can use to work with the HyperlinkButton control. Table 17.8 lists the noteworthy properties of the HyperlinkButton class: