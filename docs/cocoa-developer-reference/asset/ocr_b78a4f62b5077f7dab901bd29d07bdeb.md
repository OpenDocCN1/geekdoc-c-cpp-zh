![](bbox=[0.12, 0.128, 0.188, 0.184])

# NOTE

Behind the scenes, KVO works by using a trick called isa swizzling — a fancy way of saying that classes are copied and modified on the fly and updated versions impersonate the originals. This isn't a speedy process.

So in this example, you explicitly enable and disable KVO for all properties with a method called `isObserving:` in the App Delegate. The method is listed below:

```
```objective-c
#import "TempVerterAppDelegate.h"
@implementation TempVerterAppDelegate
@synthesize window, celsFloat, fahrFloat;
- (void)applicationDidFinishLaunching:(NSNotification *)
    aNotification {
    self.celsFloat = 100.0;
    self.fahrFloat = 212.0;
    [self isObserving: YES];
}
- (void) isObserving: (BOOL) observing {
    if (observing) {
        [self addObserver:self forKeyPath:@"celsFloat"
        options:NSKeyValueObservingOptionNew context:NULL];
        [self addObserver:self forKeyPath:@"fahrFloat"
        options:NSKeyValueObservingOptionNew context:NULL];
    } else {
        [self removeObserver: self  forKeyPath:@"celsFloat"];
        [self removeObserver: self  forKeyPath:@"fahrFloat"];
    }
}
- (void) observeValueForKeyPath: (NSString *)keyPath ofObject:(id)
    object change:(NSDictionary *) change
    context: (void *) context {
    NSLog(@"%@KeyPath:%@ Context: %@", keyPath,
    [self valueForKeyPath:keyPath]);
    [self isObserving: NO];
    if ([keyPath isEqual: @"celsFloat"])
        self.fahrFloat = 32+self.celsFloat*1.8;

    if ([keyPath isEqual: @"fahrFloat"])
        self.celsFloat = (self.fahrFloat-32)/1.8;

    [self isObserving: YES];
}
@end
```
```