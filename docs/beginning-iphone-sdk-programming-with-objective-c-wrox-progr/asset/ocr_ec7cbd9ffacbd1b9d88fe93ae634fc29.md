```
```objc
fromLocation: (CLLocation *) oldLocation{
    NSString *lat = [[NSString alloc] initWithFormat:@"%sg",
    newLocation.coordinate.latitude];
    latitudeTextField.text = lat;

    NSString *lng = [[NSString alloc] initWithFormat:@"%sg",
    newLocation.coordinate.longitude];
    longitudeTextField.text = lng;

    NSString *acc = [[NSString alloc] initWithFormat:@"%sg",
    newLocation.horizontalAccuracy];
    accuracyTextField.text = acc;

    [acc release];
    [lat release];
    [lng release];
}
- (void) locationManager: (CLLocationManager *) manager
    didFailWithError: (NSError *) error {
    NSString *msg = [[NSString alloc] initWithString:@"Error obtaining location"];
    UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Error"
    message:msg
    delegate:nil
    cancelButtonTitle: @"Done"
    otherButtonTitles:nil];
    [alert show];
    [msg release];
    [alert release];
}
- (void) dealloc{
    [lm release];
    [latitudeTextField release];
    [longitudeTextField release];
    [accuracyTextField release];
    [super dealloc];
}
```
```

8. Press Command-R to test the application on the iPhone Simulator. Figure 17-11 shows the simulator displaying the latitude and longitude of the location returned. It also shows the accuracy of the result.

> **NOTE** You can test the application on the iPhone Simulator. However, note that for the simulator, the device always reports a fixed position. There is no prize for guessing correctly where this position is referring to.