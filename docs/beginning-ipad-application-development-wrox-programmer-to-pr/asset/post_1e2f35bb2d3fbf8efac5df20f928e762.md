
```
//---calculate how much visible space is left---
CGFloat freeSpaceHeight =
applicationFrame.size.height - keyboardBounds.size.height;

//---calculate how much the scrollView must scroll---
CGFloat scrollAmount = viewCenterY - freeSpaceHeight / 2.0;

if (scrollAmount < 0) scrollAmount = 0;

//---set the new scrollView contentSize---
scrollView.contentSize = CGSizeMake(applicationFrame.size.width,
applicationFrame.size.height +
keyboardBounds.size.height);

//---scroll the ScrollView---
[scrollView setContentOffset:CGPointMake(0, scrollAmount)
animated:YES];
}
```

When the TextField view resigns its First Responder status, the `textFieldDidEndEditing:` method will be invoked. At this point, you restore the ScrollView view to its original content size:

```
//---when a TextField view is done editing---
-(void) textFieldDidEndEditing:(UITextField *) textFieldView {
[UIView beginAnimations:@"back to original size" context:nil];
scrollView.contentSize = scrollViewOriginalSize;
[UIView commitAnimations];
}
```

A noteworthy point here is that you use the `beginAnimations` method of the `UIView` class to animate the ScrollView view in the process of restoring to its original size. If you do not use this method, the ScrollView will very abruptly restore to its original size, causing a flicker.

Just before the keyboard disappears, the `keyboardWillHide:` method is invoked. In this case, you don't have much to do:

```
//---when the keyboard disappears---
-(void) keyboardWillHide:(NSNotification *) notification {
}
```

Finally, in the `dealloc` method, you release all the outlets you have created:

```
-(void) dealloc {
[textField release];
[scrollView release];
[super dealloc];
}
```

![](img/744c5ec15e15ca7891c98be71dc25d13_205_0.png)

FIGURE 6-3

## How It Works

By default, the iPad application project you created using Xcode supports all orientations — portrait as well as landscape modes. This is evident in the ScreenRotationsViewController.m file, where you have the shouldAutorotateToInterfaceOrientation: method:

```objc
- (BOOL)shouldAutorotateToInterfaceOrientation:
(UIInterfaceOrientation)interfaceOrientation {
    return YES;
}
```

> NOTE On the iPad, screen rotation is automatically handled by the OS. When the OS detects a change in screen orientation, it fires the shouldAutorotateToInterfaceOrientation: event; it is up to the developer to decide how the application should display in the target orientation.

The shouldAutorotateToInterfaceOrientation: method is called when the View is loaded and when orientation of the device changes. This method passes in a single parameter — the orientation that the device has been changed to. The returning value of this event determines whether the current orientation is supported. By default, your iPad application supports all screen orientations, hence it simply returns a YES.

This means that your application will rotate to all orientations (the status bar will always appear at the top) when the device is rotated.

To support specific orientations, simply perform an equality check to specify the orientation supported. For example, the following code snippet shows that only the landscape left orientation is supported.

```
- (BOOL)shouldAutorotateToInterfaceOrientation:
(UIInterfaceOrientation)interfaceOrientation {
    //return YES;
    return (interfaceOrientation ==
        UIInterfaceOrientationLandscapeLeft);
}
```

This means that your application will display upright only in landscape mode with the Home button on its left (hence the constant name UIInterfaceOrientationLandscapeLeft).

If the user rotates the device to portrait mode or landscape mode with the Home button on the right (UIInterfaceOrientationLandscapeRight), the application will not change its orientation.

While you can specify the orientation supported by your application, Apple has specifically indicated that your application should support all screen orientations.

> **NOTE** Here is one easy way to differentiate between UIInterfaceOrientationLandscapeLeft and UIInterfaceOrientationLandscapeRight. Just remember that UIInterfaceOrientationLandscapeLeft refers to the Home button positioned on the left and UIInterfaceOrientationLandscapeRight refers to the Home button positioned on the right.

### Different Types of Screen Orientations

You have a total of four constants to use for specifying screen orientations:

- UIInterfaceOrientationPortrait — Displays the screen in portrait mode
- UIInterfaceOrientationPortraitUpsideDown — Displays the screen in portrait mode but with the Home button at the top of the screen
- UIInterfaceOrientationLandscapeLeft — Displays the screen in landscape mode with the Home button on the left
- UIInterfaceOrientationLandscapeRight — Displays the screen in landscape mode with the Home button on the right

### willAnimateSecondHalfOfRotationFromInterfaceOrientation:

The willAnimateSecondHalfOfRotationFromInterfaceOrientation: event is fired when the rotation is halfway through. The method looks like this:

```
- (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:
(UIInterfaceOrientation) fromInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

The fromInterfaceOrientation parameter indicates the orientation that it is changing from, whereas the duration parameter indicates the duration of the second half of the rotation, in seconds.

In this event, you typically perform tasks such as repositioning the views on the View, resuming media playback, and so on.

### willRotateToInterfaceOrientation:

The previous two events are fired consecutively — first the willAnimateFirstHalfOfRotationToInterfaceOrientation:, followed by the willAnimateSecondHalfOfRotationFromInterfaceOrientation: event. If you do not need two separate events for handling rotation, you can use the simpler willRotateToInterfaceOrientation: event.

The willRotateToInterfaceOrientation: event is fired before the orientation starts. In contrast to the previous two events, this is a one-step process. Note that if you handle this event, the willAnimateFirstHalfOfRotationToInterfaceOrientation: and willAnimateSecondHalfOfRotationFromInterfaceOrientation: events will still be fired.

The method looks like this:

```
- (void)willRotateToInterfaceOrientation:
(UIInterfaceOrientation) toInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

The toInterfaceOrientation parameter indicates the orientation that it is changing to, and the duration parameter indicates the duration of the rotation, in seconds.

### willAnimateRotationToInterfaceOrientation:

The willAnimateRotationToInterfaceOrientation: event is fired before the animation of the rotation starts.

> **NOTE** If you handle both the willRotateToInterfaceOrientation: and willAnimateRotationToInterfaceOrientation: events, the former will fire first, followed by the latter.

The method looks like this:

```objective-c
- (void)willAnimateRotationToInterfaceOrientation:
(UIInterfaceOrientation) interfaceOrientation
duration: (NSTimeInterval) duration {

}
```

The interfaceOrientation parameter specifies the target orientation to which it is rotating.

> **NOTE** If you handle this event, the willAnimateFirstHalfOfRotationToInterfaceOrientation: and willAnimateSecondHalfOfRotationFromInterfaceOrientation: events will not fire anymore.

In the following Try It Out, you will reposition the views on your user interface (UI) when the device changes orientation.

### **TRY IT OUT** Repositioning Views during Orientation Change

1. Using the project created earlier, double-click the ScreenRotationsViewController.xib file and add a Round Rect Button view to the View (see Figure 6-4).

![](img/744c5ec15e15ca7891c98be71dc25d13_209_0.png)
