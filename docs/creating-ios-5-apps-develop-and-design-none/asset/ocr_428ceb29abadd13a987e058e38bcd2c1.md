```
```objectivec
@" images when they are exported.";
[self.manager startUpdatingLocation];
default:
    // If permission has been denied, we're done.
    // We will return a nil location. No need to do
    // anything more.
    self.done = YES;
    break;
}
}
```
```

We start by clearing a few properties, and then we check to see if our application is authorized to use location services. If we're authorized, authorizationStatus will return kCLAuthorizationStatusAuthorized. If our application has not yet asked for permission, it will return kCLAuthorizationStatusNotDetermined. Otherwise, it will return one of the failure constants, depending on whether permission was denied, or whether permission cannot be granted (e.g., due to parental controls).

If we explicitly don't have permission, we don't bother setting up our location manager. We just set the done property to YES and leave our location property as nil. Otherwise, we go ahead and try to set up our location manager. The system will automatically ask the user for permission to use location services, if it hasn't done so already.

We still need to set three properties. First is the distance filter. This is the distance (in meters) that the device must move before generating a new location update. Setting this to kCLDistanceFilterNone will produce update notifications for any motion at all. In our case, we only want updates if the user moves a significant distance, so we set this value to 10 meters.

Next, we set the desired accuracy. Core Location sets a number of constants that we can use here. In our case, speed is more important than accuracy, so we set it to the nearest 10 meters. That should be good enough. In fact, if it's not fast enough, you may want to lower the accuracy even more. Be sure to test your application in a variety of environments, including indoors and in areas with little or no GPS reception (basement parking garages are good for this).