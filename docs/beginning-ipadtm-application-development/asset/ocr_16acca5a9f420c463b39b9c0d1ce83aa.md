4. Press Command-R to test the application on the iPhone Simulator. Observe the map displaying the location reported by the location manager (see Figure 18-9). The center of the map is the location reported.

![](bbox=[0.11, 0.2, 0.88, 0.64])

FIGURE 18-9

> **NOTE** If you test the application on an iPad, you will see that the map updates itself dynamically when you move about.

# How It Works

To use the Map Kit in your application, you first need to add the MapKit.framework to your project.

Then, you implement the MKMapViewDelegate protocol in the View Controller to handle the various methods associated with the MapView:

```
@interface LBSViewController : UIViewController
<CLLocationManagerDelegate,
MKMapViewDelegate> {
```