orientations. We simply need to register to receive the notifications and then turn the notifications on. This is done in GSRootViewController's viewDidLoad method.

```
```
// Catch device orientation changes.
[[NSNotificationCenter defaultCenter]
 addObserverForName:UIDeviceOrientationDidChangeNotification
 object:[UIDevice currentDevice]
 queue:nil
 usingBlock:^(NSNotification *note) {
     UIDeviceOrientation orientation =
     [[UIDevice currentDevice] orientation];
     switch (orientation) {
         case UIDeviceOrientationLandscapeLeft:
         case UIDeviceOrientationLandscapeRight:
             self.bestSubviewOrientation = orientation;
             break;
         default:
             // Ignore anything else.
             break;
     }
 }];
[[UIDevice currentDevice]
    beginGeneratingDeviceOrientationNotifications];
```
```

Here, when we receive the orientation did change notification, we simply check to see if the current orientation is one of the two landscape modes. If it is, we assign it to our bestSubviewOrientation property. Otherwise, we ignore it. We can then use the bestSubviewOrientation to manually rotate our pop-up views as needed.