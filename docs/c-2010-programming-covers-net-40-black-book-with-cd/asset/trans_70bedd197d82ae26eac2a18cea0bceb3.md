

```
<MeshGeometry3D
TriangleIndices="0,1,2 3,4,5 "
Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 "
TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0 "
Positions="-0.5,-0.5,0.5 -0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5 "/>
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<MaterialGroup>
<DiffuseMaterial>
<DiffuseMaterial.Brush>
<SolidColorBrush Color="Bisque"/>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</MaterialGroup>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<RotateTransform3D>
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
<Viewport3D ClipToBounds="True" Width="100" Height="100" Canvas.Left="0" Canvas.Bottom="1">
<Viewport3D.Camera>
<PerspectiveCamera Position="0,0,2" LookDirection="0,0,-1" FieldOfView="40" />
</Viewport3D.Camera>
<Viewport3D.Children>
<ModelVisual3D>
<ModelVisual3D.Content>
<SpotLight Color="Yellow" InnerConeAngle="50" OuterConeAngle="25" Direction="0,0,-1" Position="1,1,6" Range="10"/>
</ModelVisual3D.Content>
</ModelVisual3D>
<ModelVisual3D>
<ModelVisual3D.Content>
<GeometryModel3D>
<GeometryModel3D.Geometry>
<MeshGeometry3D
TriangleIndices="0,1,2 3,4,5 "
Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 "
TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0 "
Positions="-0.5,-0.5,0.5 -0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5 "/>
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<MaterialGroup>
<DiffuseMaterial>
<DiffuseMaterial.Brush>
<LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
```
```
<LinearGradientBrush.GradientStops>
<GradientStop Color="Green" Offset="0" />
<GradientStop Color="SpringGreen" Offset="1" />
</LinearGradientBrush.GradientStops>
</LinearGradientBrush>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</MaterialGroup>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<RotateTransform3D>
<RotateTransform3D.Rotation>
<AxisAngleRotation3D Axis="0,3,0" Angle="30" />
</RotateTransform3D.Rotation>
</RotateTransform3D>
</GeometryModel3D.Transform>
</GeometryModel3D>
</ModelVisual3D.Content>
</ModelVisual3D>
</Viewport3D.Children>
</Viewport3D>
</Canvas>
</Page>

在清单 12.18 中，展示了四种光类型的用法。在运行代码之前，您必须将 App.xaml 文件中的 StartupUri 属性设置为 Page1.xaml。

当您按下键盘上的 F5 键运行应用程序时，您会得到输出，如图 12.22 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_601_0.png)

图 12.22：添加光照

## 转换 3-D 模型

您可以以与对 2-D 模型应用相同的方式对 3-D 模型应用转换。您可以应用于 3-D 模型的转换类型有：平移、缩放和旋转。这些转换是通过使用 TranslateTransform3D、ScaleTransform3D 和 RotateTransform3D 类实现的。转换允许您在不改变定义它们的基类的情况下调整 3-D 模型的大小和重新定向。在 WPF 应用程序中应用的 3-D 转换继承自 Transform3D 基类。

## TranslateTransform3D

TranslateTransform3D 类沿着您使用 OffsetX、OffsetY 和 OffsetZ 属性指定的偏移向量方向移动 3-D 模型的所有点。让我们创建一个可以应用 TranslateTransform3D 类的 3-D 模型。为此，创建一个名为 TranslateTransform3D 的 WPF 应用程序（也可在 CD 上获得）并将清单 12.19 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.19：应用 TranslateTransform3D 类

```
<Window x:Class="TranslateTransform3D.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<DockPanel>
<Canvas Width="300" Height="300">
<Viewport3D ClipToBounds="True" Width="200" Height="200">
<Viewport3D.Camera>
<PerspectiveCamera x:Name="myPerspectiveCamera" Position="0,0,2" LookDirection="0,0,-1" FieldOfView="60" />
</Viewport3D.Camera>
<Viewport3D.Children>
<ModelVisual3D>
<ModelVisual3D.Content>
<DirectionalLight Color="Pink" Direction="-0.612372,-0.5,-0.612372" />
</ModelVisual3D.Content>
</ModelVisual3D>
<ModelVisual3D>
<ModelVisual3D.Content>
<GeometryModel3D>
<GeometryModel3D.Geometry>
<MeshGeometry3D TriangleIndices="0,1,2 3,4,5" Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1" TextureCoordinates="0,0 1,0 1,1 1,1 0,1 0,0" Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5" />
</GeometryModel3D.Geometry>
<GeometryModel3D.Material>
<MaterialGroup>
<DiffuseMaterial>
<DiffuseMaterial.Brush>
<SolidColorBrush Color="LightYellow" Opacity="0.9"/>
</DiffuseMaterial.Brush>
</DiffuseMaterial>
</MaterialGroup>
</GeometryModel3D.Material>
<GeometryModel3D.Transform>
<TranslateTransform3D OffsetX="1" OffsetY="0" OffsetZ="0" />
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

在清单 12.19 中，3-D 模型根据 TranslateTransform3D 类的 OffsetX、OffsetY 和 OffsetZ 属性移动。当您按下键盘上的 F5 键运行应用程序时，您会得到输出，如图 12.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_603_0.png)

图 12.23：显示 TranslateTransform3D 应用程序的输出

## ScaleTransform3D

ScaleTransform3D 类用于相对于中心点按指定向量缩放 3-D 模型。您可以在 ScaleX、ScaleY 和 ScaleZ 属性中指定相同的值，以便 3-D 模型在 X、Y 和 Z 轴上按相同的值缩放。让我们创建一个可以应用 ScaleTransform3D 类的 3-D 模型。为此，创建一个名为 ScaleTransform3D 的 WPF 应用程序（也可在 CD 上获得）并将清单 12.20 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.20：应用 ScaleTransform3D 类

```
<Window x:Class="ScaleTransform3D.MainWindow" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" Title="MainWindow" Height="300" Width="300">
<DockPanel>
<Canvas Width="321" Height="201">
<Viewport3D Width="150" Height="150" Canvas.Left="0" Canvas.Top="10">
<Viewport3D.Camera>
<PerspectiveCamera Position="0,0,2" LookDirection="0,0,-1" FieldOfView="60" />
</Viewport3D.Camera>
<Viewport3D.Children>
<ModelVisual3D>
<ModelVisual3D.Content>
<DirectionalLight Color="White" Direction="-0.612372,-0.5,-0.612372" />
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
<LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5">
```
```
<LinearGradientBrush.GradientStops>
<GradientStop Color="Yellow" Offset="0.25" />
<GradientStop Color="Red" Offset="0.75" />
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

在清单 12.20 中，3-D 模型根据 ScaleTransform3D 类的 ScaleX、ScaleY 和 ScaleZ 属性调整大小。当您按下键盘上的 F5 键运行应用程序时，您会得到输出，如图 12.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_604_0.png)

图 12.24：显示 ScaleTransform3D 应用程序的输出

## RotateTransform3D

您可以使用 RotateTransform3D 类以不同方式旋转 3-D 模型。典型的旋转是指定旋转轴和绕轴的旋转角度。旋转使用 Rotation 属性定义。旋转的轴角度使用 Axis 和 Angle 属性定义。让我们创建一个可以应用 RotateTransform3D 类的 3-D 模型。为此，创建一个名为 RotateTransform3D 的 WPF 应用程序（也可在 CD 上获得）并将清单 12.21 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.21：应用 RotateTransform3D 类

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
