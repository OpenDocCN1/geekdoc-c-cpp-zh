```
```objc
- (void)viewDidUnload
{
    [super viewDidUnload];
    [self.weightHistory removeObserver:self forKeyPath:WeightKey];
    [self.weightHistory removeObserver:self forKeyPath:UnitsKey];
}
```
```

And we still need to catch these notifications. Remember, all KVO notifications go through the observeValueForKeyPath:ofObject:change:context: method. Let's implement that now.

```
```objc
- (void)observeValueForKeyPath:(NSString *)keyPath
                      ofObject:(id)object
                        change:(NSDictionary *)change
                       context:(void *)context {
    if ([keyPath isEqualToString:WeightKey]||
        [keyPath isEqualToString:UnitsKey]) {
        id graphView = self.view;
        [graphView
            setWeightEntries:self.weightHistory.weights
            andUnits:self.weightHistory.defaultUnits];
    }
}
```
```

Having all KVO notifications route through the same method is usually a disadvantage, but this time it actually helps simplify things. If we receive a change notification, we just verify that it matches one of our two keys. If there is a match—we don't even care which one—we call setWeightEntries:andUnits:, resetting both of them. Also, remember that setWeightEntries:andUnits: automatically calls setNeedsDisplay, causing our view to redraw itself.