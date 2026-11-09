Who should be the sender? How does changeGreeting: have a handle to
the button if it's not called in response to a button click?

Let's introduce an outlet for our button:

Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.h

```
```
#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSTextField *textField;
    NSButton *button;
    BOOL isPersonalized;
}
@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet NSTextField *textField;
@property (assign) IBOutlet NSButton *button;

-(IBAction) changeGreeting:(id)sender;
@end
```
```

Connect this new outlet to your button in Interface Builder. If you'd
like, you can delete the button's title so that it is blank. Save.

In the implementation file, you'll need to synthesize button. Now you
can change the use of sender to self.button inside changeGreeting:. Let's
make applicationDidFinishLaunching: worse for a moment before we make
it better.

Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.m

```
```
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    self.window.backgroundColor = [NSColor greenColor];
    [self.textField setStringValue:@"Hello, World!"];
    [self.button setTitle:@"Personalize"];
    isPersonalized = NO;
}
```
```

This code is now identical to the true branch of the if statement, so let's
refactor. Introduce two utility methods, personalize and generalize, and
use them in applicationDidFinishLaunching: and changeGreeting:.

Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.m

```
```
#import "HelloWorldProAppDelegate.h"

@implementation HelloWorldProAppDelegate

@synthesize window, textField, button;

- (void) personalize {
    self.window.backgroundColor = [NSColor redColor];
```
```