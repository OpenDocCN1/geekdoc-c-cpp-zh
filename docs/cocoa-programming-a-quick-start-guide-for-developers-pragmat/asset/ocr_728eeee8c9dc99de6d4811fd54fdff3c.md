```
```objective-c
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSArray *arrayOfSpinners = [self arrayOfSpinners];
    for (NSProgressIndicator *spinner in arrayOfSpinners) {
        [self spin:spinner];
    }
}
```
```

I’m going to size the window and place the progress indicators so that if all were visible at once, they would look like this:

![](bbox=[0.136, 0.261, 0.776, 0.362])

To do this, resize the window in Interface Builder so that its width is 415 and its height is 56. Create and place the progress indicators using Xcode in the arrayOfSpinners method.

```
```objective-c
- (NSArray *) arrayOfSpinners {
    NSMutableArray *array = [[NSMutableArray alloc] initWithCapacity:25];
    for (int i = 0; i < 25; i++) {
        NSProgressIndicator *spinner = [[NSProgressIndicator alloc]
                         initWithFrame:NSMakeRect(16 + i * 8, 20, 16, 16)];
        [spinner setStyle:NSProgressIndicatorSpinningStyle];
        [spinner setControlSize:NSSmallControlSize];
        [spinner setDisplayedWhenStopped:NO];
        [window.contentView addSubview:spinner];
        [array addObject:spinner];
    }
    return array;
}
```
```

The arrayOfSpinners method returns an array filled with the progress indicators. We iterate through this array and tell each one to start animating, sleep for one second, and then stop animating.

```
```objective-c
- (void) spin:(NSProgressIndicator *) spinner {
    [spinner startAnimation:self];
    sleep(1);
    [spinner stopAnimation:self];
}
```
```

Click Build & Run. The application will start up, and the progress indicators will appear and spin one at a time. If you hover your mouse