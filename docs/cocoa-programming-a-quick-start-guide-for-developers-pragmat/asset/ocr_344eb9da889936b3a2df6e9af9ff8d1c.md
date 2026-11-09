Our interface looks like this:

![](bbox=[0.356, 0.098, 0.556, 0.22])

Let’s get rid of the logger files. They don’t do any harm, but they clutter up this example a bit. You’ll need to delete Logger.h and logger.m. Don’t forget to delete the Logger object from Interface Builder’s Document window and remove the logger property from CounterAppDelegate.

UpOrDown will now need two outlets and two properties:

Download KVO/Counter/UpOrDown.h

```
```objc
#import <Cocoa/Cocoa.h>

@interface UpOrDown : NSObject {
    NSNumber *countOne, *countTwo;
}
@property(copy) NSNumber *countOne, *countTwo;
-(IBAction) stepOne:(id) sender;
-(IBAction) stepTwo:(id) sender;
@end
```
```

In UpOrDown.m, you need to synthesize both variables and implement the actions to set the properties using the current counter value:

Download KVO/Counter/UpOrDown.m

```
```objc
#import "UpOrDown.h"

@implementation UpOrDown

@synthesize countOne, countTwo;

-(IBAction) stepOne: (id) sender {
    self.countOne = [NSNumber numberWithInteger:[sender integerValue]];
}
-(IBAction) stepTwo: (id) sender {
    self.countTwo = [NSNumber numberWithInteger:[sender integerValue]];
}
@end
```
```