
When directional information is available, the locationManager:didUpdateHeading: method will continually fire:

```
- (void)locationManager:(CLLocationManager *)manager didUpdateHeading:(CLHeading *)newHeading {
    heading.text = [NSString stringWithFormat:@"%f degrees", newHeading.magneticHeading];
    
    //---heading is in degrees---
    double d = newHeading.magneticHeading;
    
    //---convert degrees to radians---
    double radians = d/57.2957795;
    compass.transform = CGAffineTransformMakeRotation(-radians);
}
```

The magneticHeading property of the CLHeading parameter will contain the readings in degrees, with 0 representing magnetic North. The ImageView is then rotated based on the value of the heading. Note that you need to convert the degrees into radians for the CGAffineTransformMakeRotation() method.

## Rotating the Map

The previous section showed how you can programmatically rotate the image of a compass based on the directional heading information you obtained from the Core Location framework. Using this concept, you could also rotate the map whenever the direction of your device changes. This is very useful when you are using the map for navigational purposes. By itself, the MapView does not support map rotation, but the following Try It Out shows how you can improvise.

### TRY IT OUT Rotating the Map

- 1. Using the LBS project, double-click the LBSViewController.xib file to edit it in Interface Builder.
- 2. Drag and drop a View view from the Library and set its size and location via its Size Inspector window as follows (see also Figure 18-14):
  - X:10
  - Y:60
  - W:720
  - H:678
- 3. In the Attributes Inspector window for the View, check the Clip Subviews option (see Figure 18-15).

### FIGURE 18-14

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_498_0.png)

### FIGURE 18-15

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_498_1.png)

- 4. In Xcode, add the following bold statements to the LBSViewController.h file:

```
#import <UIKit/UIKit.h>
#import <CoreLocation/CoreLocation.h>
#import <MapKit/MapKit.h>
#import "MyAnnotation.h"
#import <MapKit/MKReverseGeocoder.h>

@interface LBSViewController : UIViewController <CLLocationManagerDelegate,
MKMapViewDelegate,
MKReverseGeocoderDelegate> {
IBOutlet UITextField *accuracyTextField;
IBOutlet UITextField *latitudeTextField;
IBOutlet UITextField *longitudeTextField;
CLLocationManager *lm;

MKMapView *mapView;

IBOutlet UIImageView *compass;
IBOutlet UILabel *heading;

MyAnnotation *annotation;

NSString *location;
MKReverseGeocoder *geocoder;

}
IBOutlet UIView *viewForMap;

@property (retain, nonatomic) CLLocationManager *lm;
@property (retain, nonatomic) UITextField *accuracyTextField;
@property (retain, nonatomic) UITextField *latitudeTextField;
@property (retain, nonatomic) UITextField *longitudeTextField;

@property (nonatomic, retain) UIImageView *compass;
@property (nonatomic, retain) UILabel *heading;

@property (nonatomic, retain) IBOutlet UIView *viewForMap;

@end
```

- 5. In Interface Builder, Control-click and drag the File's Owner item and drop it over the newly added View view. Select viewForMap.

- 6. Add the following bold statements to the LBSViewController.m file:

```
@synthesize viewForMap;

- (void)viewDidLoad {
    self.lm = [[CLLocationManager alloc] init];

    if ([CLLocationServicesEnabled]) {
        lm.delegate = self;
        lm.desiredAccuracy = kCLLocationAccuracyBest;
    }
```

### How It Works

How the map rotates is actually very simple. On first thought, the easiest way would be to apply the transformation to the mapView. However, doing so not only rotates the map, it also rotates the entire rectangle (see Figure 18-16).

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_501_0.png)

### FIGURE 18-16

The trick is to embed the mapView within another View view and rotate it within the View. Hence, you added another View (viewForMap) in the View window and set it to Clip Subviews. Essentially, all the views added to this View will not display beyond its boundary.

Instead of displaying the map in the original size, you now need to set it to a minimum of 988.98 x 988.98 pixels (see Figure 18-17). This is the length of the diagonal of the viewable rectangle of the map. For simplicity, round it up to 1000 x 1000 pixels:

```
//---display the map---
mapView = [[MKMapView alloc]
    initWithFrame:CGRectMake(-140, -161, 1000,1000)];
```

The mapView is now added to viewForMap, instead of self.view:

```
//[self.view addSubview:mapView];
[self.viewForMap addSubview:mapView];
```

Recall that the initial position of the mapView was (10, 60):

```
initWithFrame:CGRectMake(10, 60,720,678)];
```

But it must now be changed to (-140, -161):

```
initWithFrame:CGRectMake(-140, -161, 1000,1000)];
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_502_0.png)

### FIGURE 18-17

Figure 18-18 shows how the new coordinate of (-140, -161) was derived. Remember, when you try to add a view to another, the coordinate specified is always with respect to the view you are adding to. In this case, the reference point (0,0) is at viewForMap.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_502_1.png)

### FIGURE 18-18

Finally, to rotate the map, apply the CGAffineTransformMakeRotation() method to the mapView:

```
//---rotate the map---
mapView.transform = CGAffineTransformMakeRotation(-radians);
```

## Displaying Annotations

So far, you have used Core Location to report your current location and heading and then used the Map Kit to display a map representing your location. A visual improvement you can make to the project is to add a push pin onto the map, representing your current location.

In the following Try It Out, you learn how to add annotations to the map in Map Kit. Annotations enable you to display push pins on the map, denoting some locations.

### TRY IT OUT Displaying a Push Pin

- 1. Continuing with the LBS project, add a new Objective-C Class file to the Classes folder of the project (see Figure 18-19).

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_503_0.png)

FIGURE 18-19

- 2. Name it as MyAnnotation.m. Once it is added, you should see the MyAnnotation.h and MyAnnotation.m files under the Classes folder (see Figure 18-20).

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_504_0.png)

FIGURE 18-20

- 3. Populate the MyAnnotation.h file as follows:

```
#import <Foundation/Foundation.h>
#import <MapKit/MapKit.h>

@interface MyAnnotation : NSObject <MKAnnotation> {

    CLLocationCoordinate2D coordinate;
    NSString *title;
    NSString *subTitle;
}

@property (nonatomic, readonly) CLLocationCoordinate2D coordinate;
@property (nonatomic, retain) NSString *title;
@property (nonatomic, retain) NSString *subTitle;

- (id)initWithCoordinate:(CLLocationCoordinate2D) c
                 title:(NSString *) t
               subTitle:(NSString *) st;

- (void) moveAnnotation: (CLLocationCoordinate2D) newCoordinate;
- (NSString *)subtitle;
- (NSString *)title;

@end
```

- 4. Populate the MyAnnotation.m file as follows:

```
#import "MyAnnotation.h"

@implementation MyAnnotation

@synthesize coordinate;
@synthesize title;
@synthesize subTitle;

- (NSString *)subtitle {
    return subTitle;
}
```

```
longitudeTextField.text]];
    [mapView addAnnotation:annotation];
}
}
-(void)dealloc {
    [annotation release];
    [compass release];
    [lm release];
    [latitudeTextField release];
    [longitudeTextField release];
    [accuracyTextField release];
    [super dealloc];
}
```

- 7. Press Command-R to test the application on the iPhone Simulator. You'll see the push pin inserted into the current position. When you tap on it, it displays the information in the annotation view as shown in Figure 18-21. Also observe that as you test it on a real device, the push pin will relocate on the map to represent your current location as you move.

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_507_0.png)

FIGURE 18-21

### How It Works

You first create the MyAnnotation class that inherits from the MKAnnotation base class. Within the MyAnnotation class, you implemented several properties (including coordinate, which specifies the center point of the annotation) and methods, in particular:

- - title — Returns the title to be displayed on the annotation.
- - subtitle — Returns the subtitle to be displayed on the annotation.
- - moveAnnotation: — Changes the location of the annotation.
