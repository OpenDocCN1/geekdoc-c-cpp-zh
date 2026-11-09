Add this line to HelloWorldProAppDelegate.m:

```
Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.m

#import "HelloWorldProAppDelegate.h"

@implementation HelloWorldProAppDelegate

@synthesize window;
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    self.window.backgroundColor = [NSColor greenColor];
}
@end
```

Click Build & Run, and your window should appear with the back-ground color set to green. How did this happen? We sent a message to the window property to change its background color. How did that message get through to the actual NSWindow that is part of the nib file?

There are two important steps to making this happen. First, check out the header file for the HelloWorldProAppDelegate class:

```
Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.h

#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
}
@property (assign) IBOutlet NSWindow *window;
@end
```

Do you see the IBOutlet keyword tucked into the middle of the @property declaration for window? This tells Interface Builder to include window in the list of outlets for every instance of HelloWorldProAppDelegate.

Double-click the MainMenu.xib file (remember you can find it under Resources). When the nib opens in Interface Builder, look at the Document window, and select the instance of the HelloWorldProAppDelegate class.²

2. If the Document window isn't visible, you can always bring it up using ⌘0 or Window > Document.