
to define the light to show the model. SpecularMaterial adds illuminated highlight reflections when specular highlight reflections occur. The example code makes use of DiffuseMaterial and references a brush from the resource named mainCover:

```
<GeometryModel3D.Material>
    <DiffuseMaterial Brush="{StaticResource mainCover}" />
</GeometryModel3D.Material>
</GeometryModel3D>
```

The brush for the main cover is a VisualBrush. The VisualBrush has a Border with a Grid that consists of two Label elements. One Label element defines the text Professional C# 4 and is written to the cover:

```
<VisualBrush x:Key="mainCover">
    <VisualBrush.Visual>
        <Border Background="Red">
            <Grid>
                <Grid.RowDefinitions>
                    <RowDefinition Height="30" />
                    <RowDefinition Height="*" />
                </Grid.RowDefinitions>
                <Label Grid.Row="0" HorizontalAlignment="Center">
                    Professional C# 4</Label>
                <Label Grid.Row="1"></Label>
            </Grid>
        </Border>
    </VisualBrush.Visual>
</VisualBrush>
```

Because a brush is defined by a 2-D coordinate system and the model has a 3-D coordinate system, a translation between them needs to be done. This translation is done by the TextureCoordinates property of the MeshGeometry3D. The TextureCoordinates specify every point of the triangle and shows how it maps to 2-D. The first point 0 0 0 maps to 0 1, the second point 10 0 0 maps to 1 1, and so on. Be aware that y has a different direction in the 3-D and 2-D coordinate systems. Figure 35-36 shows the coordinate system for 2-D:

```
<MeshGeometry3D
Positions="0 0 0, 10 0 0, 0 10 0, 10 10 0, 10 0 0"
TriangleIndices="0, 1, 2, 2, 4, 3"
TextureCoordinates="0 1, 1 1, 0 0, 1 0, 1 1"
/>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1092_0.png)

FIGURE 35-36

## Cameras

A camera is needed with a 3-D model to see something. The example uses the PerspectiveCamera that has a position and a direction to look into. Changing the camera position to the left moves the model to the right and vice versa. Changing the y position of the camera, the model appears larger or smaller. With this camera, the further away the model is, the smaller it becomes:

```
<Viewport3D.Camera>
<PerspectiveCamera Position="0,0,25" LookDirection="15,6,-50" />
</Viewport3D.Camera>
```

code snippet 3DDemo/MainWindow.xaml

WPF also has an OrthographicCamera that doesn't have a horizon on the scene, so the size of the element doesn't change if it is further away. With MatrixCamera, the behavior of the camera can be exactly specified.

## Lights

Without a light it is dark. A 3-D scene requires a light to make the model visible. There are different lights that can be used. The AmbientLight lights the scene uniformly. DirectionalLight is a light that shines in one direction, similar to sunlight. PointLight has a position in space and lights in all directions. SpotLight has a position as well but uses a cone for its lighting.

The example code uses a SpotLight with a position, a direction, and cone angles:

```
<ModelVisual3D>
<ModelVisual3D.Content>
<SpotLight Color="White" InnerConeAngle="20" OuterConeAngle="60"
Direction="15,6,-50" Position="0,0,25" />
</ModelVisual3D.Content>
</ModelVisual3D>
```

## Rotation

To get a 3-D look from the model, it should be able to be rotated. For rotation, the RotateTransform3D element is used to define the center of the rotation and the rotation angle:

```
<Model3DGroup.Transform>
<RotateTransform3D CenterX="0" CenterY="0" CenterZ="0">
<RotateTransform3D.Rotation>
<AxisAngleRotation3D x:Name="angle" Axis="-1,-1,-1"
Angle="70" />
</RotateTransform3D.Rotation>
</RotateTransform3D>
</Model3DGroup.Transform>
```

To run a rotation from the completed model, an animation is started by an event trigger. The animation changes the Angle property of the AxisAngleRotation3D element continuously:

```
<Window.Triggers>
<EventTrigger RoutedEvent="Window.Loaded">
<BeginStoryboard>
<Storyboard>
<DoubleAnimation From="0" To="360" Duration="00:00:10"
Storyboard.TargetName="angle"
Storyboard.TargetProperty="Angle"
RepeatBehavior="Forever" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Window.Triggers>
```

After running the application, you will see the output in Figure 35-37.

![](img/d7d2ffa0a76feaab821930e95daace93_1094_0.png)

FIGURE 35-37

## SUMMARY

In this chapter, you have taken a first tour through the many features of WPF. WPF makes it easy to separate work between developers and designers. All UI features can be created with XAML, and the functionality by using code-behind.

You have seen many controls and containers that are all based on vector-based graphics. Because of vector-based graphics, WPF elements can be scaled, sheared, and rotated. Because of the content flexibility of content controls, the event-handling mechanism is based on bubbling and tunneling events.

Different kinds of brushes are available to paint background and foreground of elements. You can use solid brushes, linear or radial gradient brushes, but also visual brushes to do reflections or show videos.

Styling and templates allow you to customize the look of controls. Triggers allow you to change properties of WPF elements dynamically. Animations can be done easily by animating a property value from a WPF control.

The next chapter continues with WPF showing data binding, commands, navigation, and several more features.

Binding supports several binding modes between the target and source. Binding can be one-way, where the source information goes to the target, but if the user changes information in the user interface, the source does not get updated. For updates to the source, two-way binding is required.

The following table shows the binding modes and their requirements.

| BINDING MODE | DESCRIPTION |
|---|---|
| One-time | Binding goes from the source to the target and occurs only once when the application is started or the data context changes. Here, you get a snapshot of the data. |
| One-way | Binding goes from the source to the target. This is useful for read-only data, because it is not possible to change the data from the user interface. To get updates to the user interface, the source must implement the interface INotifyPropertyChanged. |
| Two-way | With two-way binding, the user can make changes to the data from the UI. Binding occurs in both directions — from the source to the target and from the target to the source. The source needs to implement read/write properties so that changes can be updated from the UI to the source. |
| One-way-to-source | With one-way-to-source binding, if the target property changes, the source object gets updated. |

WPF data binding involves many facets besides the binding modes. This section gives you details on binding to XAML elements, binding to simple .NET objects, and binding to lists. Using change notifications, the UI is updated with changes in the bound objects. You will read about getting the data from object data providers and directly from the code. Multibinding and priority binding demonstrates different binding possibilities other than the default binding. You will also read about dynamically selecting data templates, and validation of binding values.

Let's start with the BooksDemo sample application.

## BooksDemo Application

In this section, you create a new WPF application named BooksDemo to use throughout this chapter with data binding and commanding.

Change the XAML file MainWindow.xaml and add a DockPanel, a ListBox, a Hyperlink, and a TabControl:

```xml
<Window x:Class="Wrox.ProCSharp.WPF.MainWindow"
Insert IconMargin
[FILENAME]
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:Wrox.ProCSharp.WPF"
Title="Main Window" Height="400" Width="600">
<DockPanel>
<ListBox DockPanel.Dock="Left" Margin="5" MinWidth="120">
<ListBoxItem>
<Hyperlink Click="OnShowBook">Show Book</Hyperlink>
</ListBoxItem>
</ListBox>
<TabControl Margin="5" x:Name="tabControl1">
</TabControl>
</DockPanel>
</Window>
```

Now add a WPF user control named BookUC. This user control contains a DockPanel, a Grid with several rows and columns, a Label, and TextBox controls:
