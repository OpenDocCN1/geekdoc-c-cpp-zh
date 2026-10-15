named AnimatingCamera (also available in CD) and add the code, given in Listing 12.39, to the MainWindow.xaml file:

# Listing 12.39: Using the Point3DAnimation and Vector3DAnimation Classes

```
<Window x:Class="AnimatingCamera.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
<DockPanel>
<Canvas Width="321" Height="201">
<Viewport3D Name="MyAnimatedobject" Width="150" Height="150">
<Viewport3D.Camera>
<PerspectiveCamera x:Name="myCamera" Position="0,0,1" LookDirection="0,0,-1" FieldOfView="100" />
</Viewport3D.Camera>
<Viewport3D.Children>
<ModelVisual3D>
<ModelVisual3D.Content>
<DirectionalLight Color="white" Direction="-0.612372,-0.5,-0.612372" />
</ModelVisual3D.Content>
</ModelVisual3D>
<ModelVisual3D>
<ModelVisual3D.Content>
<DirectionalLight Color="white" Direction="0.612372,-0.5,-0.612372" />
</ModelVisual3D.Content>
</ModelVisual3D>
<ModelVisual3D>
<ModelVisual3D.Content>
<GeometryModel3D>
<GeometryModel3D.Geometry>
<MeshGeometry3D TriangleIndices="0,1,2 3,4,5 " Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1" TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0" Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5" />
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<MaterialGroup>
<DiffuseMaterial>
<DiffuseMaterial.Brush>
<RadialGradientBrush>
<RadialGradientBrush.GradientStops>
<GradientStop Color="Yellow" Offset="0.5" />
<GradientStop Color="Red" Offset="1" />
</RadialGradientBrush.GradientStops>
</RadialGradientBrush>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</MaterialGroup>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<RotateTransform3D x:Name="myRotateTransform3D">
<RotateTransform3D.Rotation>
<AxisAngleRotation3D Axis="0,3,0" Angle="40" />
</RotateTransform3D.Rotation>
</RotateTransform3D>
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