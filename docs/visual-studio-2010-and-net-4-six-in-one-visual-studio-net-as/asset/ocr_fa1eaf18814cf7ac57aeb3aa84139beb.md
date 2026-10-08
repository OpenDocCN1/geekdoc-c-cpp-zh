MediaElement can play both audio and video files. It supports a number of delivery methods (including progressive download, Windows Media Streaming over HTTP, ASX, Server Side Playlist, or a custom MediaStreamSource, where the developer can implement his or her own way of delivering to a decoder).

As for the encoding format, Windows Media Audio (WMA) Standard and Professional, as well as Windows Media Video 7, 8, and 9, are supported by the Microsoft codec family. For MP3 is also supported, and Video H.264 (which is the most widespread high-quality online video format) as well.

> For a complete reference of supported delivery methods, containers, and codecs, check the Silveright SDK documentation.

MediaElement can Play, Pause, and Seek media, or Stop playing. It fires events to track playing status, buffering, and current position within the media. It is also possible to control the Volume. The Stretch property behaves exactly as in the case of Videobox.

MediaElement is a rectangular element. Silverlight has a VideoBrush that can be associated with a MediaElement using the SourceName property. If a VideoBrush is used to fill an element, or even as the Stroke of a shape, the video will play within the element. It is an interesting effect when the VideoBrush is used as the Foreground brush for a TextBlock.

```
<UserControl.Resources>
<VideoBrush x:Key="myVideoBrush"
SourceName="myMediaElement" Stretch="UniformToFill//>
</UserControl.Resources>
<Grid Name="LayoutRoot" Background="White">
<MediaElement Visibility="Collapsed" x:Name="myMediaElement"
Source="http://msichline.llnw.net/dl/ch9/0/8/7/7/7/4/
SLExpression3launch_ch9.wmv"
Stretch="Uniform" />
<TextBlock Text="Text with a VideoBrush"
Foreground=(StaticResource myVideoBrush)
FontFamily="Arial Black" FontWeight="Bold"
FontSize="72" />
</Grid>
```

Figure 8-29 shows the output.

# Text with a VideoBrush

FIGURE 8-29: Text with a VideoBrush