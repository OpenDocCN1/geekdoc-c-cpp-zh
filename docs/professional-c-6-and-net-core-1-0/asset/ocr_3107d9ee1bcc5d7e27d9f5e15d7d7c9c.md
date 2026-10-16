Adding the ScaleTransform element to the RenderTransform property of the Rectangle element, as shown here, resizes the content of the complete rectangle by 0.5 in the x axis and 0.4 in the y axis (code file Transformation [WPF | UWP] / Main [Window | Page] .xaml):

```
<Rectangle Width="120" Height="60" Fill="Red" Margin="20">
    <Rectangle.RenderTransform>
        <ScaleTransform ScaleX="0.5" ScaleY="0.4" />
    </Rectangle.RenderTransform>
</Rectangle>
```

You can do more than transform simple shapes like rectangles; you can transform any XAML element as XAML defines vector graphics. In the following code, the Canvas element with the face shown earlier is put into a user control named SmilingFace, and this user control is shown first without transformation and then resized. You can see the result in Figure 30.7.

![](bbox=[0.105, 0.34, 0.89, 0.51])

# Figure 30.7

```
<local:SmilingFace />
<local:SmilingFace>
    <local:SmilingFace.RenderTransform>
        <ScaleTransform ScaleX="1.6" ScaleY="0.8" CenterY="180" />
    </local:SmilingFace.RenderTransform>
</local:SmilingFace>
```

# Translating

For moving an element in x or y direction, you can use TranslateTransform. In the following snippet, the element moves to the left by assigning -90 to x, and in the direction to the bottom by assigning 20 to y (code file Transformation [WPF | UWP] / Main [Window | Page] .xaml):

```
<Rectangle Width="120" Height="60" Fill="Green" Margin="20">
    <Rectangle.RenderTransform>
        <TranslateTransform X="-90" Y="20" />
    </Rectangle.RenderTransform>
</Rectangle>
```

# Rotating

You can rotate an element by using RotateTransform. With RotateTransform, you set the angle of the rotation and the center of the