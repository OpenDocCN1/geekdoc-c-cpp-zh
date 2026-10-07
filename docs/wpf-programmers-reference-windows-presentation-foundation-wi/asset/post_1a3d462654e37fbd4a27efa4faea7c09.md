
# MediaElement Control

This appendix summarizes the MediaElement's most useful properties, methods, and events.
Note that many of these properties shown in Tables E-1 through E-3 are read-only.

## TABLE E-1: Key Properties of Media

| PROPERTY | PURPOSE |
| --- | --- |
| Balance | Determines the speaker balance. |
| BufferingProgress | Returns the percentage of buffering complete. |
| CanPause | Returns True if the media can be paused. |
| DownloadProgress | Returns the percentage of download complete. |
| HasAudio | Returns True if the media has audio. |
| HasVideo | Returns True if the media has video. |
| IsBuffering | Returns True if the control is buffering its media. |
| IsMuted | Returns True if it is muted. |
| LoadedBehavior | Determines what the control does when it is loaded. This can be Manual ("manually" in code), Play (play when there's valid media), Close (close and release all memory), Pause (prepare to play and then pause), or Stop (prepare to play and then stop). |
| NaturalDuration | Returns the media's natural duration. This can be TimeSpan (use NaturalDuration.HasTimeSpan), Automatic, or Forever. |
| NaturalVideoHeight | Returns the video's height. |
| NaturalVideoWidth | Returns the video's width. |
| Position | Determines the playback position. |
| ScrubbingEnabled | Determines the control updates itself when a seek is performed while the control is paused. |
| Source | The media's source |
| SpeedRatio | Determines the speed ratio. Use a value less than 1 for slow motion or a value greater than 1 for fast motion. |
| Volume | Determines the audio volume between 0 and 1. |

## TABLE E-2: Key Methods for Media

| METHODS | PURPOSE |
| --- | --- |
| Pause | Pauses media playback. Use the Play method to restart playback. |
| Play | Starts media playback. |
| Stop | Stops media playback and resets the control to play from the beginning. |

## TABLE E-3: Key Events for Media

| EVENT | PURPOSE |
| --- | --- |
| BufferingEnded | Occurs when the control finishes buffering. |
| BufferingStarted | Occurs when the control starts buffering. |
| MediaEnded | Occurs when the media ends. |
| MediaFailed | Occurs when the control has an error. |
| MediaOpened | Occurs when the media is loaded. |

## EXAMPLE Controlling Media

The ControlMedia example program in Figure E-1 uses a MediaElement to play a video. The buttons from left to right allow you to rewind 5 seconds, play, pause, stop 5 seconds, and add a bookmark to the ListBox. If you click on a bookmark entry, the control jumps to that position in the video. The scrollbar at the bottom lets you view and change the playback position.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_526_0.png)

FIGURE E-1

Since this program's XAML code is reasonably straightforward, it isn't shown here. Download the example program and look it over.

The following code shows the program's C# code-behind. (As is the case for all of the examples, you can also download a Visual Basic version.)

```csharp
private DispatcherTimer tmrProgress = new DispatcherTimer();

// Prepare the timer.
private void WindowLoaded(object sender, RoutedEventArgs e) {
    tmrProgress = new DispatcherTimer();
    tmrProgress.Tick += tmrProgress.Tick;
}

private void btnPlayClick(object sender, RoutedEventArgs e) {
    mmBear.Position = mmBear.Position.Add(new TimeSpan(0, 0, -5));
}

private void btnPauseClick(object sender, RoutedEventArgs e) {
    mmBear.Play();
    tmrProgress.Start();
}

private void btnStopClick(object sender, RoutedEventArgs e) {
    mmBear.Stop();
    tmrProgress.Stop();
}
```

```csharp
private void btnForward_Click(object sender, RoutedEventArgs e)
{
    mmBear.Position = mmBear.Position.Add(new TimeSpan(0, 0, 5));
}
private void btnBookmark_Click(object sender, RoutedEventArgs e)
{
    lstBookmarks.Items.Add(mmBear.Position);
}
// Jump to this bookmark.
private void SelectionChanged(object sender, SelectionEventArgs e)
{
    if (mmBear == null) return;
    if (e.AddedItems.Count < 1) return;
    TimeSpan bookmark = (TimeSpan)e.AddedItems[0];
    mmBear.Position = bookmark;
    scrProgress.Value = mmBear.Position.TotalSeconds;
    lstBookmarks.SelectedIndex = -1;
}
// Display the media's progress.
private void tmProgress_Tick(Object sender, System.EventArgs e)
{
    scrProgress.Value = mmBear.Position.TotalSeconds;
}
// Prepare the progress ScrollBar.
private void MediaOpened(System.Object sender, System.Windows.RoutedEventArgs e)
{
    if (mmBear.Media.NaturalDuration.HasTimeSpan)
    {
        TimeSpan ts = mmBear.Media.NaturalDuration.TimeSpan;
        scrProgress.Maximum = ts.TotalSeconds;
        scrProgress.SmallChange = 1;
        scrProgress.LargeChange = ts.TotalSeconds / 10;
    } else {
        scrProgress.Visibility = Visibility.Hidden;
    }
}
// Go to the selected position.
private void scr_Scroll(object sender, System.Windows.Primitives.ScrollEventArgs e)
{
    mmBear.Position = TimeSpan.FromSeconds(e.NewValue);
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_527_0.png)

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

When the window loads, the program creates a new DispatcherTimer and registers the tmProgress_Tick event handler to receive the timer's Tick events.

The program’s rewind, play, pause, stop, and forward event handlers are straightforward. They simply invoke the MediaElement’s corresponding methods.

The bookmark Button’s event handler adds the MediaControl’s position.

# Pens

This appendix summarizes Pens. A Pen defines the colors and geometry of lines, paths, and edges.

Typically Pen properties are provided by some other than the Pen itself. For example, the Ellipse defines its border.

```xml
<Ellipse Width="200" Height="100" Stroke="10">
```

## TABLE F-1: Key Properties of Pen

| PROPERTY | PURPOSE |
| --- | --- |
| Stroke | Determines the Pen's Brush. This can be a solid color or an element such as LinearGradientBrush. |
| StrokeDashArray | Determines the Pen's pattern of draw and skipped segments in units of pen thickness. For example, the pattern 3,1 means "draw three pens, skip one pen, and repeat.".
| StrokeDashCap | Determines the shape of ends of each dash. This can be Flat, Round, or Square. |
| StrokeDashOffset | Determines how far into the first dash the line starts. |
| StrokeEndLineCap | Determines the shape of the Pen's ending. This can be Flat, Round, or Square. |
| StrokeLineJoin | Determines how the Pen draws corners. This can be Bevel, Miter, or Round. |
| StrokeMiterLimit | Determines how pointy a corner can be when two segments connect as in Polygon. |
| StrokeStartLineCap | Determines the shape of the Pen's starting end. This can be Flat, Round, or Square. |
| StrokeThickness | Determines the Pen's thickness.

## EXAMPLE EXAMPLE StrokeMiterLimit

The StrokeMiterLimit example program in Figure F-1 uses the following code to draw its shape. This example defines the Pen's Stroke property with an element containing a RadialGradientBrush. It also sets StrokeMiterLimit to 3 as the sharpest corner on the lower right is visible.

```xml
<Polygon Points="100.3,30.2,250.0,30.7,200.5,75,170*" StrokeThickness="20"
<StrokeLineJoin="Miter" StrokeMiterLimit="3">
<Polygon.Stroke>
  <RadialGradientBrush>
    <GradientStop Offset="0" Color="Gray"/>
    <GradientStop Offset="0.5" Color="Gray"/>
    <GradientStop Offset="1" Color="Black"/>
  </RadialGradientBrush>
</Polygon.Stroke>
</Polygon>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_531_0.png)

The Dashes example program in Figure F-2 demonstrates the StrokeStartLineCap, StrokeEndLineCap, and StrokeDash values.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_531_1.png)
