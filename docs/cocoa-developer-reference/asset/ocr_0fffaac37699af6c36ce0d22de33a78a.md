**Figure 6.21**
Exploring the new subclass. Currently it's still a subclass of NSObject.

![](bbox=[0.192, 0.155, 0.822, 0.538])

# **TIP**

When you create a new file in Xcode, you can use the drop-down menu to select NSObject, NSDocument, NSView, or NSWindowController as the source class. These classes are subclassed regularly, so they're built into Xcode to save you time. Choosing NSObject creates a blank header and implementation file. The other classes generate files that include stub definitions of some of their key methods.

Now that you have subclassed NSWindow, you can extend it by overriding one of the NSResponder mouse methods. You'll use `mouseDown:`. As before, the easy way to do this is to copy and paste the signature from the method signature from the class reference into the new class.

In Xcode, select `FirstNewWindow.m`. Paste the line under the `@implementation FirstNewWindow` directive so that the file looks like this:

```
    - (void)
    @implementation FirstNewWindow
    - (void)mouseDown: (NSEvent *) theEvent
    @end
```