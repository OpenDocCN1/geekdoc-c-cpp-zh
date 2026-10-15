The MediaElement class has several properties, methods, and events that allow you to add and manipulate media through the MediaElement control. Table 17.9 lists the noteworthy properties of the MediaElement class:

| Property | Description |
|---|---|
| Table 17.9: Noteworthy Properties of the MediaElement Class | |
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