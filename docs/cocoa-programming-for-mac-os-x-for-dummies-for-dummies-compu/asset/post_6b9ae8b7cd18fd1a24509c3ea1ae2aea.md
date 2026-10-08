
![](img/ea40cad434a338535474e82c1a6ace20_324_0.png)

5. **Connect the new button to the `stopSoundFile` action.**
Control+drag from the new button to the `MyAudioController` instance in the XIB project window. Select `stopSoundFile` from the black connections list overlay that opens.
6. **Control+drag from the three other buttons to the `MyAudioController` class and connect each one to its corresponding action.**
7. **Choose File > Save to save the MainMenu.xib file.**
8. **Return to Xcode and choose Build > Build and Go to test your work.**
When testing, initiate playback of an audio file that has a long duration with the Play Sound File button. While the file plays, click the Stop Sound File button to cease playback.

## Watching Movies with Cocoa

Unless you've been living under a rock, you know that Mac OS X is a whiz at playing other kinds of multimedia content as well. *QuickTime* is a cross-platform multimedia engine that enables users to view, edit, and create all sorts of multimedia content. Chief among the various multimedia formats is the QuickTime movie. By using the QTKit framework in Cocoa, it's easy to add movie playback functions to your applications.

To work with QuickTime content in your projects, Cocoa provides you with five important classes:

- **`QTMovie`**: A movie that you want to view, edit, or create.
- **`QTTrack`**: Movies are composed of one or more tracks. `QTTrack` helps you to work with the individual tracks in a movie.
- **QTMedia**: Each track in a movie is composed of media. **QTMedia** lets you get and set information media in a track.
- **QTDataReference**: QuickTime is multifaceted and permits you to load movies from files, the Internet, or even straight from memory. **QTDataReference** is the QuickTime class that you use when you need this level of access.
- **QTMovieView**: A movie player you use to play a **QTMovie**.

Because the QTKit framework is so vast, and in certain cases, somewhat advanced, I show you two classes: **QTMovie** and **QTMovieView**. With these two classes, you can load a movie and display it in a fully functional player.

### QTMovie

**QTMovie** is a class that represents a QuickTime movie. **QTMovie** can load movies into from files, Uniform Resource Locators (URLs), data references, or even the Pasteboard (Clipboard). For this section, I show you how to use the movieWithFile class method of the **QTMovie** class to load a movie from a file.

Earlier in this chapter, you loaded a sound file with an NSOpenPanel. Then you used the result from that NSOpenPanel to open the file using a traditional file path. You can follow a similar methodology for movies, but you have to expand the functionality a bit by filtering which files a user can select in the NSOpenPanel. To do this, you must pass an array to the runModalForType method of NSOpenPanel:

1. Create an array that defines which file types a user can open.

The last item in the array is always nil. For example, to define an array for .mov and .mp4 files, your code might look like this:

```objc
NSArray *fileTypes = [NSArray arrayWithObjects:@"mov",
@"mp4", nil];
```

2. Pass the array to runModalForType:

```objc
if ([openPanel runModalForTypes:fileTypes] ==
NSOKButton) {
// code to load a movie goes here
}
```

3. Pass the file path to the movieWithFile class method to create a **QTMovie**.

```objc
QTMovie *movie = [QTMovie movieWithFile:theFilePath
error:nil];
```

### QTMovieView

After you load a movie, use the *QTMovieView* class to play it. You can find the *QTMovieView* control in the Library window of Interface Builder (see Figure 16-7) by searching for Movie View via the search field at the bottom of the Library window.

![](img/ea40cad434a338535474e82c1a6ace20_326_0.png)

*QTMovieView* has several attributes that you can set manually in Interface Builder — see Figure 16-8 — or programmatically with code.

![](img/ea40cad434a338535474e82c1a6ace20_326_1.png)

Here are the attributes you can set in Interface Builder:

- **Display color:** Control the color of the `QTMovieView` when no movie is loaded. The default color is black, but you can change it to whatever color you desire.
- **Show controller:** Toggle the display of the built-in QuickTime controller, which appears at the bottom of the `QTMovieView` control when you load a movie into it. You'll be familiar with the QuickTime controller if you've ever viewed a QuickTime movie in a Web browser or in the QuickTime Player application. The controller lets users control the playback of QuickTime content using a set of familiar buttons. Besides starting and stopping playback, you can rewind and fast forward through portions of the movie as well as adjust the volume during playback. Figure 16-9 shows a typical QuickTime movie controller.
- **Editable:** By default, Editable has a value of `NO` (that is, it's deselected in the Inspector window). The QuickTime controller appears, as shown in Figure 16-9. When you set Editable to `YES` by selecting the Editable check box in the Inspector window of Interface Builder and then loading a movie in code, you see a controller that looks like Figure 16-10.

The Editable attribute causes a `QTMovieView` to display a slightly different QuickTime controller. You can use this type of controller for different purposes, such as to select some portion of the movie. As you can see in Figure 16-11, Shift-clicking permits you to select some or all the movie in the `QTMovieView`.

- **Volume:** Toggle the display of the volume button control that appears at the left edge of the `QTMovieView`. When you set this attribute to `YES` by clicking the Volume check box in the Inspector window, the volume button displays. When `NO` (deselected), the volume button doesn't display.

![](img/ea40cad434a338535474e82c1a6ace20_327_0.png)

Figure 16-9: The standard QuickTime controller offers simple playback interface elements.

![](img/ea40cad434a338535474e82c1a6ace20_328_0.png)

Figure 16-10:
The Editable attribute toggles between playback and editing interface elements.

![](img/ea40cad434a338535474e82c1a6ace20_328_1.png)

Figure 16-11:
Shift-click the controller to select some section of a movie in a QMovieView.

After you set the desired `QMovieView` attributes in Interface Builder, add some code to Xcode to play a movie. Assuming you’ve already loaded a movie into memory using the `QTMovie` class, display that movie in the `QMovieView`, by adding the following code:

```cpp
[moviePlayer setMovie:theMovie];
```

You can set many other aspects of playback using code. Besides the attributes that you found in Interface Builder, you can set the volume of the movie during playback. A volume of 1.0 is *full* volume, as defined by the maximum system volume level. Thus, a volume of 0.5 is half the maximum system volume level.

```
[*moviePlayer* setVolume:1.0];
```

Alternatively, if you prefer, you can mute the sound:

```
[*moviePlayer* setMuted:YES];
```

## Building a simple movie player

The easiest way to see how movie playback in Cocoa works is to build a player. Follow these steps:

1. Launch Xcode and create a new Cocoa application project by choosing File > New Project. Double-click the MainMenu.xib file in Xcode to open it with Interface Builder.
2. From the MainMenu.xib file window, open the main window for your interface and then open the Inspector for the window by choosing Tools > Inspector.
3. In the Inspector window, change the *Title* field for the window to something appropriate. Add a *QTMovieView* control and an *NSButton* from the controls from the Library window (as shown in Figure 16-12).

![](img/ea40cad434a338535474e82c1a6ace20_329_0.png)

4. Create a controller class for this interface.

Drag an NSObject from the Library window to the XIB project window. Press ⌘+6 and name the new object MyMovieController. Figure 16-13 shows the new class.

![](img/ea40cad434a338535474e82c1a6ace20_330_0.png)

5. Add an outlet and an action to the new controller class in the Inspector window.

Name the outlet moviePlayer and name the action loadMovie.

6. Connect the MyMovieController instance to the interface:

   - a. Control+drag from the new MyMovieController instance to the QTMovieView that you added to the window earlier.
   - b. Select the moviePlayer outlet in the black connections list overlay that appears.
   - c. Control+drag from the push button to MyMovieController and connect it to the loadMovie action.

7. After you design the interface, select the MyMovieController instance in the XIB project window and choose File⥫Write Class Files. Write the class files and add them to the Xcode project.

8. In Xcode, change the code in the MyMovieController.h interface file to look like this:

```objc
#import <Cocoa/Cocoa.h>

@interface MyMovieController : NSObject {
    IBOutlet id moviePlayer;
}
- (IBAction)loadMovie:(id)sender;
@end
```
