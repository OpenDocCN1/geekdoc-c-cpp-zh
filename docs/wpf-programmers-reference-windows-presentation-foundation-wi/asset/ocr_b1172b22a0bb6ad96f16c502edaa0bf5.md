The following code shows how the UseMediaElement example program controls the video control:

```
// Play the video file.
private void btnPlayVideo_Click(object sender, RoutedEventArgs e)
{
    mmJulia.Play();
}
```

```
// Pause the video file.
private void btnPauseVideo_Click(object sender, RoutedEventArgs e)
{
    mmJulia.Pause();
}
```

```
// Rewind the video file.
private void btnRewindVideo_Click(object sender, RoutedEventArgs e)
{
    mmJulia.Position = new TimeSpan(0);
}
```

# UseMediaElement

Figure 5-3 shows the UseMediaElement program action.

![](bbox=[0.535, 0.438, 0.875, 0.573])

FIGURE 5-3

Unfortunately, the MediaElement control doesn't provide any dependency properties that a XAML file control its playback. For example, it doesn't provide an IsPlaying or State property that XAML code could set to control the play or pause. That means you have to write code-behind to control the media.

However, XAML does include a SoundPlayerAction command that allows you to play an audio file to the end without pausing or stopping. You can write XAML trigger to invoke this command when an event takes place.

The following XAML code defines a trigger that executes when the btnSoundPlayerAction button fires its Click. When the code executes, the SoundPlayerAction plays the file notify.wav.

```
<Window.Triggers>
  <EventTrigger RoutedEvent="Button.Click"
    SourceName="btnSoundPlayerAction">
    <SoundPlayerAction Source="notify.wav"/>
  </EventTrigger>
</Window.Triggers>
```

# UseMediaElement