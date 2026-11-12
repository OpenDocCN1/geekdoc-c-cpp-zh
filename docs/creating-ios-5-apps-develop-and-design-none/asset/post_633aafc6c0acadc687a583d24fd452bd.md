
Once we determine the direction of the swipe, we use that information to set the animation type. Specifically, we select an animation sequence that will slide our view in from the side, making sure its motion follows the direction of our swipe.

Next, we check to see if our canvas view is currently paused. If it is, we simply return. We don't want to display any other pop-up views while our application is paused. Once this check is passed, we pause our canvas, grab a snapshot of our current drawing, and pass both the snapshot and our current best orientation to the export view. Finally, we display the pop-up view, using the showPopupController: animationType:withCompletionHandler: method we developed in the first part of this chapter.

Unlike what we did with the pause menu, we do not provide any code for dismissing the pop-up view and restarting the canvas here. Our export menu must handle those tasks when an export item is selected.

Now let's add the one-finger pan gesture for our acceleration control. Add the following code to our viewDidLoad method, after the code that creates our swipe gestures.

```objective-c
// Add 1-finger pan for acceleration.
UIPanGestureRecognizer* accelerationGesture =
    [[UIPanGestureRecognizer alloc]
        initWithTarget:self
        action:@selector(accelerationGesture:)];
accelerationGesture.maximumNumberOfTouches = 1;
// This can only succeed if we definitely don't have a swipe.
[accelerationGesture requireGestureRecognizerToFail:
    swipeToExportDown];
[accelerationGesture requireGestureRecognizerToFail:
    swipeToExportUp];
[self.view addGestureRecognizer:accelerationGesture];
```

Here, we create a pan gesture recognizer and then set it for a single touch. Next, we create a dependency between our pan recognizer and our swipe recognizers. Both swipe recognizers must fail before a pan gesture can be recognized.

Unlike the others, pans are continuous gestures. There is no difference when the recognizer is created, but we have to design our accelerationGesture: method to handle multiple calls. Not surprisingly, the method is more complicated than our previous examples. Let's step through it.

```objective-c
- (void)accelerationGesture:(UIGestureRecognizer *)gestureRecognizer {
    // Don't process acceleration gestures if paused.
    if (!self.canvasViewController.running) return;
    CGPoint motion =
        [(UIPanGestureRecognizer*)gestureRecognizer
            translationInView:self.view];
    [(UIPanGestureRecognizer*)gestureRecognizer
        setTranslation:CGPointZero inView:self.view];
}
```

Just like before, we check to see if the canvas view is running before we proceed. We don't show the acceleration control if the canvas is paused.

Then we calculate the distance that the user's finger has moved since the last update. UIPanGestureRecognizer has three methods to help track the pan gesture: translationInView:, velocityInView:, and setTranslation:inView:. translationInView: tracks the touch's change in position in the given view's coordinates. This is the cumulative distance moved—by default, it gives the offset from the gesture's starting position. Similarly, velocityInView: gives the gesture's current velocity using the given view's coordinate system. The velocity is broken into both vertical and horizontal components. Finally, setTranslation:inView: lets us reset the reference point for translationInView: and resets the velocity.

Since we're only concerned with the position, not the velocity, we only need to use translationInView:. However, we want the change in position for each update. To calculate this, we simply reset the translation by calling setTranslation:inView: and passing in CGPointZero—effectively assigning a new starting point for the next iteration.

```objective-c
// Update the value in the gesture recognizer screen.
CGFloat min = logf(0.05f);
CGFloat max = logf(10.0f);
CGFloat range = max - min;
CGFloat current =
    logf(self.canvasViewController.accelerationRate);
CGFloat change = motion.y;
// If we're landscape left, reverse the acceleration changes.
if (self.bestSubviewOrientation ==
    UIDeviceOrientationLandscapeRight) {
    change *= -1;
}
current += range / self.view.bounds.size.height * 4.0f / 3.0f *
           change;
if (current < min) current = min;
if (current > max) current = max;
self.canvasViewController.accelerationRate = expf(current);
[self.accelerationController.progressBar
    setProgress:(current - min) / range
    animated:YES];
```

Next, we calculate the acceleration value. We will use this value to scale the results from Core Motion in the next section. The larger the value, the more quickly the cursor responds when tilting the phone. Here, we're going to scale the value from 0.05 to 10.0. The exact math isn't too important. However, there are two points worth noting. First, a linear change in the gesture's location results in an exponential change in the cursor's responsiveness. Second, we've set the scale so that you only need to pan three-quarters of the way across the screen to go from the lowest setting to the highest.

Once the acceleration value is calculated, we assign it. We set the canvas's accelerationRate property to the exponential value. However, we use the linear value to set our acceleration control's progress bar. This means that the minimum value will correspond to 0.0f on the progress bar (a completely empty bar), while the maximum value will correspond to 1.0f (a completely filled bar).

```swift
    switch (gestureRecognizer.state) {
        case UIGestureRecognizerStateBegan:
            [self showPopupController:self.accelerationController
                        animationType:GSPopupFade
                        withCompletionHandler:nil];
            break;
        case UIGestureRecognizerStateChanged:
            // Do nothing.
            break;
        case UIGestureRecognizerStateEnded:
            [self hidePopupController:self.accelerationController
                        animationType:GSPopupFade];
            break;
        case UIGestureRecognizerStateCancelled:
            NSLog(@"Acceleration Gesture Canceled");
            break;
        case UIGestureRecognizerStateFailed:
            NSLog(@"Acceleration Gesture Failed");
            break;
        case UIGestureRecognizerStatePossible:
            NSLog(@"Acceleration Gesture Possible");
            break;
    }
}
```

Finally, we check and respond to the gesture recognizer's state. Since this is a continuous recognizer, we're really only worried about the ...Began, ...Changed, and ...Ended states. We're already recalculating the acceleration values for each update. So, all we really need to do here is display our acceleration view in the ...Began state, and hide it in the ...Ended state. We don't pause the canvas, since the user might want to see how the cursor's behavior changes as they adjust the cursor acceleration.

## CORE MOTION

The gestures give us access to all our ancillary controls, but we still haven't dealt with our device's main control; we want the user to steer the cursor by tipping and tilting their device. To do this, we must dig into the Core Motion framework.

Core Motion lets us access data from a variety of sensors on the device. The `CMMotionManager` class acts as the gateway to all our motion data. It provides access to our device's accelerometer, gyroscopes, and magnetometer, as well as the processed device motion data.

Device motion combines data from all the sensors using a sensor fusion algorithm. This produces more accurate motion estimates but comes at a somewhat higher computational cost. Device motion also provides some features that individual sensors cannot perform on their own. For example, it automatically separates acceleration from the device's motion, and acceleration from gravity.

Unfortunately, not all devices have the same set of sensors. In particular, iPhone 4 and iPad 2 both have access to all the sensors. iPhone 3GS and the original iPad only have the accelerometer and the magnetometer. The 4th generation iPod touch has both the accelerometer and gyroscopes, but no magnetometer. The 3rd generation iPod touch only has the accelerometer. And the simulator doesn't support any of these sensors. Fortunately, Core Motion provides methods to check and make sure a feature is supported before you attempt to use it.

> **NOTE:** Device motion is only available on devices that have both the accelerometer and the gyroscopes. If you have a magnetometer, that will be used to improve accuracy, but it is not necessary. Unfortunately, this means the iPhone 3GS, the original iPad, and the 3rd generation iPod touch do not support device motion.

![](img/fe9fea534a8e7868f811f7cd33da015f_501_0.png)

Core Motion also provides both push and pull approaches to accessing the data. In the push approach, Core Motion runs on its own operation queue. We set the interval, and we provide a block of code to execute. Core Motion will then sample the sensors and call this block at every interval.

In the pull approach, Core Motion updates the motion data in the background, and we sample it whenever we need to. In general, the pull approach is recommended for most applications. It is more efficient and typically requires less code. The push data should only be used for applications that focus on data collection, where we want to make sure we don't accidentally miss any samples.
