
</ModelVisual3D.Content>
</ModelVisual3D>
</Viewport3D.Children>
<Viewport3D.Triggers>
    <EventTrigger RoutedEvent="Viewport3D.Loaded">
        <BeginStoryboard>
            <Storyboard>
                <Point3DAnimation Storyboard.TargetName="myCamera" Storyboard.TargetProperty="Position" From="0,0,2" To="1,2,3" Duration="0:0:4" RepeatBehavior="Forever"/>
                <Vector3DAnimation Storyboard.TargetName="myCamera" Storyboard.TargetProperty="LookDirection" From="0,0,-1" To="-1,-2,-3" Duration="0:0:4" RepeatBehavior="Forever"/>
            </Storyboard>
        </BeginStoryboard>
    </EventTrigger>
</Viewport3D.Triggers>
</Viewport3D>
</Canvas>
</DockPanel>
</Window>

在清单 12.39 中，3D 模型被添加到应用程序中。当你按下键盘上的 F5 键运行应用程序时，你可以看到 3D 模型在移动。动画使摄像机围绕物体移动。物体本身并未改变位置或旋转。正是移动的摄像机使其看起来如此。随着摄像机位置使用 Point3DAnimation 类发生变化，摄像机指向的方向使用 Vector3DAnimation 类保持物体在摄像机的视野内。当你按下键盘上的 F5 键运行应用程序时，你会得到如图 12.41 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_629_0.png)

## 使用 Rotation3DAnimation 类旋转 3D 模型

在 WPF 中，你可以使用 Rotation3DAnimation 类来为应用于 3D 对象的 RotateTransform3D 对象的 Rotation 属性设置动画。Rotation3DAnimation 类使用两个值之间的线性插值来为 Rotation3D 属性设置动画。这些值是使用为动画设置的 From、To 和 By 属性的组合确定的。让我们创建一个应用程序，使用 Rotation3DAnimation 类旋转 3D 模型。为此，创建一个名为 Rotating3DModel 的 WPF 应用程序（也在 CD 上提供）并将清单 12.40 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.40：使用 Rotation3DAnimation 类

```
<Window x:Class="Rotating3DModel.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <DockPanel>
        <Viewbox>
<Canvas Width="321" Height="201">
    <Viewport3D Name="MyAnimatedobject"
ClipToBounds="True" Width="150" Height="150"
Canvas.Left="0" Canvas.Top="10">
        <Viewport3D.Camera>
            <PerspectiveCamera x:Name="myPerspectiveCamera" Position="0,0,2"
LookDirection="0,0,-1"
FieldOfView="60" />
        </Viewport3D.Camera>
        <Viewport3D.Children>
            <ModelVisual3D>
                <ModelVisual3D.Content>
                    <DirectionalLight Color="#FFFFFF" Direction="-0.612372,-0.5,-0.612372" />
                </ModelVisual3D.Content>
            </ModelVisual3D>
            <ModelVisual3D>
                <ModelVisual3D.Content>
                    <DirectionalLight Color="#FFFFFF" Direction="0.612372,-0.5,-0.612372" />
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
Positions="-0.5,-0.5,0.5 0.5,-0.5,0.5 -0.5,0.5 0.5,0.5,0.5 0.5,0.5,0.5 -0.5,0.5,0.5 -0.5,-0.5,0.5 " />
                        </GeometryModel3D.Geometry>
                        <GeometryModel3D.Material>
                            <MaterialGroup>
                                <DiffuseMaterial>
                                    <DiffuseMaterial.Brush>
                                        <LinearGradientBrush StartPoint="0,0.5" EndPoint="1,0.5">
                                            <LinearGradientBrush.GradientStops>
                                                <GradientStop Color="Yellow" Offset="0" />
                                                <GradientStop Color="Red" Offset="0.25" />
                                                <GradientStop Color="Yellow" Offset="0.75" />
                                                <GradientStop Color="Red" Offset="1" />
                                            </LinearGradientBrush.GradientStops>
                                        </LinearGradientBrush>
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
</Viewbox>
</DockPanel>
</Window>
```

在清单 12.40 中，一个 3D 对象被添加到应用程序中。动画附加到 3D 对象上。当窗口加载时，3D 对象开始移动。3D 对象的 RepeatBehavior 属性设置为 Forever。当你按下键盘上的 F5 键运行应用程序时，你会得到如图 12.42 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_631_0.png)

## 在 WPF 4.0 中使用多媒体

在图形和动画之后，另一种丰富的信息传达方式是多媒体。它是 WPF 的一部分，不仅提供丰富的 UI，而且以更好的方式传达你的信息。多媒体允许你在 WPF 中播放音频和视频文件。你可以将多媒体与动画集成，创建图形丰富的界面。你可以创建诸如将视频窗口放置在旋转的 3D 立方体上之类的效果。你已在本书章节的深入部分详细了解了多媒体。在本节中，你将学习实际应用以及如何在 WPF 中使用多媒体。

## 使用 Image 控件显示图像

在多媒体中，你可以使用 Image 控件显示图像。BitmapImage 标签用于定义图像源。BitmapImage 标签的 DecodePixelWidth 属性设置为与 Image 的 Width 相同。Stretch 属性决定图像的拉伸方式。让我们创建一个应用程序来显示图像。为此，创建一个名为 ImageControl 的 WPF 应用程序（可在 CD 上获得）并将清单 12.41 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.41：使用 Image 控件

```
<Window x:Class="ImageControl.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="400" Width="525">
    <StackPanel Height="300" Width="400">
        <Image Width="402" Stretch="UniformToFill" Height="298">
            <Image.Source>
                <BitmapImage DecodePixelWidth="200"
                    UriSource="D:\pictures\img8.jpg"/>
            </Image.Source>
        </Image>
    </StackPanel>
</Window>
```

在清单 12.41 中，使用 Image 控件将图像加载到应用程序中。Stretch 属性决定图像如何拉伸以填充 Image 控件。当你按下键盘上的 F5 键运行应用程序时，你会得到如图 12.43 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_632_0.png)

> NOTE
> 你已在第 10 章《使用 WPF 4.0 控件、资源、样式、模板和命令》中详细了解了 Image 控件。

## 转换图像

在 WPF 中，你可以使用 BitmapImage 类的属性来转换图像。你可以应用于 WPF 图像的不同转换是旋转、转换和裁剪图像。你可以使用 BitmapImage 类的 Rotation 属性旋转图像。你可以使用 FormatConvertedBitmap 类将图像转换为不同的像素格式，例如灰度。你可以使用 Clip 属性或 CroppedBitmap 属性裁剪图像。如果你想显示图像的一部分，应使用 Clip 属性，如果你想编码并保存裁剪后的图像，则应使用 CroppedBitmap 属性。让我们创建一个应用程序并执行不同的转换。为此，创建一个名为 TransformingImages 的 WPF 应用程序（可在 CD 上获得）并将清单 12.42 中的代码添加到 MainWindow.xaml 文件中：

### 清单 12.42：显示图像的转换

```
<Window x:Class="TransformingImages.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
```
