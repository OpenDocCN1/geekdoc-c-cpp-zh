
The MediaElement class has several properties, methods, and events that allow you to add and manipulate media through the MediaElement control. Table 17.9 lists the noteworthy properties of the MediaElement class:

Table 17.9: Noteworthy Properties of the MediaElement Class

| Property | Description |
|---|---|
| Attributes | Retrieves a collection of attributes for the current entry in the Advanced Stream Redirector (ASX) file that is the source media in the MediaElement control. |
| AudioStreamCount | Retrieves the number of audio streams in the currently opened media file. |
| AudioStreamIndex | Sets or retrieves the index of the audio stream that plays simultaneously with the video. The default value for this property is a null reference. |
| AutoPlay | Sets or retrieves a value that indicates whether the media automatically starts playing as soon as the MediaElement is loaded. By default, the value of this property is true. |
| Balance | Sets or retrieves the proportion of balance among the stereo speakers. This property has the default value of zero and can range between -1 and 1. If you set the value of this property to -1, then the left stereo speaker is on full volume. If you set value of this property to 1, then the right stereo speaker is on full volume. |
| BufferingProgress | Retrieves a value that denotes the current amount of buffering for the current media. The default value of this property is zero and can be any fractional value up to 1. |
| BufferingTime | Sets or retrieves the amount of time for buffering. The default value of this property is five seconds. |
| CanPause | Retrieves a value that indicates whether the currently opened media can be paused. |
| CanSeek | Retrieves a value that indicates whether you can change the position of the media. |
| CurrentState | Retrieves the current state of the MediaElement control. This property can return any of the values – Buffering, Opening, Playing, Paused, Stopped, and Closed. |
| DownloadProgress | Retrieves the percentage of the media (at a remote location) downloaded. The default value is zero. |
| DownloadProgressOffset | Retrieves the offset for downloading the media. |
| DroppedFramesPerSecond | Retrieves the number of frames per second dropped by the media file. |
| IsMuted | Sets or retrieves a value that indicates whether the media is silent (muted). |
| Markers | Retrieves a collection of markers present in the media file. |
| NaturalDuration | Retrieves the total time of the media. |
| NaturalVideoHeight | Retrieves the height (in pixels) of the video for the MediaElement control. For audio, this property has a value of zero. |
| NaturalVideoWidth | Retrieves the width (in pixels) of the video for the MediaElement control. For audio, this property has a value of zero. |
| Position | Sets or retrieves the position (instance of time) in the entire playback of the media. |
| RenderedFramesPerSecond | Retrieves the number of frames rendered per second for the MediaElement control. |
| Source | Sets or retrieves the source (media file) to be played in the MediaElement control. |
| Stretch | Sets or retrieves a value that indicates the way the media occupies the UI of the MediaElement control. This property can take None, Uniform, UniformToFill, or Fill as its value. |
| Volume | Sets or retrieves the volume of the media. The default value of this property is 0.5 and can range between zero and one. |

Table 17.10 lists the noteworthy methods of the MediaElement class:

Table 17.10: Noteworthy Methods of the MediaElement Class

| Method | Description |
|---|---|
| Pause | Pauses the media at the current position (instance of time) |
| Play | Starts playing the media from the current position (instance of time) |
| SetSource | Sets the source of the MediaElement control |
| Stop | Stops the playback of media and resets the media to start from the beginning |

Table 17.11 lists the noteworthy events of the MediaElement class:

Table 17.11: Noteworthy Events of the MediaElement Class

| Event | Description |
|---|---|
| BufferingProgressChanged | Occurs when the amount of buffering for the current media file changes. |
| CurrentStateChanged | Occurs when the current state of the media changes. |
| DownloadProgressChanged | Occurs when the current download progress of the media changes. |
| MarkerReached | Occurs when a marker is reached during the playback of the media. |
| MediaEnded | Occurs when no media is being played in the MediaElement control. |
| MediaFailed | Occurs when an error related to the media is raised. The error may occur when the media file is not found or when the media file is in an unsupported media format. |
| MediaOpened | Occurs when the media is opened and the media headers are read by the MediaElement control. |

Next, let’s discuss about the Silverlight 3.0 Popup control.

## The Popup Control

The Popup control is used to display any information or description on top of some other control, such as a Button or Grid control. The Popup control can appear only for a single UI control. This implies that if you want to display some information for multiple controls, you need to encapsulate them within a container control, such as a Grid or StackPanel control. In addition, a Popup control can either be displayed over an existing Silverlight content or within the margins of a Silverlight control. In addition, one Popup control may appear on top of another Popup control. Figure 17.14 shows a Popup control:

![](img/e073a4882197be4ab61103cbe0bcb394_891_0.png)

Figure 17.14: The Popup Control in Silverlight 3.0

The Popup control is an instance of the Popup class, which exists in the System.Windows.Controls.dll assembly in the System.Windows.Controls.Primitives namespace. The class hierarchy of the Popup class is:

```
System.Object
  System.Windows.DependencyObject
    System.Windows.UIElement
      System.Windows.FrameworkElement
        System.Windows.Controls.Primitives.Popup
```

The Popup class has some properties and events that allow you to work with Popup controls in the Silverlight applications. Table 17.12 lists the noteworthy properties of the Popup class:

Table 17.12: Noteworthy Properties of the Popup Class

| Property | Description |
|---|---|
| Child | Sets or retrieves the UI element or content hosted in the popup. |
| HorizontalOffset | Sets or retrieves the distance (in pixels) between the left sides of the control and the popup. The popup, by default, appears in the bottom or bottom-left corner of the control. |
| IsOpen | Sets or retrieves a value that indicates whether the popup is visible on the screen. |
| VerticalOffset | Sets or retrieves the distance (in pixels) from the top of the control to the top of the popup. |

Table 17.13 lists the noteworthy events of the Popup class:

Table 17.13: Noteworthy Events of the Popup Class

| Event | Description |
|---|---|
| Closed | Occurs when the popup is just closed. |
| Opened | Occurs when the popup appears. |

Now, let’s discuss the TabControl control in Silverlight 3.0.

## The TabControl Control

The TabControl control allows you to utilize the available UI space of a Silverlight application by providing a tabbed surface. A TabControl control has several tabs, each of which further contains one or more controls. Every tab has a header that is visible at all times and the content that is visible only when you select the tab by clicking it. You can select only one tab at a time. Figure 17.15 shows a TabControl control:

![](img/e073a4882197be4ab61103cbe0bcb394_892_0.png)

The TabControl control is an instance of the TabControl class, which exists in the System.Windows.Controls.dll assembly in the System.Windows.Controls namespace. The class hierarchy of the TabControl class is:

```
System.Object
    System.Windows.DependencyObject
        System.Windows.UIElement
            System.Windows.FrameworkElement
                System.Windows.Controls.Control
                    System.Windows.Controls.ItemsControl
                        System.Windows.Controls.TabControl
```
