Finally, we need to set the location manager's purpose property. This is our chance to explain to the user why our application needs access to location services. It will be displayed when the system asks the user for permission to use location services.

**NOTE:** When using location services, the initial update may not have the desired accuracy. This is particularly true when requesting high-accuracy data. Core Location will calculate an initial estimate as quickly as possible and then refine the estimate as additional information comes in.

![](bbox=[0.745, 0.267, 1.0, 0.439])

Once everything is configured properly, we start generating location updates.

```
```objective-c
- (void)cancelSearch {
    [self.manager stopUpdatingLocation];
    self.done = YES;
}
```
```

By comparison, our cancel method is dead simple. We turn off location updates, and then we set our done property to YES.

```
```objective-c
- (void)getLocationWithCompletionHandler:
    (void (^)(CLLocation* location))completionHandler {
    self.callbackBlock = completionHandler;
    // If we've already found a location (or an error).
    if (self.done) {
        [self dispatchCallbackAndStopSearching];
    }
}
```
```

This should also be relatively straightforward. If we already have a location update, we'll call our callback immediately. To do this, we start by saving a reference to our callback block. If we're done, we go ahead and call dispatchCallbackAndStopSearching. If not, we keep waiting.