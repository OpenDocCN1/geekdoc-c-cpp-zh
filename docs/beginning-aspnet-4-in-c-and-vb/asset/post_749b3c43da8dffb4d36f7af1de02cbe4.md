
With a data grid you can use Read, Selected, and Edit states to define different looks for a row, depending on user selection. MouseOver and IsPressed can be states as well that replace the triggers, which have been discussed earlier.

The example code displays different states of a baby and defines the states Sleeping, Playing, and Crying. The states are defined within the element VisualStateManager.VisualStateGroups. Here the states are defined within a Button element because they are needed only there. With the content, the Button defines a Border and an Image element that are named border1 and image1. With VisualStateManager, a single VisualStateGroup named CommonStates is defined. This state group contains VisualState elements. Within a visual state a Storyboard is defined. With all the states the storyboard contains a ColorAnimation that changes the color of the border brush, and ObjectAnimationUsingKeyFrames. This keyframe animation just makes a one-time change to the Source property of the Image. The UriSource property requires a BitmapImage that is created and a filename that is stored within the project.

The VisualStateGroup also contains VisualTransition elements that define what should happen before a state changes. With VisualTransition you can specify both From and To values. With these you can create different transitions when the state changes from Sleeping to Crying as opposed to from Playing to Crying. In the example, only the To property is used, so this transition applies no matter what the previous state was. With the transitions, the Width property of the Button and the Thickness of the Border element are changed:

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

negative values down. The z-axis defines positive values in direction to the viewer.

The most important concepts that need to be known to understand 3-D with WPF are the model, camera, and lights. The model defines what is shown using triangles. The camera defines the point where and how we look at the model, and without a light the model is dark. The light defines how the complete scene is illuminated. This section gives you information on how to define the model, camera, and light with WPF and what different options you have here. Also, you will get the information on how the scene can be animated.

## Model

This section creates a model that has the 3-D look of a book. A 3-D model is made up of triangles, so the simplest model is just one triangle. More complex models are made up from multiple triangles. Rectangles can be made up from two triangles. Balls are made up from a multiplicity of triangles. The more triangles used, the rounder the ball.

With the book model, each side is a rectangle, which could be made up from only two triangles. However, because the front cover has three different materials, six triangles are used.

A triangle is defined by the Positions property of the MeshGeometry3D. Here is just a part of the front side of the book. The MeshGeometry3D defines two triangles. You can count five coordinates for the points because the third point of the first triangle is also the first point of the second triangle. This can be done for optimization to reduce the size of the model. All the points use the same z coordinate, 0, and x/y coordinates 0 0, 10 0, 0 10, 10 10, and 10 0. The property TriangleIndices indicates the order of the positions. The first triangle is defined clockwise, the second triangle counterclockwise. With this property you define which side of the triangle is visible. One side of the triangle shows the color defined with the Material property of the GeometryModel3D, and the other side shows the BackMaterial property.

The rendering surface for 3-D is ModelVisual3D that surrounds the models as shown:

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

code snippet 3DDemo/MainWindow.xaml

The Material property of the GeometryModel defines what material is used by the model. Depending on the viewpoint, the Material or BackMaterial property is important.

WPF offers different material types: DiffuseMaterial, EmissiveMaterial, and SpecularMaterial. The material will influence the look of the model together with the light that is used to illuminate the scene. EmissiveMaterial and the color that is applied to the brush of the material is part of the calculations
