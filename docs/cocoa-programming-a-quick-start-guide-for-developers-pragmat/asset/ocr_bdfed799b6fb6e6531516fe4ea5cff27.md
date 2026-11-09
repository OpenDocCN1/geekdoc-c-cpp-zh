You need to make two changes to HelloWorldAppDelegate.m. You have to import the header file for Greeter so that the compiler doesn't complain when you try to call greeting. You also have to set the label's string value to be whatever you get back by sending the message greeting to the class Greeter.

```
Download Classes/HelloWorld/HelloWorldAppDelegate.m

#import "HelloWorldAppDelegate.h"
#import "Greeter.h"
@implementation HelloWorldAppDelegate
@synthesize window;

- (void)createLabel {
    NSRect labelFrame = NSMakeRect(20, 20, 540, 50);
    NSTextField *label = [[NSTextField alloc] initWithFrame:labelFrame];
    [label setEditable:NO];
    [label setSelectable:NO];
    [label setAlignment:NSCenterTextAlignment];
    [label setFont:[NSFont boldSystemFontOfSize:36]];
    [label setStringValue:[Greeter greeting]];
    [[self.window contentView] addSubview:label];
}

-(void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    [self createLabel];
}
@end
```

Click Build & Run, and the results should be exactly the same as before. When you're ready, quit the application, and let's change this application to create objects and to use instance methods.

# 4.7 Creating a New Object

Next, we're going to create a new object and call an instance method. Because we configured the project to use garbage collection, there are a whole bunch of memory management details you don't have to worry about right now. I'll wait to show you those until Chapter 6, *Memory*, on page 102 because the details are a bit dry yet still important if you ever want to work in a non-garbage-collected Cocoa application or want to develop applications for the iPhone where garbage collection isn't supported.8 Because garbage collection is enabled, we just make a few small changes in our code to create an object of type Greeter.

8. Actually, memory management won't be the first detail I'll gloss over. You may have noticed an asterisk (*) or two float by without a comment. We also haven't talked about what happens when an application first starts up. How is it that our browser appeared