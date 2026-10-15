
## Using Brushes

In the In Depth section of this chapter, you have learned about the types of brushes available in WPF. In this section, you learn about how you use the different brushes to give your WPF application a rich look. As you know, there are five types of brushes available in WPF, such as LinearGradientBrush, RadialGradientBrush, ImageBrush, DrawingBrush, and VisualBrush. You see further the usage of all the brushes in detail.

### LinearGradientBrush and RadialGradientBrush

The LinearGradientBrush class is used to paint an area with linear gradient; while the RadialGradientBrush class is used to paint an area with radial gradient. You use the GradientStop object to specify the colors in the gradient and their position.

Let's add the LinearGradientBrush and RadialGradientBrush classes to an application. To do this, create a WPF application named Linear_RadialBrush (also available in CD) and add the code, given in Listing 12.8, to the MainWindow.xaml file:

**Listing 12.8: Using the LinearGradientBrush and RadialGradientBrush Classes**

```
<Window x:Class="Linear_RadialBrush.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
<Grid>
<Ellipse Name="ellipse1" Stroke="OrangeRed" HorizontalAlignment="Right" Width="96" Height="96" VerticalAlignment="Top" Margin="0,8,19,0">
<Ellipse.Fill>
<LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5">
<GradientStop Color="OrangeRed" Offset="0.0"/>
<GradientStop Color="Orange" Offset="0.25"/>
<GradientStop Color="Yellow" Offset="0.75"/>
<GradientStop Color="MediumVioletRed" Offset="1"/>
</LinearGradientBrush>
</Ellipse.Fill>
</Ellipse>
<Rectangle Margin="9,103,0,17" Name="rectangle2" Stroke="Thistle" HorizontalAlignment="Left" Width="103" StrokeThickness="4">
<Rectangle.Fill>
<RadialGradientBrush GradientOrigin="1,1" Center="1,1" RadiusX="1" RadiusY="1">
<RadialGradientBrush.GradientStops>
<GradientStop Offset="0.09" Color="Yellow"/>
<GradientStop Offset="0.25" Color="Green"/>
<GradientStop Offset="0.5" Color="Red"/>
<GradientStop Offset="1.25" Color="Blue"/>
</RadialGradientBrush.GradientStops>
</RadialGradientBrush>
</Rectangle.Fill>
</Rectangle>
<Polygon Points="10,110 60,11 110,110" Stroke="IndianRed" StrokeThickness="4" Canvas.Left="150" Canvas.Top="150" Margin="0,-9,0,9" Fill="IndianRed"></Polygon>
</Grid>
</Window>
```

In Listing 12.8, the shapes are colored using the LinearGradientBrush and RadialGradientBrush classes. As you can see in the code, the colors in both the brushes are described using the GradientStop class. The difference is shown in the output of the brushes. When you run the application, by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.12:

![](img/e073a4882197be4ab61103cbe0bcb394_586_0.png)

**Figure 12.12:** Using the LinearGradientBrush and RadialGradientBrush Classes

### ImageBrush

The ImageBrush class paints an area with an image. The ImageSource property of the ImageBrush is used to paint the area. Let's add the ImageBrush class to an application. To do this, create a WPF application named ImageBrush (also available in CD) and add the code, given in Listing 12.9, to the MainWindow.xaml file:

**Listing 12.9: Using the ImageBrush Class**

```
<Window x:Class="ImageBrush.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300"
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="PresentationOptions">
    <Grid>
        <StackPanel>
            <Rectangle Width="100" Height="100" Stroke="Red" StrokeThickness="4">
                <Rectangle.Fill>
                    <ImageBrush Stretch="uniformToFill" ImageSource="D:\pictures\DE-wp3.jpg" PresentationOptions:Freeze="True" />
                </Rectangle.Fill>
            </Rectangle>
            <Rectangle Width="200" Height="100" Stroke="Black" StrokeThickness="2" Margin="50,50,20,20">
                <Rectangle.Fill>
                    <ImageBrush Stretch="Fill" ImageSource="D:\pictures\DE-wp3.jpg" PresentationOptions:Freeze="True" TileMode="Tile"/>
                </Rectangle.Fill>
            </Rectangle>
        </StackPanel>
    </Grid>
</Window>
```

> **NOTE:** You need to change the path of the file specified in the application.

In the preceding code, images are added to the application in different views and mode. When you run the application, by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.13:

![](img/e073a4882197be4ab61103cbe0bcb394_587_0.png)

**Figure 12.13:** Displaying the use of the ImageBrush Class

### DrawingBrush and VisualBrush

The DrawingBrush class paints an area with shapes, images, and text. The VisualBrush class paints an area with a visual which can include a Button, Page, or MediaElement. Let's add DrawingBrush and VisualBrush to the application. To do this, create a WPF application named Drawing_VisualBrush (also available in CD) and add the code, given in Listing 12.10, to the MainWindow.xaml file:

**Listing 12.10: Using the DrawingBrush and VisualBrush Classes**

```
<Window x:Class="Drawing_VisualBrush.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="525">
<Grid>
<Button Name="button1">
<Button.Background>
<DrawingBrush>
<DrawingBrush.Drawing>
<GeometryDrawing Brush="Firebrick">
<GeometryDrawing.Geometry>
<GeometryGroup>
<EllipseGeometry RadiusX="50" RadiusY="12"/>
<EllipseGeometry RadiusX="45" RadiusY="10"/>
<EllipseGeometry RadiusX="30" RadiusY="7"/>
<EllipseGeometry RadiusX="20" RadiusY="5"/>
</GeometryGroup>
</GeometryDrawing.Geometry>
</GeometryDrawing>
</DrawingBrush.Drawing>
</DrawingBrush>
</Button.Background>
</Button>
<Rectangle Margin="79,83,76,83" Name="rectangle1" Stroke="Gold">
<Rectangle.Fill>
<VisualBrush>
<VisualBrush.Visual>
<StackPanel Background="Antiquewhite">
<TextBlock FontSize="10pt" Margin="3">
Hello!!!!
</TextBlock>
</StackPanel>
</VisualBrush.Visual>
</VisualBrush>
</Rectangle.Fill>
</Rectangle>
</Grid>
</Window>
```

> **NOTE:** You can change the root element of the application to Page in a WPF application.

When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.14:

![](img/e073a4882197be4ab61103cbe0bcb394_588_0.png)

**Figure 12.14:** Using the DrawingBrush and VisualBrush Classes

Note that when you move the mouse over the shape, the image automatically changes.

### Changing the Tile Size and the Pattern of Brushes

You can use the TileMode property of the TileBrush class in WPF to create a pattern. The TileMode property enables you to specify how the content of the TileBrush object is repeated to fill the output area. You can set the TileMode property to Tile, FlipX, FlipY, or FlipXY. The TileMode property of the TileBrush class works identically for the ImageBrush, VisualBrush, and DrawingBrush classes also. You should also set the Viewport property of the TileBrush class to create the tiles. Let's create an application and change the tile size and pattern of the brush. To do this, create a WPF application named TileSize_Pattern_Brush (also available in CD) and add a page to the application. Now add the code, given in Listing 12.11, to the Page1.xaml file:

**Listing 12.11: Applying the TileMode Property**

```
<Page x:Class="TileSize_Pattern_Brush.Page1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"
mc:Ignorable="PresentationOptions"
Background="White" Margin="15">
    <Page.Resources>
        <GeometryDrawing x:Key="Tilesize" Geometry="M0,0 L50,0 0,50Z" Brush="Aquamarine" PresentationOptions:Freeze="True" >
            <GeometryDrawing.Pen>
                <Pen Thickness="2" Brush="PalevioletRed" MiterLimit="0" />
            </GeometryDrawing.Pen>
        </GeometryDrawing>
    </Page.Resources>
    <StackPanel HorizontalAlignment="Center">
        <Rectangle Height="96" Name="rectangle1" Stroke="Black" Width="222">
            <Rectangle.Fill>
                <DrawingBrush TileMode="None" Drawing="{StaticResource Tilesize}" />
```
