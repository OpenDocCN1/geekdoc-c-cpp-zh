```
location = [NSString stringWithFormat:@"%@, %@", placemark.locality, placemark.country];
annotation.subTitle = location;

[geocoder release];
geocoder = nil;
}
```

3. Press Command-R to test the application on the iPhone Simulator. Notice that the Annotation view now displays the address of the location (see Figure 18-22).

![](bbox=[0.22, 0.4, 0.48, 0.66])

FIGURE 18-22

# How It Works

To perform reverse geocoding, use the MKReverseGeocoder class available in the Map Kit framework:

```
MKReverseGeocoder *geocoder;
```

When a location is obtained (via the locationManager:didUpdateToLocation:fromLocation: event), you instantiate the MKReverseGeocoder class by setting it to a location coordinate:

```
//---perform reverse geocoding---
if (igeocoder) {
geocoder=[[MKReverseGeocoder alloc]
initWithCoordinate:newLocation.coordinate];
geocoder.delegate = self;
[geocoder start];
}
```

The MKReverseGeocoder class works asynchronously, and will fire the reverseGeocoder:didFindPlacemark: event when an address has been found. Hence, you need to implement the MKReverseGeocoderDelegate protocol in the View Controller:

```
@interface LBSViewController : UIViewController
<CLLocationManagerDelegate,
MKMapViewDelegate,
MKReverseGeocoderDelegate> {
```