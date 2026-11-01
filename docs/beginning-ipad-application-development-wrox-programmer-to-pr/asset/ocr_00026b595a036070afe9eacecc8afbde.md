The didReceiveMemoryWarning method will be called whenever your iPad runs out of memory. You should insert code in this method so that you can free resources/objects that you do not need.

In addition, you should also handle the applicationDidReceiveMemoryWarning: method in your application delegate:

```
```objc
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application {
    //---insert code here to free unused objects---
    [[ImageCache sharedImageCache] removeAllImagesInMemory];
}
```
```

In this method, you should stop all memory-intensive activities, such as audio and video playback. You should also remove all images cached in memory.

# PROTOCOLS

In Objective-C, a protocol declares a programmatic interface that any class can choose to implement. A protocol declares a set of methods, and an adopting class may choose to implement one or more of its declared methods. The class that defines the protocol is expected to call the methods in the protocols that are implemented by the adopting class.

The easiest way to understand protocols is to examine the UIAlertView class. As you have experienced in the various chapters in this book, you can simply use the UIAlertView class by creating an instance of it and then calling its show method:

```
```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
[alert show];
```
```

The preceding code displays an alert view with one button — OK. Tapping the OK button automatically dismisses the alert view. If you want to display additional buttons, you can set the otherButtonTitles: parameter like this:

```
```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:@"Option 1", @"Option 2", nil];
```
```

The alert view now displays three buttons — OK, Option 1, and Option 2. But how do you know which button was tapped by the user? You can determine this by handling the relevant method(s) that will be fired by the alert view when the buttons are clicked. This set of methods is defined by the UIAlertViewDelegate protocol. This protocol defines the following methods:

+   - alertView:clickedButtonAtIndex:
+   - willPresentAlertView: