
![](img/16991b58db5894715c4a443315e06a22_178_0.png)

FIGURE 6-6

The fromInterfaceOrientation parameter indicates the orientation that it is changing from, whereas the duration parameter indicates the duration of the second half of the rotation, in seconds.

In this event, you typically perform tasks when the rotation is halfway done, such as repositioning the views on the View, resuming media playback, and so on.

### willRotateToInterfaceOrientation:

The previous two events are fired consecutively — first the willAnimateFirstHalfOfRotationToInterfaceOrientation: is fired, followed by the willAnimateSecondHalfOfRotationFromInterfaceOrientation event. If you do not need two separate events for handling rotation, you can use the simpler willRotateToInterfaceOrientation: event.

The willRotateToInterfaceOrientation: event is fired before the orientation starts. In contrast to the previous two events, this is a one-step process. Note that if you handle this event, the willAnimateFirstHalfOfRotationToInterfaceOrientation: and willAnimateSecondHalfOfRotationFromInterfaceOrientation: events will not be fired anymore.

The method looks like this:

```
- (void)willRotateToInterfaceOrientation:
(UIInterfaceOrientation) toInterfaceOrientation
 duration: (NSTimeInterval) duration {

}
```

The toInterfaceOrientation parameter indicates the orientation that it is changing to, and the duration parameter indicates the duration of the rotation, in seconds.

![](img/16991b58db5894715c4a443315e06a22_180_0.png)

FIGURE 6-7

2. Observe its size and positioning by viewing the Size Inspector window. Here, its position is (20,20) and its size is 280 by 37 pixels.
3. Rotate the orientation of the View by clicking the arrow icon on the upper-right corner of the window (see Figure 6-8).
4. Reposition the Round Rect Button view by relocating it to the bottom-right corner of the View window (see Figure 6-9). Also observe and record its position.

![](img/16991b58db5894715c4a443315e06a22_180_1.png)

FIGURE 6-8

![](img/16991b58db5894715c4a443315e06a22_180_2.png)

FIGURE 6-9

5. In the ScreenRotationsViewController.xib window, select the File's Owner item and create an outlet named btn (of type UIButton) in the Identity Inspector window (see Figure 6-10).

![](img/16991b58db5894715c4a443315e06a22_181_0.png)

FIGURE 6-10

6. Connect the outlet you have created by control-clicking the File's Owner item and dragging over to the Round Rect Button view (see Figure 6-11). Select btn.

![](img/16991b58db5894715c4a443315e06a22_181_1.png)

FIGURE 6-11

7. Save the project in Interface Builder.

8. Back in Xcode, insert the following code into the ScreenRotationsViewController.h file:

    ```
    #import <UIKit/UIKit.h>
    
    @interface ScreenRotationsViewController : UIViewController {
        IBOutlet UIButton *btn;
    }
    @property (nonatomic, retain) UIButton *btn;
    @end
    ```

9. In the ScreenRotationsViewController.m file, add the following code:

    ```
    @implementation ScreenRotationsViewController
    
    @synthesize btn;
    
    ...
    - (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:
    (UIInterfaceOrientation) fromInterfaceOrientation
     duration: (NSTimeInterval) duration {
        UIInterfaceOrientation destOrientation = self.interfaceOrientation;
        if (destOrientation == UIInterfaceOrientationPortrait)
        {
            //---if rotating to portrait mode---
            btn.frame = CGRectMake(20,20,280,37);
        }
        else
        {
            //---if rotating to landscape mode---
            btn.frame = CGRectMake(180,243,280,37);
        }
    }
    - (void)dealloc {
        [btn release];
        [super dealloc];
    }
    ```

10. Save the project and press Command-R in Xcode to deploy the application onto the iPhone Simulator.

11. Observe that when the iPhone Simulator is in portrait mode, the Round Rect Button view is displayed in the top-left corner. But when you change the orientation to landscape mode, it is repositioned to the bottom-right corner (see Figure 6-12).

It's interesting to note that the setOrientation: method described in the previous section cannot be used to change the orientation of the View during loading time:

```
//---does not work during View loading time--
[[UIDevice currentDevice] setOrientation:UIInterfaceOrientationLandscapeLeft];
```

Likewise, setting the orientation of the status bar does not work during runtime (after the View has loaded):

```
//---does not work during run time--
[UIApplication sharedApplication].statusBarOrientation = 
UIInterfaceOrientationLandscapeLeft;
```

> NOTE The orientation to which you are changing must first of all be specified in the shouldAutorotateToInterfaceOrientation: event. This can also be specified in the info.plist file for the application by setting the InitialInterfaceOrientation key to the desired orientation.

### SUMMARY

In this chapter, you have seen how changes in screen orientations are handled by the various events in the view controller class. Proper handling of screen orientations will make your application more useable and improve the user experience.

### EXERCISES

1. Suppose you want your application to only support the landscape right and landscape left orientation. How should you modify your code?
2. What is the difference between the frame and center property of a view?

## PART II: Building Different Types of iPhone Applications

- **CHAPTER 7:** View Controllers
- **CHAPTER 8:** Tab Bar and Navigation Applications
- **CHAPTER 9:** Utility Applications

![](img/16991b58db5894715c4a443315e06a22_188_0.png)

![](img/16991b58db5894715c4a443315e06a22_190_0.png)

## View Controllers

### WHAT YOU WILL LEARN IN THIS CHAPTER

- How to create a Window-based Application and manually add a View Controller and a View window to it
- How to create views dynamically during runtime
- How to wire up events of views with event handlers via code
- How to switch to another view during runtime
- How to animate the switching of views

Until this point, you have been dealing with single view applications; that is, applications with a single View Controller. The previous chapters have all been using the View-based Application template available in the iPhone SDK because it is the simplest way to get started in iPhone programming. When you create a View-based application, there is by default one View Controller (named `<project_name>ViewController` by the iPhone SDK). In real-life applications, you often need more than one View Controller, with each controlling a different view displaying different information. A good example of a multiview application is the Weather application shipped with the iPhone. The main view shows the weather of a region you have selected, and you can swipe the screen to view the weather of other locations. You can also press the i icon to flip to another view and add locations.

This chapter teaches you how to create multiple views in your application and then programmatically switch among them during runtime. In addition, you learn how to animate the switching of views using the built-in animation methods available in the iPhone SDK.

### CREATING A WINDOW-BASED APPLICATION

In this section, you discover another type of application template you can create using the iPhone SDK: the Window-based Application template. Unlike the View-based Application template, the Window-based Application template does not include a View Controller by default. Instead, it provides only the skeleton of an iPhone application and leaves the rest to the developer — you need to add your own views and View Controllers. Because of this, a Window-based Application presents a very good way for you to understand how View Controllers work and appreciate all the work needed to connect the View Controllers and XIB files. When you understand how View Controllers work, you will be on your way to creating multiview applications.

To put first things first, execute the following Try it Out to write a Window-based Application and then progressively add a View Controller to it. You will need to download the project files as indicated here for this and other Try It Out features in this chapter.

### TRY IT OUT  Adding a View Controller Using Interface Builder

*Codefile [WinBasedApp.zip] available for download on Wrox.com*

1. Using Xcode, create a Window-based Application project and name it `WinBasedApp`. Observe the files created for this project type (see Figure 7-1). Apart from the other, usual supporting file, note that there is only one XIB file (`MainWindow.xib`) and two delegate files (`WinBasedAppAppDelegate.h` and `WinBasedAppAppDelegate.m`).
2. Press Command-R to test the application, and you will realize that an empty screen is displayed on the iPhone Simulator. This is because the Window-based Application template provides only the skeleton structure for a simple iPhone application containing just a window and the application delegate.
3. Back in Xcode, double-click `MainWindow.xib` to edit it in Interface Builder. Observe that there are four items in the `MainWindow.xib` window (see Figure 7-2):
   - File's Owner
   - First Responder
   - Win Based App App Delegate
   - Window
