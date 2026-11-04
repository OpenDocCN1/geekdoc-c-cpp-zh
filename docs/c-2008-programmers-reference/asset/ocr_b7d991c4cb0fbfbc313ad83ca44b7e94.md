# Disabling Auto-Play

While automatically playing a video is a useful feature, sometimes you might want to disable this. For example, if you have multiple videos embedded in a page, this feature is actually more nuisance than helpful. To disable the auto-play feature, just set the AutoPlay attribute in the <MediaElement> element to False, like this:

```
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
        Width="320" Height="240"
        Source="WindowsMedia.wmv"
        Stretch="Fill"
        Canvas.Top="8" Canvas.Left="8"
        AutoPlay="False"
    />
</Canvas>
```

So how and when do you get it to play? You can programmatically play the video when the user's mouse enters the video and pause it when the mouse leaves the video. Also, if the user clicks on the video, the video can stop and return to the beginning. To do so, set the following highlighted attributes:

```
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Width="640" Height="480"
    Background="White"
    x:Name="Page">
    <MediaElement x:Name="WindowsMedia_wmv"
        Width="320" Height="240"
        Source="WindowsMedia.wmv"
        Stretch="Fill"
        Canvas.Top="8" Canvas.Left="8"
        AutoPlay="False"
        MouseEnter="MouseEnter"
        MouseLeave="MouseLeave"
        MouseLeftButtonDown="MouseClick"
    />
</Canvas>
```

Basically, you are setting the event handlers for the various events handled by the <MediaElement> element. To write the event handler, go to the Project window and double-click on the Page.xaml.cs file.