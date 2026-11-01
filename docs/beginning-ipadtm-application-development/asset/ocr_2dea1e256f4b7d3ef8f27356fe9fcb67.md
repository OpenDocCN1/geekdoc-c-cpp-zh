Note that this property merely specifies whether the user's location is displayed on the map (represented as a throbbing blue circle); it does not center the map to display the user's location. Hence, if you are viewing the map of another location, your current location indicator may not be visible on the map.

![](bbox=[0.1, 0.2, 0.82, 0.7])

FIGURE 18-3

Observe that as you can pinch the map to zoom it in or out. As you change the zoom level of the map, it is important that you keep track of this information so that when the user restarts the application you can display the map using the previous zoom level.

In the following Try It Out, you keep track of the map zoom level as the user changes the zoom level.

# TRY IT OUT Printing Out the Zoom Level of the Map

+   1. Using the MapKit project created in the previous section, edit the MapKitViewController.h file and add in the following bold statement:
+   
+   ```objc
+   #import <UIKit/UIKit.h>
+   
+   #import <MapKit/MapKit.h>
+   
+   @interface MapKitViewController : UIViewController
+   ```