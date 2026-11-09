justify the text in the text field, adjust the font size using the Attributes inspector, and save your work.

Add a new property for that text field to your header file for the HelloWorldProAppDelegate, and declare it to be an outlet. Use the outlet to print “Hello, World!” after the application launches.

Back in Interface Builder, connect the outlet to the text field.

Click Build & Run, and you should see a green background in your window with a text field on top displaying the message “Hello, World!”

# 7.4 Solution: Creating and Using an Outlet

There’s a rhythm to using Xcode and Interface Builder. You’ll bounce back and forth between them. You should have had no trouble dragging a text field and positioning it in your window in Interface Builder. Before you head back to Xcode, look at the Connections inspector for HelloWorldProAppDelegate. It should look exactly as it did before with a single outlet that is actively connected.

This next part is kind of cool. Add these two highlighted lines to your header file:

```
```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSTextField *textField;
}
@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet NSTextField *textField;
@end
```
```

You’ve added an instance variable named textField to HelloWorldProAppDelegate and declared the corresponding property. But even more important for our current purposes, you’ve marked textField as an outlet. Save the header file, and click back on the Connections inspector in Interface Builder.

Did you see that?