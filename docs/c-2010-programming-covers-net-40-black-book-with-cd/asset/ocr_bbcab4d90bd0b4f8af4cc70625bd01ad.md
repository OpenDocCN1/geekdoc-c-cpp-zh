```
<LinearGradientBrush.GradientStops>
<GradientStop Color="Yellow" offset="0.25" />
<GradientStop Color="Red" offset="0.75" />
</LinearGradientBrush.GradientStops>
</LinearGradientBrush>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</MaterialGroup>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<ScaleTransform3D ScaleX="1" ScaleY="1.5" ScaleZ="1.5" CenterX="1" CenterY="1" CenterZ="1" />
</GeometryModel3D.Transform>
</GeometryModel3D>
</ModelVisual3D.Content>
</ModelVisual3D>
</Viewport3D.Children>
</Viewport3D>
</Canvas>
</DockPanel>
</Window>
```

In Listing 12.20, the 3-D model is sized according to the ScaleX, ScaleY, and ScaleZ properties of the ScaleTransform3D class. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.24:

![](bbox=[0.33, 0.48, 0.58, 0.66])

Figure 12.24: Showing the Output of the ScaleTransform3D Application

# RotateTransform3D

You can rotate a 3-D model in different ways using the RotateTransform3D class. A typical rotation is the one in which you specify an axis and an angle of rotation around the axis. The rotation is defined using the Rotation property. The axis angle of the rotation is defined using the Axis and Angle properties. Let’s create a 3-D model on which you can apply the RotateTransform3D class. To do this, create a WPF application named RotateTransform3D (also available in CD) and add the code, given in Listing 12.21, to the MainWindow.xaml file:

# Listing 12.21: Applying the RotateTransform3D Class

```
<Window x:Class="RotateTransform3D.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<DockPanel>
<Canvas Width="250" Height="201">
<Viewport3D Width="200" Height="150" Canvas.Left="20" Canvas.Top="10">
<Viewport3D.Camera>
```