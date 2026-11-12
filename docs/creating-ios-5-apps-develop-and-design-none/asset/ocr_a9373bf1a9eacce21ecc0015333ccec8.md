```
```objc
[super viewDidLoad];
id graphView = self.view;
[graphView setWeightEntries:self.weightHistory
                    andUnits:getDefaultUnits()];

// Register to receive notifications when the default unit changes.
[[NSNotificationCenter defaultCenter]
 addObserverForName:NSUserDefaultsDidChangeNotification
 object:[NSUserDefaults standardUserDefaults]
 queue:nil
 usingBlock:^(NSNotification *note) {
     [graphView setWeightEntries:self.weightHistory
                         andUnits:getDefaultUnits()];
 }];
}
```
```

Next, find the observeValueForKeyPath:ofObject:change:context: method. Delete it. We won't be using KVO in this implementation.

Finally, just as with the other view controllers, we need to convert our setWeightHistory: custom accessor into setDocuments:. This is long, but we've seen most of it before.

```
```objc
#pragma mark - Custom Accessor
- (void)setDocument:(UIManagedDocument*)document {
    NSNotificationCenter* center =
    [NSNotificationCenter defaultCenter];
    // If we're assigning the same history, don't do anything.
    if ([_document isEqual:document]) {
        return;
    }
    // Clear any notifications for the old history, if any.
    if (_document != nil) {
```
```