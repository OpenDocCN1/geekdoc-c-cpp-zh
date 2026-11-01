```
MKMapView *mapView;

IBOutlet UIImageView *compass;
IBOutlet UILabel *heading;

MyAnnotation *annotation;

NSString *location;
MKReverseGeocoder *geocoder;
}

@property (retain, nonatomic) CLLocationManager *lm;
@property (retain, nonatomic) UITextField *accuracyTextField;
@property (retain, nonatomic) UITextField *latitudeTextField;
@property (retain, nonatomic) UITextField *longitudeTextField;

@property (nonatomic, retain) UIImageView *compass;
@property (nonatomic, retain) UILabel *heading;

@end
```

2. In the LBSViewController.m file, add the following bold statements:

+   - (void)locationManager:(CLLocationManager *)manager didUpdateToLocation:(CLLocation *)newLocation fromLocation:(CLLocation *)oldLocation {
+       //---perform reverse geocoding---
+       if (!geocoder) {
+           geocoder=[MKReverseGeocoder alloc] initWithCoordinate:newLocation.coordinate];
+           geocoder.delegate = self;
+           [geocoder start];
+       }
+       //---display latitude---
+       NSString *lat = [NSString alloc] initWithFormat:@"%f", newLocation.coordinate.latitude];
+       latitudeTextField.text = lat;
+       //...
+       //...
+       //...
+   }
+   - (void)reverseGeocoder:(MKReverseGeocoder *)geo didFailWithError:(NSError *)error{
+       [geocoder release];
+       geocoder = nil;
+   }
+   - (void)reverseGeocoder:(MKReverseGeocoder *)geo didFindPlacemark:(MKPlacemark *)placemark {