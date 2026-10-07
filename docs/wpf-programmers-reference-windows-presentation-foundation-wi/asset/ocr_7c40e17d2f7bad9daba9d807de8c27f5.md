The UseRectangle example program shown in Figure 8-7 uses the following XAML code to draw two Rectangles:

```
<Rectangle Width="Auto" Height="Auto" Margin="10"
  Stroke="Red" StrokeThickness="10"
  StrokeDashArray="3,3" StrokeCap="Round"/>
```

```
<Rectangle Width="100" Height="50"
  Stroke="Blue" StrokeThickness="5" Fill="Cyan"
  HorizontalAlignment="Center" VerticalAlignment="Center/>
```

In the first Rectangle, the Width and Height are set to Auto, the control's Margin property determines the control's size and location. Because the Margin is 10 in this example, the Rectangle is positioned so its edges are 10 pixels from the edges of the Grid that contains.

In the second Rectangle, the Width and Height are explicitly set. Since the control's HorizontalAlignment and VerticalAlignment properties are both set to Center, the control is given its specified size and centered in its container.

![](bbox=[0.675, 0.305, 0.855, 0.415])

FIGURE 8-7

# SUMMARY

This chapter describes WPF's 2D drawing controls. These controls let you draw ellipses, lines, rectangles, and other 2D shapes. Although these controls draw very different shapes, they have much in common such as their Stroke and Fill properties.

Most of these controls are relatively simple, although the Path control with its specialized language can be complex. It's so complex, in fact, that you will probably only use it for relatively simple shapes. For complex shapes you want to use program code to generate the Path's drawing commands.

This chapter finishes the description of WPF controls. The controls described in Chapters 5 through 8 should meet most of your everyday programming needs.

The chapters that follow turn away from specific controls and discuss more general issues. Chapter 9, "Properties," explains in general terms how XAML code can set control properties. Since the examples so far in this book have used properties extensively, you probably already know how to set values for simple properties. Chapter 9 provides more background and explains how to set properties that take values that are objects themselves.