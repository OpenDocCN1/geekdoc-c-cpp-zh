
## Adding Media Using the MediaPlayer Class

You can add media using the MediaPlayer class in WPF. The difference between the MediaElement class and the MediaPlayer class is that, you can declare an instance of the MediaPlayer class in XAML, but you cannot load and play the media without using code. To play media only in XAML, use the MediaElement class. Let’s create an application to play the media using the MediaPlayer class. To do this, create a WPF application named UsingMediaPlayer (also available in CD) and add the code, given in Listing 12.46, to the MainWindow.xaml file:

### Listing 12.46: Using the MediaPlayer Class

```
<Window x:Class="UsingMediaPlayer.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Button Margin="77,100,64,111" Name="button1" Click="button1_Click">Click to Play</Button>
    </Grid>
</Window>
```

In Listing 12.46, a Button is added to the window. The media is attached to the Click event of the Button control. The code for the Click event of the Button control is given in Listing 12.47:

### Listing 12.47: Adding the Code for the MediaPlayer Control

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Windows.Media.Animation;
namespace UsingMediaPlayer
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, RoutedEventArgs e)
        {
            MediaTimeline myTime = new MediaTimeline(new Uri(@"D:\wmafiles\Ringtone 01.wma", UriKind.Relative));
            myTime.RepeatBehavior = RepeatBehavior.Forever;
            MediaClock myClock = myTime.CreateClock();
            MediaPlayer myPlayer = new MediaPlayer();
            myPlayer.Clock = myClock;
            VideoDrawing myDrawing = new VideoDrawing();
            myDrawing.Rect = new Rect(0, 0, 100, 100);
            myDrawing.Player = myPlayer;
        }
    }
}
```

Note that before executing the application you must change the path of the media file as per the location of the media file on your system. The code calls the media file when you click the Button control. The final output is shown in Figure 12.47:

![](img/e073a4882197be4ab61103cbe0bcb394_638_0.png)

Figure 12.47: Using the MediaPlayer Control

The media file attached to the code plays when you click the Button control.

## Using Storyboard to Control the Media Playback

You have learned to control the playback of media through user input. You have added code on the click of the Button control to control the media playback. You can control the media playback through XAML code. You need to use the Storyboard timeline to control the media playback through XAML code. You cannot use the MediaPlayer class to control the media through XAML code. When you use the Storyboard timeline to control the timing of the MediaElement control, the functionality is same as the Timeline object used in animation. The MediaTimeline class uses the BeginTime property to specify when to start the MediaElement control. It uses the Duration property to specify the duration up to which the MediaElement control is active. Let's create an application to control the media playback using the Storyboard class. To do this, create a WPF application named Storyboard_MediaPlayback (also available in CD) and add the code, given in Listing 12.48, to the MainWindow.xaml file:

### Listing 12.48: Using the Storyboard Class

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
<Storyboard>
    <MediaTimeline Source="D:\wmafiles\Ringtone 01.wma" Storyboard.TargetName="mediaElement1" CurrentTimeInvalidated="MediaTimeChanged"/>
</Storyboard>
</BeginStoryboard>
</EventTrigger.Actions>
</EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="button2">
    <EventTrigger.Actions>
        <PauseStoryboard BeginStoryboardName="Play">
        </PauseStoryboard>
    </EventTrigger.Actions>
</EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="button3">
    <EventTrigger.Actions>
        <ResumeStoryboard BeginStoryboardName="Play">
        </ResumeStoryboard>
    </EventTrigger.Actions>
</EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="button4">
    <EventTrigger.Actions>
        <StopStoryboard BeginStoryboardName="Play">
        </StopStoryboard>
    </EventTrigger.Actions>
</EventTrigger>
</Grid.Triggers>
</Grid>
</window>
```

In Listing 12.48, the MediaTimeline control is added to play media file. The Button controls are added to control the playback of the media. The Slider control is added to show the progress of media. The playback of media is controlled by using the Storyboard timeline on the click of the Button control. The functionality for the progress bar, which is the Slider control, is added through the code file given in Listing 12.49:

### Listing 12.49: Controlling the Slider Control

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace Storyboard_MediaPlayback
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
```

```
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Diagnostics;
namespace PlayingMedia_UserEvent
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, RoutedEventArgs e)
        {
            Window1 mywindow = new Window1();
            mywindow.Show();
            this.Close();
        }
    }
}
```

You need to load a new window on the click of the Button control and play the media and animation on the second window. To do this, right-click the project name, PlayingMedia_UserEvent, in the Solution Explorer and select Add→Window, as shown in Figure 12.49:

![](img/e073a4882197be4ab61103cbe0bcb394_641_0.png)

Figure 12.49: Adding New Item
