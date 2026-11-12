```
```objectivec
- (NSTimeZone*)timeZone {
    // Get transient value.
    [self willAccessValueForKey:@"timeZone"];
    NSTimeZone* timeZone = self.primitiveTimeZone;
    // If we have no transient value,
    // try to generate it from the persistent value.
    if (timeZone == nil) {
        // Get the persistent value.
        NSString* name = self.timeZoneName;
        if (name != nil) {
            timeZone = [NSTimeZone timeZoneWithName:name];
            // Set the transient value.
            self.primitiveTimeZone = timeZone;
        }
    }
    [self didAccessValueForKey:@"timeZone"];
    return timeZone;
}
```
```

```
```objectivec
- (void)setTimeZone:(NSTimeZone *)timeZone {
    // Set transient value.
    [self willChangeValueForKey:@"timeZone"];
    self.primitiveTimeZone = timeZone;
    // Set persistent value.
    self.timeZoneName = [timeZone name];
    [self didChangeValueForKey:@"timeZone"];
}
```
```