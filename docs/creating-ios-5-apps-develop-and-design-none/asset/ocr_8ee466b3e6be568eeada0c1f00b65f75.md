Once this is in place, we check to see if our device supports device motion. If it does, we set the device motion update interval to 60 updates per second. If not, we will just have to use the accelerometer alone, so we set its update interval instead.

Finally, we ensure that our operation queue will only execute one operation at a time—essentially making it a serial operation queue.

Next, let's add a method to start motion updates. We'll take this method in steps.

```
```
#pragma mark - Gravity Updates

- (void) startGravityUpdates {
    if (self.motionManager.deviceMotionAvailable) {
        [self.motionManager
         startDeviceMotionUpdatesToQueue:self.updateQueue
         withHandler:^(CMDeviceMotion *motion, NSError *error) {
             CGPoint location =
             [self addAcceleration:motion.gravity];
             [self.canvas addLineToPoint:location];
             dispatch_async(dispatch_get_main_queue(), ^{
                 [self.canvas updateCanvasUI];
             });
         }];
         }
     }
```
```

Here we check to see if the device supports device motion. If it does, we start the motion updates.

Here we're primarily interested in the acceleration data. Typically, accelerometers register both the pull of gravity as well as the actual acceleration of the device. Often, we need to separate these two signals, using a low-pass filter to focus on the pull of gravity, and a high-pass filter for device motion. Fortunately, the device motion sensor fusion algorithm uses additional information from the gyros and (if present) the magnetometer to automatically separate the device's total acceleration into its gravity and user acceleration components.

Here, we simply grab the gravity vector (the direction of gravity given the phone's reference frame) and pass it to our addAcceleration: method. Then we update the