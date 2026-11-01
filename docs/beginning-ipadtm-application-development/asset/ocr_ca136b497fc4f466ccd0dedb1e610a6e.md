# TRY IT OUT Incorporating a Compass

You will need a real device (iPad) to test this application.

+   1. Using the LBS project, add an image named Compass.gif to the Resources folder of the project (see Figure 18-10).
+   2. In Interface Builder, drag and drop an ImageView to the View window and set its attributes in the Attributes Inspector window as follows (see also Figure 18-11):
+      - Image — Compass.gif
+      - Mode — Aspect Fit
+   3. Add a Label view to the View window (see Figure 18-12).
+   4. In the LBSViewController.h file, add the following bold statements:

![](bbox=[0.12, 0.26, 0.72, 0.7])

```
#import <UIKit/UIKit.h>
#import <CoreLocation/CoreLocation.h>
#import <MapKit/MapKit.h>

@interface LBSViewController : UIViewController
<CLLocationManagerDelegate,
```