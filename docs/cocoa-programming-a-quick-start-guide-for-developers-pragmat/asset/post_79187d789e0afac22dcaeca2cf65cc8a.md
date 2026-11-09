
should behave in general. It can't possibly know how any particular application should behave. One solution would be for us to subclass NSApplication and override the appropriate methods with our custom behavior. We tend to take a different approach in Cocoa applications. We assign a delegate object to the NSApplication and implement only those methods we need to implement. And what's a delegate? You can think of it as an assistant class that the main class passes work to. When the main class, in this case Application, needs something done, it calls a method in its delegate class.

Fortunately, the Cocoa Application template created an application delegate for us named HelloWorldAppDelegate. You'll find the source files in the Classes folder under Groups & Files.²

- HelloWorld
  - Classes
    - HelloWorldAppDelegate.h
    - HelloWorldAppDelegate.m
  - Other Sources
  - Resources
  - Frameworks
  - Products

The Cocoa Application template has created the files HelloWorldAppDelegate.h and HelloWorldAppDelegate.m, which together define the class HelloWorldAppDelegate.

Inside HelloWorldAppDelegate.m, there is a method named applicationDidFinishLaunching: that contains the following comment:

```
// Insert code here to initialize your application
```

Add the log line in place of the comment like this:

[Download Classes/HelloWorld/HelloWorldAppDelegate.m](#)

```objc
#import "HelloWorldAppDelegate.h"
@implementation HelloWorldAppDelegate
@synthesize window;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSLog(@"Hello, World!");
}
@end
```

² If you don't find these files, you are probably using Xcode version 3.1 or earlier and need to move to Xcode 3.2 or later.

How is this method ever called? We don’t call it explicitly from main(). In fact, we don’t explicitly call it from anywhere.

The simple explanation is that at runtime after the application finishes launching, the application object sends its delegate the message applicationDidFinishLaunching. The slightly longer version is what you saw in the previous chapter: if the delegate didn’t implement this method, then there would be a runtime error when it is called. So, what really happens is the application object checks to make sure the delegate implements the method, and if it does, then it sends the message.

![](img/9355405953264484a02198b0e3d25b7e_65_0.png)

To run the application, first show the Console with Run > Console or ⇧ ⌘ R. Next, clear the Console by selecting Run > Clear Console, by pressing ⌃ ⌘ R, or by clicking the Clear Console button if it is visible. Finally, click Build & Run (or use the keyboard shortcut for this, ⌘R).

HelloWorld should start up, the empty window will appear, and the Console should contain a line indicating the time at which the session started followed by a line with a time stamp, the process ID, and the string we created. Mine looks like this:

```
HelloWorld[19673:10b] Hello, world!
```

Once you’ve admired your achievements for a bit, you can quit HelloWorld and get back to work.

### 4.3 Using an Existing Class

We’ve got a “Hello, World” app printing out nicely to the Console. As our next step, we’ll create a text field in code, add it to our window, configure it a little, and then display “Hello, World!” in this text field. Remember, our goal is not to print out “Hello, World!” in a text field. If that were our only goal, we could just drag the widget out of the library in Interface Builder and type in the phrase *Hello, World!*³ The rule of thumb for Interface Builder is simple: any time you can use Interface Builder, you should use Interface Builder. There is nothing you can do in Interface Builder that can't be done in code. There is no reason to avoid Interface Builder for any but very esoteric cases.

This is one of those cases. Our goal in this section is to gain experience in using code to instantiate, configure, and use a class that we didn’t write. Then we'll be ready to create and use our own classes.

To make things a bit easier, double-click MainMenu.xib to start Interface Builder, select your window, and use the Size inspector to set the width of the window to 580 and the height to 90. It’s unfortunately easy to select the view by mistake if you click the inside of the window. If you click the title bar for the window, then the title bar for the Size inspector should say *Window Size*.

I've set the maximum and minimum size of the window to be these dimensions as well so that the user can't resize the window. There’s nothing magic about these dimensions, but it will help us if we know the size of the window when we create and place a label.

So, think back to what happened when we placed the text field at the top of the window in our SimpleBrowser example. You grabbed a text field from the library and dragged it to the window and dropped it. It was automatically added to the view hierarchy. Your Document window looked something like this:

![](img/9355405953264484a02198b0e3d25b7e_66_0.png)

³ A side benefit of creating a text field in code in this example is that it should help convince you to use Interface Builder whenever you can.

Although you probably didn't pay attention at the time, the window contains a ContentView. When you dropped the text field onto the window, you were creating an instance of NSTextField, and you were adding it as a subview of the ContentView.

You then repositioned the text field and changed the text to display what you wanted. Here's how we might do this in code:⁴

Download Class: HelloWorld2/HelloWorldAppDelegate.m

```objc
#import "HelloWorldAppDelegate.h"
@implementation HelloWorldAppDelegate
@synthesize window;

-(void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSRect    labelLocation = NSMakeRect(20, 20, 540, 50);
    NSTextField *label = [[NSTextField alloc] initWithFrame:labelLocation];
    [label setStringValue:@"Hello, World!"];
    [[self.window contentView] addSubview:label];
}
@end
```

First, we create an NSRect that holds the information for the size and location of the label. This matches the work we did using Interface Builder in Chapter 2, *Using What's There*, on page 24, where we resized the text field or set its dimensions in the Size inspector. Notice that NSMakeRect() is a C function and not a method. This is fairly typical when we work with graphic elements. Although this is certainly too much information for now, an NSRect or an NSPoint is a C struct and not an Objective-C object. There will always be a corresponding C function such as NSMakeRect() or NSMakePoint() to create and configure these elements.

Next we create an instance of NSTextField named label and set its location and dimensions to those described by the labelLocation variable. We set the label's string value to be Hello, World! and add the label as a subview of the window's content view.

---

⁴ I'll assume for now you understand that *self.window* refers to the current object's window instance. I'll explain the dot syntax in Chapter 5, *Instance Variables and Properties*, on page 86.

Click Build & Run, and you should see something like this:

![](img/9355405953264484a02198b0e3d25b7e_68_0.png)

I'm not very happy with the current state of this project. Sure, the output looks ugly, and we'll fix that, but mainly I'm concerned with the state of the code. Let's refactor it a bit.

### 4.4 Refactoring Code

Now and then it helps to step back from your code and look to see what could use some cleaning up. Now that I look at it, I don't like the name labelLocation. Of course, we could get rid of the variable completely and just inline the creation of the NSRect without using an explanatory temporary variable. That would be one solution.

If instead we choose to rename the variable, then we need to take into account that it's not just the location of the label but also its size. As you might have guessed from the method name initWithFrame, these two pieces of information are collected in an NSRect and called a frame.

Let's use Xcode to change the variable name from labelLocation to labelFrame. In this case, it would be easy enough to make the change by hand, but I'd like to introduce you to how you might use Xcode to perform a couple of refactorings.

I don't know if you've noticed it yet, but when you click labelLocation (go ahead, click it), all instances of labelLocation are underlined.⁵ If you hover your mouse around the labelLocation you've selected, slightly to the right, you will get a drop-down arrow. This is the same interface you see when you hover over a phone number or an address that is part of an email you read in Mail.app. Click the arrow, and you should see the options shown here:

```objc
-(void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSRect labelLocation = NSMakeRect(..., ..., ..., 50);
    NSTextField *label = [[NSTextField alloc] initWithFrame:labelLocation];
    [label setStringValue:...];
    [self.window addSubview:label];
}
```

⁵ Here labelLocation appears only once, but you get the idea.
