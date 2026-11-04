# Part II: Application Development Using C#

Here's the complete XAML code for the media player:

```
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="472" Height="376"
    Background="#FFD6D4C8"
    x:Name="Page" >

    <MediaElement x:Name="MediaElement1" Width="466" Height="340"
        Stretch="Fill" Canvas.Left="3" Canvas.Top="3"
        AutoPlay="false"
        Source="WindowsMedia.wmv" />

    <Canvas Width="24" Height="24" Canvas.Left="5" Canvas.Top="348"
        x:Name="btnPlayPause">
        <Canvas Width="24" Height="24" x:Name="canvasPlay" >
            <Rectangle Width="24" Height="24" Fill="#FFFFFFF"
                Stroke="#FF000000" RadiusX="3" RadiusY="3" x:Name="RectPlay"
                StrokeThickness="2"/>
            <Polygon Points="8,5 8,19 18,13" StrokeThickness="5" Fill="Red"
                Width="24" Height="24"/>
        </Canvas>

        <Canvas Width="24" Height="24" x:Name="canvasPause"
            MouseEnter="PauseButtonMouseEnter"
            MouseLeave="PauseButtonMouseLeave" Opacity="0">
            <Rectangle Width="24" Height="24" Fill="#FFFFFFF"
                Stroke="#FF000000" RadiusX="3" RadiusY="3" x:Name="RectPause"
                StrokeThickness="2"/>
            <Rectangle Width="6" Height="14" Fill="#FF414141" Stroke="#FF000000"
                Canvas.Left="13" Canvas.Top="5" x:Name="rectPauseBar1"/>
            <Rectangle Width="6" Height="14" Fill="#FF414141" Stroke="#FF000000"
                Canvas.Left="5" Canvas.Top="5" x:Name="rectPauseBar2"/>
        </Canvas>
    </Canvas>

    <Canvas Width="255" Height="27" Canvas.Left="36" Canvas.Top="346"
        x:Name="canvasProgress">
        <Rectangle Width="244" Height="8" Fill="#FF414141" Stroke="#FF000000"
            Canvas.Top="10"
            x:Name="rectProgressWell"
            Canvas.Left="0.5" />
        <Rectangle Width="8" Height="8" Fill="#FF9D0808" Stroke="#FF000000"
            Canvas.Top="10" x:Name="rectDownloadProgress" StrokeThickness="0"
            Canvas.Left="0.5"/>
        <Ellipse Width="16" Height="16" Stroke="#FF000000" Canvas.Top="6"
            Canvas.Left="0"
            x:Name="ellMarker">
            <Ellipse.Fill>
                <RadialGradientBrush>
                    <GradientStop Color="#FF000000" Offset="0"/>
                    <GradientStop Color="#FFF6F6BC" Offset="1"/>
                </RadialGradientBrush>
            </Ellipse.Fill>
        </Ellipse>
    </Canvas>
```