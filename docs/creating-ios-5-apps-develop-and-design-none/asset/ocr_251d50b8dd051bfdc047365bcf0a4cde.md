Next, we have a method named keyPathsForValuesAffectingWeights. Whenever KVO is used to observe a value, the runtime looks for a method named keyPathsForValuesAffecting<key>, where <key> is the name of the value being observed. This method, if it exists, should return an NSSet containing all the keys that the observed value depends upon. Anyone observing <key> will be notified whenever any of the listed values are changed. In our case, anyone using KVO to monitor the weights property should receive notifications whenever weightHistory changes.

Then we have the accessor itself. Here we just return a reference to our weightHistory object. This isn't the most bulletproof approach. We could create an immutable copy and return that, or we could remove the weights property entirely, creating additional indexed accessors as needed. However, this approach is fast, and it does communicate our intent. The weightHistory array should never be modified outside the WeightHistory class. Given Objective-C's dynamic nature, a determined developer can always find ways to break encapsulation and monkey with our internal data, so this is probably good enough.

We still need to initialize our object. Simply override the init method, as shown:

```
```objective-c
#pragma mark - initialization

- (id)init
{
    self = [super init];
    if (self) {
        // Set initial defaults.
        _defaultUnits = LBS;
        _weightHistory = [[NSMutableArray alloc] init];
    }
    return self;
}
```
```

Here we simply set up reasonable initial defaults—creating an empty history list and setting the default units to pounds.