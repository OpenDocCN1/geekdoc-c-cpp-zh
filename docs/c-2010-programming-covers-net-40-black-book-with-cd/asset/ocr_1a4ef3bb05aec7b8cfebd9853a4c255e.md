![](bbox=[0.24, 0.08, 0.71, 0.34])

# Figure 10.2: Showing the UniformGrid Control

> NOTE
> In WPF, whenever you add a control from the Toolbox to the WPF designer, a corresponding XAML code is automatically generated for the control.

# The Canvas Control

The Canvas control is the simplest container control that supports absolute positioning of its child controls by using the coordinates that are relative to the Canvas control. When you place a control in the Canvas control, you must specify one horizontal property and one vertical property to specify the starting position of the child control inside the Canvas control. This control is the only container control that has no built-in layout of its own. By default, the Height and Width properties of the Canvas control are set to zero.

To position a child control on the Canvas control, you need to set its Canvas.Top, Canvas.Left Canvas.Right, or Canvas.Bottom property.

The Canvas control is represented by the Canvas class, which is derived from the Panel class. The inheritance hierarchy of the Canvas class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Panel
              System.Windows.Controls.Canvas
```

You can add a Canvas control to a WPF application by using the following code snippet:

```
<Canvas>
  <!--child elements-->
</Canvas>
```

Table 10.4 describes the noteworthy attached properties of the Canvas class:

Table 10.4: Showing the Noteworthy Attached Properties of the Canvas Class

| Property | Description |
|---|---|
| Bottom | Gets or sets a value that represents the distance between the bottom of a control and the bottom of its parent Canvas control |
| Left | Gets or sets a value that represents the distance between the left side of a control and the left side of its parent Canvas control |
| Right | Gets or sets a value that represents the distance between the right side of a control and the right side of its parent Canvas control |