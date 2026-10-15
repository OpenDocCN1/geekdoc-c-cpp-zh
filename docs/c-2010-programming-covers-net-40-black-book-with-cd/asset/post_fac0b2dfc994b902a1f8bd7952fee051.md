
## Chapter 12: Using Graphics and Multimedia in Windows Forms and WPF

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

In Listing 12.21, the 3-D model is rotated by specifying the Axis and Angle properties of the RotateTransform3D class. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.25.

![](img/e073a4882197be4ab61103cbe0bcb394_606_0.png)

Figure 12.25: Showing the Output of the RotateTransform3D Application

### Using Animation in WPF 4.0

Animation in WPF includes the different types of animation, which are represented by the Timeline, Storyboard, and EventTrigger classes in addition to the KeyFrames collection. Animation can make an attractive, impressive, and useful UI. You can attach animations to the 2-D and 3-D graphics in WPF. You can create normal shapes and add animations to it. You have learned about animations in the In Depth section of the chapter. Let’s now learn about the practical implementation and create animation in WPF.

### Creating Animations Using Storyboards

Storyboards are a useful tool to create animation in WPF. The Storyboard object enables you to combine timelines that affect a variety of objects into a single timeline tree, and makes it easier for you to combine and control complex timing behavior. You can use a Storyboard timeline with triggers to create animation in WPF. Normally, the Storyboard class is used with the EventTrigger class. However, you can use them with other types of triggers to create animations in WPF.

### Using Event Triggers

The EventTrigger class is used to start a set of actions based on the occurrence of an event. For example, the action can be the click of the Button control and the event can be starting point of an animation on the click of the Button control. Let’s create an animation using the EventTrigger class. To do this, create a WPF application named EventTrigger (also available in CD) and add the code, given in Listing 12.22, to the MainWindow.xaml file and the listing shows how to control the Storyboard timeline after it starts:

Listing 12.22: Using the EventTrigger Class

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
Stroke="Black" Width="9" Fill="Blue" />
<Ellipse Canvas.Left="127" Canvas.Top="168" Height="10" Name="ellipse8"
Stroke="Black" Width="9" Fill="Blue" />
<Ellipse Canvas.Left="127" Canvas.Top="188" Height="10" Name="ellipse9"
Stroke="Black" Width="9" Fill="Blue" />
<Ellipse Canvas.Left="127" Canvas.Top="208" Height="10" Name="ellipse10"
Stroke="Black" Width="9" Fill="Blue" />
<Ellipse Canvas.Left="127" Canvas.Top="228" Height="10" Name="ellipse11"
Stroke="Black" Width="9" Fill="Blue" />
<Line X1="12" X2="400" Y1="145" Y2="115" Stroke="Black"
StrokeThickness="5" Height="158" Canvas.Left="131" Canvas.Top="114"
Width="42" />
<Path Name="path1" Stroke="Black" Data="M 60,113 Q 90,146 111,111"
StrokeThickness="5" Height="134" Canvas.Left="48" Canvas.Top="-14"
Width="145" />
<Line X1="124" X2="145" Y1="145" Y2="166" Stroke="Black"
StrokeThickness="5" Height="168" Canvas.Left="40" Canvas.Top="-7"
Width="147" />
<Line X1="145" X2="600" Y1="149" Y2="166" Stroke="Black"
StrokeThickness="5" Height="168" Canvas.Left="37" Canvas.Top="8"
Width="178" />
<Line X1="124" X2="170" Y1="145" Y2="16" Stroke="Black"
StrokeThickness="5" Height="115" Canvas.Left="-42" Canvas.Top="65"
Width="147" />
<Line X1="115" X2="145" Y1="145" Y2="166" Stroke="Black"
StrokeThickness="5" Height="168" Canvas.Left="-50" Canvas.Top="11"
Width="147" />
<Polygon Points="10,110 60,10 110,110" Fill="Blue" Height="55"
Canvas.Left="72" Canvas.Top="-7" Width="132" />
<Line X1="11" X2="145" Y1="145" Y2="166" Stroke="Black"
StrokeThickness="5" Height="163" Canvas.Left="83" Canvas.Top="110"
Width="41" />
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black"
StrokeThickness="5" Height="168" Canvas.Left="-23" Canvas.Top="94"
Width="151" />
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black"
StrokeThickness="5" Height="168" Canvas.Left="-1" Canvas.Top="94"
Width="147" />
<Line X1="11" X2="10" Y1="145" Y2="115" Stroke="Black"
StrokeThickness="5"
Height="158" Canvas.Left="121" Canvas.Top="-52" Width="42" />
<Polyline Name="Base" Points="10,110 6,10 110,110" Stroke="Black"
StrokeThickness="4" Height="52" Canvas.Left="209" Canvas.Top="210"
Width="50"/>
<Ellipse Canvas.Left="172" Canvas.Top="118" Height="100" Name="Ball"
Stroke="Black" Width="87">
<Ellipse.BitmapEffect>
<OuterGlowBitmapEffect GlowColor="DarkViolet" />
</Ellipse.BitmapEffect>
</Ellipse>
<Button Canvas.Left="235" Canvas.Top="12" Height="23"
Name="StartAnimation" Width="75">Start</Button>
<Button Canvas.Left="235" Canvas.Top="45" Height="23"
Name="StopAnimation" Width="75">Stop</Button>
</Canvas>
</Grid>
<DockPanel.Triggers>
```
