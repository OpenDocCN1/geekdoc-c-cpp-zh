The Add New Item dialog box opens. Select Window (WPF) and provide a name to it, if required. The default name is Window1.xaml. Now, click the Add button, as shown in Figure 12.50:

![](bbox=[0.19, 0.112, 0.74, 0.392])

Figure 12.50: Adding Window1

A new Window with the name Window1.xaml is added to your project. Add the code, given in Listing 12.52, in the Window1.xaml file:

# Listing 12.52: Adding the XAML Code for Media and Animation to the Window1.xaml File

```
<Window x:Class="PlayingMedia_UserEvent.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Window1" Height="300" Width="300">
    <Canvas Background="Pink">
        <Path Stroke="Purple" StrokeThickness="10">
            <Path.Data>
                <EllipseGeometry x:Name="MyEllipseGeometry" Center="125,125" RadiusX="50" RadiusY="25" />
            </Path.Data>
        </Path>
        <Path Stroke="Gold" StrokeThickness="10">
            <Path.Data>
                <EllipseGeometry x:Name="MyEllipseGeometry2" Center="125,125" RadiusX="25" RadiusY="50" />
            </Path.Data>
        </Path>
        <MediaElement Name="mediaElement1">
            <MediaElement.Triggers>
                <EventTrigger RoutedEvent="MediaElement.Loaded">
                    <EventTrigger.Actions>
                        <BeginStoryboard>
                            <Storyboard SlipBehavior="Slip">
                                <MediaTimeline Source="D:\wm afiles\Ringtone 01.wma" BeginTime="0:0:0" />
                                </MediaTimeline>
                                <DoubleAnimationUsingKeyFrames Storyboard.TargetName="MyEllipseGeometry" Storyboard.TargetProperty="RadiusY" RepeatBehavior="Forever">
                                    <DoubleAnimationUsingKeyFrames.KeyFrames>
                                        <LinearDoubleKeyFrame Value="100"
```