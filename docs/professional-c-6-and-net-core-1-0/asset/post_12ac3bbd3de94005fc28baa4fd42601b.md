
Adding the ScaleTransform element to the RenderTransform property of the Rectangle element, as shown here, resizes the content of the complete rectangle by 0.5 in the x axis and 0.4 in the y axis (code file Transformation [WPF | UWP] / Main [Window | Page] .xaml):

```
<Rectangle Width="120" Height="60" Fill="Red" Margin="20">
    <Rectangle.RenderTransform>
        <ScaleTransform ScaleX="0.5" ScaleY="0.4" />
    </Rectangle.RenderTransform>
</Rectangle>
```

You can do more than transform simple shapes like rectangles; you can transform any XAML element as XAML defines vector graphics. In the following code, the Canvas element with the face shown earlier is put into a user control named SmilingFace, and this user control is shown first without transformation and then resized. You can see the result in Figure 30.7.

![](img/3d365b72b289213a91ade7eb366b8f35_1100_0.png)

## Figure 30.7

```
<local:SmilingFace />
<local:SmilingFace>
    <local:SmilingFace.RenderTransform>
        <ScaleTransform ScaleX="1.6" ScaleY="0.8" CenterY="180" />
    </local:SmilingFace.RenderTransform>
</local:SmilingFace>
```

## Translating

For moving an element in x or y direction, you can use TranslateTransform. In the following snippet, the element moves to the left by assigning -90 to x, and in the direction to the bottom by assigning 20 to y (code file Transformation [WPF | UWP] / Main [Window | Page] .xaml):

```
<Rectangle Width="120" Height="60" Fill="Green" Margin="20">
    <Rectangle.RenderTransform>
        <TranslateTransform X="-90" Y="20" />
    </Rectangle.RenderTransform>
</Rectangle>
```

## Rotating

You can rotate an element by using RotateTransform. With RotateTransform, you set the angle of the rotation and the center of the rotation with CenterX and CenterY (code file Transformation[WPF|UWP]/Main[Window|Page].xaml):

```
<Rectangle Width="120" Height="60" Fill="Orange" Margin="20">
    <Rectangle.RenderTransform>
        <RotateTransform Angle="45" CenterX="10" CenterY="-80" />
    </Rectangle.RenderTransform>
</Rectangle>
```

## Skewing

For skewing, you can use the SkewTransform element. With skewing you can assign angles for the x and y axes (code file Transformation[WPF|UWP]/Main[Window|Page].xaml):

```
<Rectangle Width="120" Height="60" Fill="LightBlue" Margin="20">
    <Rectangle.RenderTransform>
        <SkewTransform AngleX="20" AngleY="30" CenterX="40" CenterY="390" />
    </Rectangle.RenderTransform>
</Rectangle>
```

## Transforming with Groups and Composite Transforms

An easy way to do multiple transformations at once is by using the CompositeTransform (with UWP apps) and TransformationGroup elements. The TransformationGroup element can have SkewTransform, RotateTransform, TranslateTransform, and ScaleTransform as its children (code file Transformation[WPF|UWP]/Main[Window|Page].xaml):

```
<Rectangle Width="120" Height="60" Fill="LightGreen" Margin="20">
    <Rectangle.RenderTransform>
        <TransformGroup>
            <SkewTransform AngleX="45" AngleY="20" CenterX="-390" CenterY="40" />
            <RotateTransform Angle="90" />
            <ScaleTransform ScaleX="0.5" ScaleY="1.2" />
        </TransformGroup>
    </Rectangle.RenderTransform>
</Rectangle>
```

To rotate and skew together, it is possible to define a TransformGroup that contains both RotateTransform and SkewTransform. The class CompositeTransform defines properties to do multiple transformations at once—for example, ScaleX and ScaleY for scaling as well as TranslateX and TranslateY for moving an element. You can also define a MatrixTransform whereby the Matrix element specifies the properties M11 and M22 for stretching and M12 and M21 for skewing, as shown in the next section.

## Transforming Using a Matrix

Another option for defining multiple transformations at once is to specify a matrix. Here, you use MatrixTransform. MatrixTransform defines a Matrix property that has six values. Setting the values 1, 0, 0, 1, 0, 0 doesn’t change the element. With the values 0.5, 1.4, 0.4, 0.5, −200, and 0, the element is resized, skewed, and translated (code file Transformation[WPF|UWP]/Main[Window|Page].xaml):

```
<Rectangle Width="120" Height="60" Fill="Gold" Margin="20">
    <Rectangle.RenderTransform>
        <MatrixTransform Matrix="0.5, 1.4, 0.4, 0.5, -200, 0" />
    </Rectangle.RenderTransform>
</Rectangle>
```

The Matrix type is a struct and thus cannot be instantiated within XAML code in a UWP app. However, the previous sample puts all the value of the matrix into a string, which gets converted. With WPF, you can instantiate a struct within XAML code, and thus it is possible to define the same values by assigning the Matrix properties by its name. The properties M11 and M22 are used for scaling, M12 and M21 for skewing, and OffsetX and OffsetY for translating:

```
<Rectangle Width="120" Height="60" Fill="Gold" Margin="20">
    <Rectangle.RenderTransform>
        <MatrixTransform>
            <MatrixTransform.Matrix>
                <Matrix M11="0.5" M12="1.4" M21="0.4" M22="0.5" OffsetX="-200" OffsetY="0" />
            </MatrixTransform.Matrix>
        </MatrixTransform>
    </Rectangle.RenderTransform>
</Rectangle>
```

Directly assigning the values in a string to the Matrix property of the MatrixTransform class has this order: M11—M12—M21—M22—OffsetX—OffsetY.

## Transforming Layouts

The transformation samples have used RenderTransform. WPF also supports LayoutTransform. With RenderTransform, the transformation takes place after the layout phase is done, so it’s not taking into account when elements have a need for different sizes after the transformation. With LayoutTransform, the transformation happens before the layout phase—which is best demonstrated with an example. In the following code snippet, two rectangles are defined within a StackPanel. Both have the same height and width defined, but the first one is resized by a factor of 1.5 using render transformation. Looking at Figure 30.8 you can see that the rectangles overlay each other. The layout phase was done before the transformation, and thus the first rectangle doesn’t have enough room and just moves outside its positions for display (code file TransformationWPF/MainWindow.xaml):

![](img/3d365b72b289213a91ade7eb366b8f35_1102_0.png)

Figure 30.8

```
```xml
<StackPanel Orientation="Horizontal">
    <Rectangle Width="120" Height="60" Fill="Blue" Margin="20">
        <Rectangle.RenderTransform>
            <ScaleTransform ScaleX="1.5" ScaleY="1.5" />
        </Rectangle.RenderTransform>
    </Rectangle>
    <Rectangle Width="120" Height="60" Fill="Blue" Margin="20" />
</StackPanel>
```
```

By using the same rectangles and ScaleTransform but now with LayoutTransform (which is supported with WPF), you can see in Figure 30.9 that more room is made. The layout phase is done after the transformation.

![](img/3d365b72b289213a91ade7eb366b8f35_1103_0.png)

**Figure 30.9**

```
```xml
<StackPanel Orientation="Horizontal">
    <Rectangle Width="120" Height="60" Fill="Blue" Margin="20">
        <Rectangle.LayoutTransform>
            <ScaleTransform ScaleX="1.5" ScaleY="1.5" />
        </Rectangle.LayoutTransform>
    </Rectangle>
    <Rectangle Width="120" Height="60" Fill="Blue" Margin="20" />
</StackPanel>
```
```

> > **NOTE** *In addition to* `LayoutTransform` *there’s also a* `RenderTransform`. `LayoutTransform` *happens before the layout phase and* `RenderTransform` *happens after.*

## Brushes

This section demonstrates how to use XAML’s brushes for drawing backgrounds and foregrounds. When you use brushes, WPF has a lot more to offer than UWP apps. Consequently, this section starts by covering brushes that are offered by both technologies and then it gets into brushes that are available only with specific XAML technologies.

The first examples in this section reference Figure 30.10, which shows the effects of using various brushes within the `Background` of `Button` elements.
