```
myDrawing.Player = myPlayer;
}
}
```

Note that before executing the application you must change the path of the media file as per the location of the media file on your system. The code calls the media file when you click the Button control. The final output is shown in Figure 12.47:

![](bbox=[0.33, 0.18, 0.59, 0.36])

Figure 12.47: Using the MediaPlayer Control

The media file attached to the code plays when you click the Button control.

# Using Storyboard to Control the Media Playback

You have learned to control the playback of media through user input. You have added code on the click of the Button control to control the media playback. You can control the media playback through XAML code. You need to use the Storyboard timeline to control the media playback through XAML code. You cannot use the MediaPlayer class to control the media through XAML code. When you use the Storyboard timeline to control the timing of the MediaElement control, the functionality is same as the Timeline object used in animation. The MediaTimeline class uses the BeginTime property to specify when to start the MediaElement control. It uses the Duration property to specify the duration up to which the MediaElement control is active. Let's create an application to control the media playback using the Storyboard class. To do this, create a WPF application named Storyboard_MediaPlayback (also available in CD) and add the code, given in Listing 12.48, to the MainWindow.xaml file:

Listing 12.48: Using the Storyboard Class

```
<Window x:Class="Storyboard_MediaPlayback.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<Grid Background="Aquamarine">
<Button HorizontalAlignment="Left" Margin="0,0,0,99" Name="button1" Width="75" Height="23" VerticalAlignment="Bottom">Play</Button>
<Button Margin="67,0,136,99" Name="button2" Height="23" VerticalAlignment="Bottom">Pause</Button>
<Button Margin="137,0,66,99" Name="button3" Height="23" VerticalAlignment="Bottom">Resume</Button>
<Button HorizontalAlignment="Right" Margin="0,0,0,99" Name="button4" Width="75" Height="23" VerticalAlignment="Bottom">Stop</Button>
<MediaElement Margin="0,0,118,0" Name="mediaElement1" Height="120" VerticalAlignment="Top" MediaOpened="Element_MediaOpened"/>
<Slider Height="21" Margin="77,0,101,54" Name="slider1" VerticalAlignment="Bottom" />
<Grid.Triggers>
<EventTrigger RoutedEvent="Button.Click" SourceName="button1">
<EventTrigger.Actions>
<BeginStoryboard Name="Play">
```