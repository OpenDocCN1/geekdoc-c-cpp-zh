# 12.1  Exercise: Creating and Setting the Delegate

Create a new property named delegate in the CurrentApp class. For now we use id as the type of delegate, so any object can be assigned to it.

Remove all the methods from ActivityController.m except for awakeFromNib. We’ll put some of it back before we’re done, but this will help you see some of the details in declaring and implementing a protocol. Set CurrentApp’s delegate to self in awakeFromNib.

# 12.2  Solution: Creating and Setting the Delegate

Add the delegate instance variable and property to CurrentApp.h:

```
Download Protocols/HelloApplication7/CurrentApp.h

#import <Cocoa/Cocoa.h>

@interface CurrentApp : NSObject {
    id delegate;
}
@property id delegate;

@end
```

We’ve labeled the delegate as an id so that an object of any type could be set as the CurrentApp delegate. Remember to synthesize the property in CurrentApp.m.

For now, we’re doing just three things in the ActivityController’s awakeFromNib method: we’re creating an instance of CurrentApp, we’re assigning this to our instance variable, and we’re setting that object’s delegate to be ourselves.

```
Download Protocols/HelloApplication7/ActivityController.m

#import "ActivityController.h"
#import "CurrentApp.h"

@implementation ActivityController

@synthesize currentApp, activityDisplay;

-(void)awakeFromNib {
    self.currentApp = [[CurrentApp alloc] init];
    self.currentApp.delegate = self;
}
@end
```