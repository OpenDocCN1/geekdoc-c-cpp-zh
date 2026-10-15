
在清单 12.19 中，`3-D` 模型根据 `TranslateTransform3D` 类的 `OffsetX`、`OffsetY` 和 `OffsetZ` 属性移动。当您按下键盘上的 `F5` 键运行应用程序时，您会得到输出，如图 12.23 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_603_0.png)

图 12.23：显示 `TranslateTransform3D` 应用程序的输出

## ScaleTransform3D

`ScaleTransform3D` 类用于相对于中心点按指定向量缩放 `3-D` 模型。您可以在 `ScaleX`、`ScaleY` 和 `ScaleZ` 属性中指定相同的值，以便 `3-D` 模型在 X、Y 和 Z 轴上按相同的值缩放。让我们创建一个可以应用 `ScaleTransform3D` 类的 `3-D` 模型。为此，创建一个名为 `ScaleTransform3D` 的 WPF 应用程序（也可在 CD 上获得）并将清单 12.20 中的代码添加到 `MainWindow.xaml` 文件中：

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

在清单 12.20 中，`3-D` 模型根据 `ScaleTransform3D` 类的 `ScaleX`、`ScaleY` 和 `ScaleZ` 属性调整大小。当您按下键盘上的 `F5` 键运行应用程序时，您会得到输出，如图 12.24 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_604_0.png)

图 12.24：显示 `ScaleTransform3D` 应用程序的输出

## RotateTransform3D

您可以使用 `RotateTransform3D` 类以不同方式旋转 `3-D` 模型。典型的旋转是指定旋转轴和绕轴的旋转角度。旋转使用 `Rotation` 属性定义。旋转的轴角度使用 `Axis` 和 `Angle` 属性定义。让我们创建一个可以应用 `RotateTransform3D` 类的 `3-D` 模型。为此，创建一个名为 `RotateTransform3D` 的 WPF 应用程序（也可在 CD 上获得）并将清单 12.21 中的代码添加到 `MainWindow.xaml` 文件中：

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

## 第12章：在 Windows Forms 和 WPF 中使用图形和多媒体

```xml
<PerspectiveCamera x:Name="myPerspectiveCamera" Position="0,0,2"
    LookDirection="0,0,-1" FieldOfView="60" />
</Viewport3D.Camera>
<Viewport3D.Children>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <DirectionalLight Color="White" Direction="-0.612372,-0.5,-
                0.612372" />
        </ModelVisual3D.Content>
    </ModelVisual3D>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <DirectionalLight Color="White" Direction="0.612372,-0.5,-
                0.612372" />
        </ModelVisual3D.Content>
    </ModelVisual3D>
    <ModelVisual3D>
        <ModelVisual3D.Content>
            <GeometryModel3D>
                <GeometryModel3D.Geometry>
                    <MeshGeometry3D TriangleIndices="0,1,2 3,4,5
Normals="0,0,1 0,0,1 0,0,1 0,0,1 0,0,1 0,0,1" TextureCoordinates="0,1 1,1 1,0 0,0"
Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5" />
                </GeometryModel3D.Geometry>
                <GeometryModel3D.Material>
                    <MaterialGroup>
                        <DiffuseMaterial>
                            <DiffuseMaterial.Brush>
                                <RadialGradientBrush>
                                    <RadialGradientBrush.GradientStops>
                                        <GradientStop Color="Yellow" Offset="0" />
                                        <GradientStop Color="Red" Offset="0.25" />
                                        <GradientStop Color="Blue" Offset="0.75" />
                                        <GradientStop Color="LimeGreen"
                                            Offset="1" />
                                    </RadialGradientBrush.GradientStops>
                                </RadialGradientBrush>
                            </DiffuseMaterial.Brush>
                        </DiffuseMaterial>
                    </MaterialGroup>
                </GeometryModel3D.Material>
                <GeometryModel3D.Transform>
                    <RotateTransform3D>
                        <RotateTransform3D.Rotation>
                            <AxisAngleRotation3D Axis="0,2,1" Angle="45" />
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

在清单 12.21 中，`3-D` 模型通过指定 `RotateTransform3D` 类的 `Axis` 和 `Angle` 属性进行旋转。当你通过在键盘上按下 `F5` 键运行应用程序时，你会得到输出，如图 12.25 所示。

![](img/e073a4882197be4ab61103cbe0bcb394_606_0.png)

图 12.25：显示 `RotateTransform3D` 应用程序的输出

### 在 WPF 4.0 中使用动画

WPF 中的动画包括不同类型的动画，这些动画由 `Timeline`、`Storyboard` 和 `EventTrigger` 类以及 `KeyFrames` 集合表示。动画可以使 UI 更具吸引力、更令人印象深刻且更有用。你可以将动画附加到 WPF 中的 `2-D` 和 `3-D` 图形。你可以创建普通形状并为其添加动画。你已在章节的深入部分学习过动画。现在让我们学习实际实现并在 WPF 中创建动画。

### 使用 Storyboards 创建动画

`Storyboards` 是在 WPF 中创建动画的有用工具。`Storyboard` 对象使你能够将影响多种对象的时序线组合成单个时序线树，并使你更容易组合和控制复杂的时间行为。你可以使用带有触发器的 `Storyboard` 时序线在 WPF 中创建动画。通常，`Storyboard` 类与 `EventTrigger` 类一起使用。然而，你也可以将它们与其他类型的触发器一起使用以在 WPF 中创建动画。

### 使用事件触发器

`EventTrigger` 类用于基于事件的发生启动一组操作。例如，操作可以是 `Button` 控件的点击，事件可以是 `Button` 控件点击时动画的开始点。让我们使用 `EventTrigger` 类创建一个动画。为此，创建一个名为 `EventTrigger` 的 WPF 应用程序（也在 CD 上提供）并将清单 12.22 中的代码添加到 `MainWindow.xaml` 文件中，该清单显示了如何在开始后控制 `Storyboard` 时序线：

清单 12.22：使用 EventTrigger 类

```
<Window x:Class="EventTrigger.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="318" Width="400">
<DockPanel>
    <Grid DockPanel.Dock="Top">
        <Canvas Background="CadetBlue">
            <Ellipse Canvas.Left="86" Canvas.Top="41" Height="90" Name="ellipse1"
                Stroke="Black" Width="96" Fill="AntiqueWhite" />
            <Ellipse Canvas.Left="105" Canvas.Top="62" Height="13" Name="ellipse2"
                Stroke="Black" Width="14" Fill="Cornsilk" />
            <Ellipse Canvas.Left="144" Canvas.Top="62" Height="13" Name="ellipse3"
                Stroke="Black" Width="14" Fill="Cornsilk" />
            <Ellipse Canvas.Left="112" Canvas.Top="68" Height="5" Name="ellipse4"
                Stroke="Black" Width="5" Fill="Black" />
            <Ellipse Canvas.Left="151" Canvas.Top="67" Height="5" Name="ellipse5"
                Stroke="Black" Width="5" Fill="Black" />
            <Rectangle Canvas.Left="105" Canvas.Top="129" Height="111"
                Name="rectangle1" Stroke="Black" Width="59" Fill="HotPink" />
            <Ellipse Canvas.Left="127" Canvas.Top="128" Height="10" Name="ellipse6"
Stroke="Black" Width="9" Fill="Blue" />
<Ellipse Canvas.Left="127" Canvas.Top="148" Height="10" Name="ellipse7"
```
