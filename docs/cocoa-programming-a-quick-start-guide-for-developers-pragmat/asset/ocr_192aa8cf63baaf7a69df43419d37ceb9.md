As an aside, when you are designing applications for the iPhone or the iPod touch, you can use two additional variations. You can create an action that has no arguments. The following signature will work fine in Cocoa Touch:4

```
```objective-c
- (IBAction) actionSelector
```
```

This version is always my first choice when working with Cocoa Touch. If I had this no argument signature available to me in Cocoa, it would be my first choice here as well. In the case that I need to pass along the sender, I love having the option to do so. But there are many times where I don't need to communicate with the sender and don't need to know anything about the sender. I'd like that to be more clearly expressed in my code by using the no-argument version.

On the other hand, sometimes I need to know more than can be communicated by just passing along the sender. Sometimes I'd like to know something about the event that triggered the message. If you are writing a Cocoa Touch application, you can use this signature for an IBAction:

```
```objective-c
- (IBAction)respondToButtonClick:(id)sender forEvent:(UIEvent*)event;
```
```

Currently, for desktop applications, we need to use the single argument form for declaring an IBAction. For Cocoa Touch applications, we are free to use the no-argument and two-argument versions as well.

Back to our current example, add this highlighted declaration to the header file, and save your work:

![](bbox=[0.14, 0.592, 0.505, 0.611])

```
```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSTextField *textField;
}
@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet NSTextField *textField;

- (IBAction) changeGreeting:(id)sender;
@end
```
```

4. Cocoa Touch is how we describe the Cocoa APIs that target the iPhone OS.