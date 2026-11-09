The ActivityMonitorDelegate protocol has two required methods, so we have to stub them out in IconViewController.m:

```
Download `CustomView/HelloApplication22/IconViewController.m`

#import "IconViewController.h"

@implementation IconViewController

- (void) applicationDidLaunch: (NSRunningApplication *) app {}
- (void) applicationDidTerminate: (NSRunningApplication *) app {}

@end
```

Now, here’s the part that’s different.

We’re going to create a custom class for the view. Create a new class of type NSView, and name it IconView.¹ We’ll spend much of this chapter working with the IconView class, but first let’s set up the infrastructure around it.

In IconView.xib, use the Identity inspector to change the File’s Owner’s class to IconViewController and the view’s class to IconView. Use the Connections inspector to connect the IconViewController’s view outlet to the IconView. Also use the Size inspector to set the IconView’s width to be 216 and height to be 240. Save your work, and quit IB.

![](bbox=[0.14, 0.53, 0.773, 0.658])

![](bbox=[0.14, 0.752, 0.773, 0.778])

We also need to change MyWindowController to create an IconViewController and load the IconView nib. In the MyWindowController header file, we can just change all of the instances of ActivityController to IconViewController.

+   1. Select the Objective-C class template, and use the drop-down list to find the NSView option.