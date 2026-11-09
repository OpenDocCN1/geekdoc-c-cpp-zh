```
-(void) applicationDidLaunch: (NSRunningApplication *) app {
    [self displayAction:@"Launched" forApplication:app];
}
-(void) applicationDidTerminate: (NSRunningApplication *) app {
    [self displayAction:@"Terminated" forApplication:app];
}
@end
```

The signature of our delegate methods has changed, so we have to
update the protocol to match:

Download Dictionaries/HelloApplication18/ActivityMonitorDelegate.h

```
@protocol ActivityMonitorDelegate

-(void)applicationDidLaunch: (NSRunningApplication *) app;
-(void)applicationDidTerminate: (NSRunningApplication *) app;

@end
```

Another advantage of using the NSRunningApplication object is that we
can remove the import and forward declarations of the CurrentApp class.

In CurrentApp.h, we replace the name property with a property named
app of type NSRunningApplication:

Download Dictionaries/HelloApplication18/CurrentApp.h

```
#import <Cocoa/Cocoa.h>
#import "ActivityMonitorDelegate.h"

@interface CurrentApp : NSObject {
    NSObject <ActivityMonitorDelegate> *delegate;
    NSRunningApplication *app;
    NSDictionary *delegateMethods;
}
@property IBOutlet NSObject <ActivityMonitorDelegate> *delegate;
@property NSRunningApplication *app;

@end
```

Lastly, we synthesize the app property, set its value from the userInfo
dictionary, and pass it in as our parameter when we call the delegate
methods:

Download Dictionaries/HelloApplication18/CurrentApp.m

```
@synthesize delegate, app;

-(void) respondToChange:(NSNotification *) notification {
    SEL methodName = NSSelectorFromString(
        [delegateMethods objectForKey:[notification name]]);
```