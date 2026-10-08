![](bbox=[0.13, 0.13, 0.48, 0.28])

+   5. **Connect the new button to the `stopSoundFile` action.**
Control+drag from the new button to the `MyAudioController` instance in the XIB project window. Select `stopSoundFile` from the black connections list overlay that opens.
6. **Control+drag from the three other buttons to the `MyAudioController` class and connect each one to its corresponding action.**
7. **Choose File > Save to save the MainMenu.xib file.**
8. **Return to Xcode and choose Build > Build and Go to test your work.**
When testing, initiate playback of an audio file that has a long duration with the Play Sound File button. While the file plays, click the Stop Sound File button to cease playback.

# # Watching Movies with Cocoa

Unless you've been living under a rock, you know that Mac OS X is a whiz at playing other kinds of multimedia content as well. *QuickTime* is a cross-platform multimedia engine that enables users to view, edit, and create all sorts of multimedia content. Chief among the various multimedia formats is the QuickTime movie. By using the QTKit framework in Cocoa, it's easy to add movie playback functions to your applications.

To work with QuickTime content in your projects, Cocoa provides you with five important classes:

+   - **`QTMovie`**: A movie that you want to view, edit, or create.
- **`QTTrack`**: Movies are composed of one or more tracks. `QTTrack` helps you to work with the individual tracks in a movie.