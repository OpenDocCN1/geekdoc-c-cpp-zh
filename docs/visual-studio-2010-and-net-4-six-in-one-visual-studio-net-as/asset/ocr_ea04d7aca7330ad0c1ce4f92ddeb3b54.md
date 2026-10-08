The animations to the element ellipseTranslate, which is defined within the Ellipse tag:

```
<Ellipse x:Name="ellipse" Fill="Black" Height="50">
Canvas.Left="20" Canvas.Top="20" Width="50">
  <Ellipse.RenderTransform>
    <TranslateTransform x:Name="ellipseTranslate" />
  </Ellipse.RenderTransform>
</Ellipse>
```

Changing the size, position, rotation, or other transformations via Silverlight's render transformations does not trigger a layout recalculation. This results in much less work for the CPU to do; therefore, more complex animations can be performed before the performance starts to degrade. WPF has the notion of layout transformations that affect the layout—this can be very useful in certain cases. For Silverlight, the Silverlight Toolkit has a LayoutTransformer that pretty much the same thing.

![](bbox=[0.625, 0.258, 0.93, 0.42])

Figure 8-28 shows the available transformations in Silverlight, except TranslateTransform, which simply relocates the element.

> Figure 8-28: Render transformations in Silverlight

# Media

Media in Silverlight includes playing audio and video files, access to the microphone and the webcam on the computer, DRM, and Deep Zoom. This section describes the basics of Silverlight media.

# Audio and Video Playback

Just playing an audio or video file is very simple when using the MediaElement control. When compiled and run, this code pays back a Designer-versus-Developer view over Channel9:

```
<UserControl x:Class="Mediaelems.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
c:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot" Background="White">
  <MediaElement Source="http://mschnlnline.llwd.net/dl/ch9/0/8/7/7/7/4/SL3ExpressionLaunch_ch9.wmv"
Stretch="Uniform" />
</Grid>
</UserControl>
```