

## 清单 12.37：使用 KeyTime 属性

```
<Window x:Class="ControllingTiming.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="200" Width="400">
<Grid>
<Rectangle Margin="17,14,0,0" Stroke="Black" Height="116" VerticalAlignment="Top" Fill="Orange" HorizontalAlignment="Left" Width="125">
<Rectangle.RenderTransform>
<TranslateTransform x:Name="RectangleTransform1" X="0" Y="0"/>
</Rectangle.RenderTransform>
<Rectangle.Triggers>
<EventTrigger RoutedEvent="Rectangle.Loaded">
<BeginStoryboard>
<Storyboard>
<DoubleAnimationUsingKeyFrames
Storyboard.TargetName="RectangleTransform1"
Storyboard.TargetProperty="X" Duration="0:0:10"
RepeatBehavior="Forever">
<LinearDoubleKeyFrame Value="350" KeyTime="0:0:10"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Rectangle.Triggers>
</Rectangle>
<Rectangle Height="54" Margin="17,15,0,0" Stroke="Black" VerticalAlignment="Top" HorizontalAlignment="Left" Width="62" Fill="Red">
<Rectangle.RenderTransform>
<TranslateTransform x:Name="RectangleTransform2" X="0" Y="0"/>
</Rectangle.RenderTransform>
<Rectangle.Triggers>
<EventTrigger RoutedEvent="Rectangle.Loaded">
<BeginStoryboard>
<Storyboard>
<DoubleAnimationUsingKeyFrames
Storyboard.TargetName="RectangleTransform2"
Storyboard.TargetProperty="X" Duration="0:0:10"
RepeatBehavior="Forever">
<LinearDoubleKeyFrame Value="350" KeyTime="100%"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Rectangle.Triggers>
</Rectangle>
<Rectangle Margin="79,68,0,0" Stroke="Black" Height="62" VerticalAlignment="Top" Fill="OrangeRed" HorizontalAlignment="Left" Width="63">
<Rectangle.RenderTransform>
<TranslateTransform x:Name="RectangleTransform3" X="0" Y="0"/>
</Rectangle.RenderTransform>
<Rectangle.Triggers>
<EventTrigger RoutedEvent="Rectangle.Loaded">
<BeginStoryboard>
<Storyboard>
<DoubleAnimationUsingKeyFrames
Storyboard.TargetName="RectangleTransform3"
Storyboard.TargetProperty="X" Duration="0:0:10"
RepeatBehavior="Forever">
<LinearDoubleKeyFrame Value="350" KeyTime="Uniform"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Rectangle.Triggers>
</Rectangle>
<Rectangle Height="30" Margin="57,53,0,0" Stroke="Black" VerticalAlignment="Top" HorizontalAlignment="Left" Width="42" Fill="Orange">
<Rectangle.RenderTransform>
<TranslateTransform x:Name="RectangleTransform4" X="0" Y="0"/>
</Rectangle.RenderTransform>
<Rectangle.Triggers>
<EventTrigger RoutedEvent="Rectangle.Loaded">
<BeginStoryboard>
<Storyboard>
<DoubleAnimationUsingKeyFrames Storyboard.TargetName="RectangleTransform4" Storyboard.TargetProperty="X" Duration="0:0:10" RepeatBehavior="Forever">
<LinearDoubleKeyFrame Value="350" KeyTime="Paced"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Rectangle.Triggers>
</Rectangle>
</Grid>
</Window>
```

在清单 12.37 中，向窗口添加了四个矩形，窗口加载后它们开始移动。当您按键盘上的 F5 键运行应用程序时，可以看到这些矩形以相同的速度一起移动。这是因为 KeyTime 属性使矩形能够以相同的速度移动。代码输出如图 12.39 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_626_0.png)

图 12.39：控制关键帧的时间

## 几何图形动画

WPF 中有不同类型的几何图形，例如简单几何图形、路径几何图形和复合几何图形。您可以对不同类型的几何图形应用动画，以在 WPF 中创建具有视觉吸引力的应用程序。让我们创建一个具有动画几何图形的应用程序。为此，创建一个名为 AnimatingGeometry 的 WPF 应用程序（也可在 CD 中找到），并将清单 12.38 中给出的代码添加到 MainWindow.xaml 文件中：

## 清单 12.38：为几何图形使用动画

```
<Window x:Class="AnimatingGeometry.MainWindow" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
Title="MainWindow" Height="300" Width="300">
<Canvas>
    <Path Fill="Pink" Stroke="Black" StrokeThickness="5">
        <Path.Data>
            <EllipseGeometry x:Name="MyGeometry" Center="200,200" RadiusX="25" RadiusY="50" />
        </Path.Data>
        <Path.Triggers>
            <EventTrigger RoutedEvent="Path.Loaded">
                <BeginStoryboard>
                    <Storyboard>
                        <PointAnimation Storyboard.TargetName="MyGeometry" Storyboard.TargetProperty="Center" From="200,200" To="50,50" Duration="0:0:2" AutoReverse="true" RepeatBehavior="Forever"/>
                    </Storyboard>
                </BeginStoryboard>
            </EventTrigger>
        </Path.Triggers>
    </Path>
</Canvas>
</Window>
```

在清单 12.38 中，使用 EllipseGeometry 类在应用程序中添加了一个椭圆形状，该形状通过动画移动。当您按键盘上的 F5 键运行应用程序时，椭圆形状从 From 属性中指定的点开始移动到 To 属性中指定的点。移动速度由 Duration 属性确定。输出如图 12.40 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_627_0.png)

## 将动画与 3-D 模型一起使用

到目前为止的主题涉及 2-D 模型中的动画。您也可以将动画应用于 WPF 中的 3-D 模型。在 WPF 中为 3-D 模型制作动画可使您的 3-D 应用程序具有丰富的外观。您可以对 3-D 模型应用不同的动画。制作 3-D 模型动画的一种方法是动画化相机。您还可以使用 Rotation3DAnimation 类来为 3-D 模型制作动画。Rotation3DAnimation 类对 3-D 模型应用旋转效果。

### 动画化相机

在 WPF 中，您可以使用 Point3DAnimation 和 Vector3DAnimation 类来动画化 PerspectiveCamera 类的 Position 和 LookDirection 属性。Point3DAnimation 类使用起始值和结束值之间的线性插值来动画化 Point3D 属性的值。Vector3DAnimation 类动画化 Vector3D 属性的值。让我们创建一个动画化 3-D 模型相机的应用程序。为此，创建一个名为 AnimatingCamera 的 WPF 应用程序（也可在 CD 中找到），并将清单 12.39 中给出的代码添加到 MainWindow.xaml 文件中：

## 清单 12.39：使用 Point3DAnimation 和 Vector3DAnimation 类

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

