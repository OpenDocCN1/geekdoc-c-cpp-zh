Well, there’s no sense in delaying the inevitable. Let’s jump right in.
Let’s start by creating a few helper methods. Still working in the WeightHistory implementation file, declare a string constant to hold our filename. Be sure to place this before the @implementation block.

```
```
static NSString* const FileName = @"health_beat.hbhistory";
```
```

Now find the WeightHistory class extension, and declare three private helper methods.

```
```
+ (NSURL*)localURL;
+ (NSURL*)cloudURL;
+ (BOOL)isCloudAvailable;
```
```

Then implement the methods as shown:

```
```
#pragma mark - Convenience Methods
+ (NSURL*)localURL {
    static NSURL* sharedLocalURL;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        NSError* error;
        NSURL* documentDirectory =
        [[NSFileManager defaultManager]
            URLForDirectory:NSDocumentDirectory
            inDomain:NSUserDomainMask
            appropriateForURL:nil
            create:NO
            error:&error];
        if (documentDirectory == nil) {
            [NSException
                raise:NSInternalInconsistencyException
                format:@"Unable to locate the local document "
```
```