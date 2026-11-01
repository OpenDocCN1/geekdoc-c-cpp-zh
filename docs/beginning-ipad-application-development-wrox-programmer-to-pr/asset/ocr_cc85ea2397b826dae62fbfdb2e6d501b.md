# TRY IT OUT Getting Started with Map Kit

*codefile MapKit.zip available for download at Wrox.com*

+   1. Using Xcode, create a View-based Application project and name it MapKit.
+   2. Add the MapKit.framework framework to the Frameworks folder of the project (see Figure 18-1).

![](bbox=[0.12, 0.32, 0.8, 0.7])

FIGURE 18-1

+   3. Double-click the MapKitViewController.xib file to edit it in Interface Builder.
+   4. Populate the View window with the following views (see Figure 18-2):
+      - MapView
+      - Round Rect Button (label it as Show My Location)
+   5. In the MapKitViewController.h file, add in the following bold statements:

```
#import <UIKit/UIKit.h>

#import <MapKit/MapKit.h>

@interface MapKitViewController : UIViewController {
```