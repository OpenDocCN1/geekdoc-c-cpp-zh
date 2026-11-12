
The Settings.bundle property files can get quite complex. Check out Apple’s documentation for all the sticky details. In particular, I recommend looking over the Settings Application Schema Reference and reading “Creating and Modifying the Settings Bundle” in the Preferences and Settings Programming Guide.

Run the application again. From the enter weight screen, set the Units value to kilograms. Now put the app in the background and open the Settings app. Navigate to the Health Beat settings. Change the weight back to pounds. Move back to the Health Beat application. The units should have automatically changed to match the value in our Settings app.

There’s only one last thread to tie up. We’ve already registered an undo action every time we add or delete a weight entry. Now we need to finish setting up our undo support.

```objective-c
NSString* message = @"There are no changes that "
                  @"can be undone at this time.";
UIAlertView* alert = [[UIAlertView alloc]
                      initWithTitle:title
                      message:message
                      delegate:nil
                      cancelButtonTitle:@"OK"
                      otherButtonTitles:nil];
[alert show];
[alert release];
}
}
```

iOS typically uses the shake gesture to trigger undo commands; however, it’s very easy to accidentally trigger shake gestures. Therefore, we should have the user confirm the undo command before we actually perform it.

This method handles that for us. If we have an undo action available, it creates an alert message using the action name. Otherwise, it displays a message letting the user know that it cannot undo anything at this time.

Note that our code doesn’t actually do anything until the user taps the Undo button. We catch this in the alertView:didDismissWithButtonIndex: method.

```objective-c
#pragma mark - alert view delegate methods
- (void)alertView:(UIAlertView *)alertView
didDismissWithButtonIndex:(NSInteger)buttonIndex {
    // Undo the last action if it is confirmed.
    if (buttonIndex == 1) {
        [self.undoManager undo];
    }
}
```

If the user dismisses an alert view by tapping the second button (which we have previously defined as the Undo button), then we call our undo manager's undo method. That will trigger the undo action currently at the top of the stack.

Finally, we can improve our application's memory management by clearing out the undo stack if we receive a memory warning. Simply implement the applicationDidReceiveMemoryWarning: method.

```objective-c
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application {
    // Clear the undo manager.
    [self.undoManager removeAllActions];
}
```

Now, let's modify the HistoryViewController so that it responds to the shake gesture. When this gesture occurs, we'll undo our last action. Fortunately, UIResponder provides support for motion events using the motionBegan:withEvent:, motionEnded:withEvent:, and motionCanceled:withEvent: methods. Our HistoryViewController, as a UIResponder subclass, inherits these methods.

In general, I prefer to respond to shake events in the motionEnded:withEvent: method. This will occur after the user stops shaking the device—provided the shaking motion was sufficient to trigger an event. This helps prevent accidental shakes. Implement the method as shown:

```objective-c
#pragma mark - Responder Events

- (void)motionEnded:(UIEventSubtype)motion
        withEvent:(UIEvent *)event {
    // Only respond to shake events.
    if (event.type == UIEventSubtypeMotionShake) {
        [self.undoManager undo];
    }
}
```

Here, we check to make sure we have a motion shake event, and then we trigger our document's undo method. Currently, UIEventSubtypeMotionShake is iOS's only motion event, so the check doesn't actually do anything. Still, it helps future-proof our code. Apple may add new motion events to future releases.

This seems too simple to be true, and it is. Run the app, add a new weight entry, and then after it navigates to the history view, shake your phone. Nothing happens. It turns out that motion events are only sent to the first responder. So, we just need to set our controller as the first responder.

First, we have to tell the system that our controller can become first responder, by overriding the canBecomeFirstResponder method. Here, we just need to return YES.

```
- (BOOL)canBecomeFirstResponder {
    return YES;
}
```

Next, we need to set our controller as the first responder when the history view appears and release the first responder when it disappears. We can do this in our viewDidAppear: and viewWillDisappear: methods.

```
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    [self becomeFirstResponder];
}
- (void)viewWillDisappear:(BOOL)animated
{
    [super viewWillDisappear:animated];
    [self resignFirstResponder];
}
```

That's it. Run the application. Try adding and deleting weights. Navigate to the history view and shake to undo. Everything should work as expected. Don't forget to commit all your changes.

## WRAPPING UP

We’ve covered a lot of important ground in this chapter. iCloud is, without a doubt, one of the most important new features in iOS 5. As you’ve seen, it is also somewhat complicated to implement correctly. In this chapter, we covered the steps needed to implement a UIDocument subclass. We looked at techniques for creating new documents and opening existing documents. We also modified our application to respond to notifications from our document and to merge any conflicts as they arise. We added undo support and autosaving. And we synced our user preferences using iCloud key-value storage.

Our Health Beat application is now functionally complete. We can add and remove weight entries. These entries are saved and synced to all our devices. We can view our history and graph our progress. While the application can undoubtedly be improved, there are no major pieces left to implement.

Next chapter, we will take a step back and replace our application’s model with Core Data. As you will see, UIManagedDocument and the Core Data model automatically handle many tedious document management tasks for us.

题目：已知点 A(-2, 1), B(3, 2)，若直线 l 的倾斜角是直线 AB 的倾斜角的 2 倍，则直线 l 的斜率为 ____。

过点 P(1, 1) 作直线 l 与两坐标轴围成的三角形面积为 2，这样的直线 l 可作 ____ 条。

已知直线 l 的倾斜角为 60°，在 y 轴上的截距为 -2，则直线 l 的方程为 ____。

## INTRODUCING CORE DATA

The Core Data framework provides support for automatically managing many common model layer tasks. We have already seen how Xcode simplifies our application’s view layer. With Interface Builder, we can draw our application’s scenes. The built-in guidelines ensure that our application follows Apple’s Human Interface Guidelines, but it goes beyond that. We can draw connections between our view and controllers, linking objects to outlets and events to actions. With storyboards, we can link scenes with segues, letting us rapidly sketch out the entire application’s workflow. With a few clicks of the mouse, Xcode helps us build complex structures that would normally require a considerable amount of boilerplate code.

Core Data brings a similar magic to our model. For most applications, the models share a number of features. This includes one or more object graphs. These graphs define both the content and the relationships in our application’s data. Applications need to manage the life cycles of these object graphs, adding, modifying, and deleting objects in the graphs. They also need to validate the graphs, and save and load them to disk. Undo and redo support would also be nice. Furthermore, if the format of our data changes, we need to migrate our saved data from one schema to the next.

Core Data provides all of these features and more. In many cases, it can perform these tasks automatically. In others, it presents a rich API for expanding and customizing its behavior. It is also tightly integrated with Xcode’s tool chain. Core Data is mature, well tested, and highly optimized. It is used by millions of customers across thousands of applications. While we could try to build a custom solution to better fit our specific needs, it would require a considerable amount of effort to match the performance and stability already provided by Core Data. In most cases, it’s more cost effective to just use Core Data and to focus the developer effort on other areas.

And, yes, we can even graphically lay out our object graphs.

This chapter will start with a quick overview of Core Data’s architecture, to give you an idea of how it works and how you might use it for other projects. Then we will convert our Health Beat application over from a custom model to Core Data. Along the way, we will look at many of the tricks and tips (and possible traps) involved in using Core Data.
