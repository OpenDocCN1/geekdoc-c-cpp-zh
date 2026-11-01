
在数据网格中，您可以使用 Read、Selected 和 Edit 状态来为行定义不同的外观，具体取决于用户选择。MouseOver 和 IsPressed 也可以作为状态使用，以替代前面讨论过的触发器。

示例代码显示了婴儿的不同状态，并定义了 Sleeping、Playing 和 Crying 状态。状态在元素 VisualStateManager.VisualStateGroups 内定义。在这里，状态在 Button 元素内定义，因为它们仅在那里需要。通过内容，Button 定义了一个名为 border1 和 image1 的 Border 和 Image 元素。通过 VisualStateManager，定义了一个名为 CommonStates 的单个 VisualStateGroup。此状态组包含 VisualState 元素。在可视状态内定义了一个 Storyboard。对于所有状态，故事板都包含一个 ColorAnimation 来更改边框画刷的颜色，以及 ObjectAnimationUsingKeyFrames。此关键帧动画只是对 Image 的 Source 属性进行一次性更改。UriSource 属性需要一个创建的 BitmapImage 和存储在项目中的文件名。

VisualStateGroup 还包含 VisualTransition 元素，用于定义在状态更改之前应发生什么。使用 VisualTransition，您可以同时指定 From 和 To 值。通过这些，您可以创建在状态从 Sleeping 更改为 Crying 时与从 Playing 更改为 Crying 时不同的过渡。在示例中，仅使用 To 属性，因此无论之前的状态是什么，此过渡都适用。通过过渡，Button 的 Width 属性和 Border 元素的 Thickness 被更改：

```
<Window x:Class="VisualStateDemo.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="240" Width="500">
<DockPanel>
    <StackPanel Orientation="Vertical" DockPanel.Dock="Left">
        <Button Margin="5" Padding="3" Content="Sleeping" Click="OnSleeping" />
        <Button Margin="5" Padding="3" Content="Playing" Click="OnPlaying" />
        <Button Margin="5" Padding="5" Content="Crying" Click="OnCrying" />
    </StackPanel>
    <Grid>
        <Button Name="button1" Width="300" Height="200">
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup Name="CommonStates">
                    <VisualState Name="Sleeping">
                        <Storyboard>
                            <ObjectAnimationUsingKeyFrames Duration="0:0:0"
                                Storyboard.TargetProperty="(Image.Source)"
                                Storyboard.TargetName="image1">
                                <DiscreteObjectKeyFrame KeyTime="0:0:0">
                                    <DiscreteObjectKeyFrame.Value>
                                        <BitmapImage>
                                            <BitmapImage.UriSource>Images/Sleeping.jpg</BitmapImage.UriSource>
                                        </BitmapImage>
                                    </DiscreteObjectKeyFrame.Value>
                                </DiscreteObjectKeyFrame>
                            </ObjectAnimationUsingKeyFrames>
                            <ColorAnimation To="LightBlue"
                                Storyboard.TargetProperty="(SolidColorBrush.Color)"
                                Storyboard.TargetName="brush1" Duration="0:0:5" />
                        </Storyboard>
                    </VisualState>
                    <VisualState Name="Playing">
                        <Storyboard>
                            <ObjectAnimationUsingKeyFrames Duration="0:0:0"
                                Storyboard.TargetProperty="(Image.Source)"
                                Storyboard.TargetName="image1">
                                <DiscreteObjectKeyFrame KeyTime="0:0:0">
<BitmapImage UriSource="Images/Playing.jpg" />
<DiscreteObjectKeyFrame.Value>
<BitmapImage UriSource="Images/Playing.jpg" />
</DiscreteObjectKeyFrame.Value>
<ObjectAnimationUsingKeyFrames>
<ColorAnimation To="Red"
Storyboard.TargetProperty="(SolidColorBrush.Color)"
Storyboard.TargetName="brush1" Duration="0:0:0.5" />
</Storyboard>
</VisualState>
<VisualState Name="Crying">
<Storyboard>
<ObjectAnimationUsingKeyFrames Duration="0"
Storyboard.TargetProperty="(Image.Source)"
Storyboard.TargetName="image1">
<DiscreteObjectKeyFrame KeyTime="0:0">
<DiscreteObjectKeyFrame.Value>
<BitmapImage UriSource="Images/Crying.jpg" />
</DiscreteObjectKeyFrame.Value>
</DiscreteObjectKeyFrame>
</ObjectAnimationUsingKeyFrames>
<ColorAnimation To="LightBlue"
Storyboard.TargetProperty="(SolidColorBrush.Color)"
Storyboard.TargetName="brush1" Duration="0:0:0.5" />
</Storyboard>
</VisualState>
<VisualStateGroup.Transitions>
<VisualTransition To="Sleeping">
<Storyboard>
<DoubleAnimation By="50" AutoReverse="True"
Storyboard.TargetProperty="Width"
Storyboard.TargetName="button1"
Duration="0:0:1.2">
<DoubleAnimation.EasingFunction>
<BounceEase />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
</Storyboard>
</VisualTransition>
<VisualTransition To="Crying">
<Storyboard>
<ThicknessAnimation Duration="0:0:0.2" By="100,100"
AutoReverse="True"
Storyboard.TargetProperty=
"(Border.BorderThickness)"
Storyboard.TargetName="border1" />
</Storyboard>
</VisualTransition>
<VisualTransition To="Playing">
<Storyboard>
<DoubleAnimation By="50" AutoReverse="True"
Storyboard.TargetProperty="Width"
Storyboard.TargetName="button1"
Duration="0:0:1.2">
<DoubleAnimation.EasingFunction>
<ElasticEase />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
</Storyboard>
</VisualTransition>
</VisualStateGroup.Transitions>
```

负值向下。z 轴的正值方向指向观察者。

理解 WPF 中的 3-D 需要了解的最重要概念是模型、摄像机和灯光。模型使用三角形定义显示的内容。摄像机定义了观察模型的位置和方式，如果没有灯光，模型就会是黑暗的。灯光定义了整个场景的照明方式。本节将介绍如何使用 WPF 定义模型、摄像机和灯光，以及您在此处拥有的不同选项。此外，您还将获得有关如何对场景进行动画处理的信息。

## Model

本节创建一个具有书本 3-D 外观的模型。3-D 模型由三角形组成，因此最简单的模型只是一个三角形。更复杂的模型由多个三角形组成。矩形可以由两个三角形组成。球体由大量三角形组成。使用的三角形越多，球体越圆润。

对于书本模型，每个面都是一个矩形，可以由仅两个三角形组成。然而，由于封面前面有三种不同的材质，因此使用了六个三角形。

三角形由 MeshGeometry3D 的 Positions 属性定义。这里只是书本正面的一部分。MeshGeometry3D 定义了两个三角形。您可以数出五个点的坐标，因为第一个三角形的第三个点也是第二个三角形的第一个点。这可以为了优化而完成，以减少模型的大小。所有点都使用相同的 z 坐标 0，x/y 坐标 0 0、10 0、0 10、10 10 和 10 0。属性 TriangleIndices 表示位置的顺序。第一个三角形按顺时针定义，第二个三角形按逆时针定义。通过此属性，您定义三角形的哪一侧可见。三角形的一侧显示 GeometryModel3D 的 Material 属性定义的颜色，另一侧显示 BackMaterial 属性。

用于 3-D 的渲染表面是 ModelVisual3D，它包围模型，如下所示：

```
<ModelVisual3D>
    <ModelVisual3D.Content>
        <Model3DGroup>
            <!-- front -->
            <GeometryModel3D>
                <GeometryModel3D.Geometry>
                    <MeshGeometry3D
                        Positions="0 0 0, 10 0 0, 0 10 0, 10 10 0, 10 0 0"
                        TriangleIndices="0, 1, 2, 2, 4, 3"
                    />
                </GeometryModel3D.Geometry>
            </GeometryModel3D>
        </Model3DGroup>
    </ModelVisual3D.Content>
</ModelVisual3D>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1091_0.png)

FIGURE 35-35

代码片段 3DDemo/MainWindow.xaml

GeometryModel 的 Material 属性定义模型使用什么材质。根据视点，Material 或 BackMaterial 属性很重要。

WPF 提供不同的材质类型：DiffuseMaterial、EmissiveMaterial 和 SpecularMaterial。材质将与用于照亮场景的光一起影响模型的外观。EmissiveMaterial 和应用于材质画刷的颜色是计算的一部分
