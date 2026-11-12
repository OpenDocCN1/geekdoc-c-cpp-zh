In the second part of the addAcceleration: method, we check to make sure our cursor remains within the screen's bounds. If either the x- or y-component is out of bounds, we set it to the screen's edge and reverse the velocity along that axis. We also reduce the velocity by half. This gives our cursor a nice little bounce when it hits the edge of the screen.

Finally, we assign our new velocity and return the updated cursor location. Now we just need a method to turn off motion updates.

```
```objc
- (void)stopGravityUpdates {
    // Turn off gravity updates.
    if (self.motionManager.deviceMotionAvailable) {
        [self.motionManager stopDeviceMotionUpdates];
    }
    else {
        [self.motionManager stopAccelerometerUpdates];
    }
}
```
```

Here, we just check to see which type of motion updates we're using and then stop the appropriate one.

# ## DEVICE ORIENTATION

As mentioned earlier, we keep our canvas view locked in portrait orientation. There are a couple of reasons for this. First, it's easier. As we just saw, our gravity vector comes in the device's reference frame. Keeping the view orientation constant makes it easy to translate our gravity coordinates to the view coordinates; we just need to invert our y-coordinate. However, if we allowed the view to rotate to different orientations, we would have to convert the gravity coordinates separately for each orientation.

The biggest problem, however, is simply usability. The user will be tilting and tipping their phone as they steer the cursor about the screen. We don't want to accidentally rotate the view just because they tilted the phone too far in one direction or another.