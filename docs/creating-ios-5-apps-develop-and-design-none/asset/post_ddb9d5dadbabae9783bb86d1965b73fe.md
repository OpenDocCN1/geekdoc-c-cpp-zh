
## CUSTOMIZING THE INTERFACE'S APPEARANCE

Often the standard user interface elements work just fine. They're reasonably attractive. Users recognize them and understand them. They know exactly what they do and how to use them. But let's face it: If you just use Apple's default controls, your application may begin to look somewhat bland. Sometimes it's important to color outside the lines.

How radical should your interface be? The answer depends on a number of things. What kind of application are you building? How comfortable are your users with new interfaces? How clearly can you communicate its intended use? While I can't answer these questions for you, I can show you some techniques to help you when you start striking out on your own.

Right off the bat, our GravityScribbler app needs to make two important changes to the default application behavior. As an immersive app, we want to seize control of the entire screen, hiding the device's status bar. This isn't something we should do lightly. The status bar contains vital information, including the time and the battery status. Hiding the status bar means your users won't have access to that information while using your app. Still, in many cases it's necessary to hide the status bar. If you're trying to build an immersive application, it can be a real distraction. Nobody wants to see the status bar while watching movies. Similarly, we don't want it to appear in GravityScribbler.

We also want to disable the system's idle timer. Again, the idle timer usually performs a vital role. If the application doesn't detect any user touches for a short period, it will dim the screen and then put the device to sleep. This helps save battery power when the device is not in use. Unfortunately, in our case, the user may use the device for long periods without ever touching the screen. Instead, they control the cursor using the accelerometer, and we don't want our application to go to sleep while someone is using it.

Both of these changes are incredibly easy to make. Add the following lines of code to the application delegate's application:didFinishLaunchingWithOptions: method.

```
UIApplication* app = [UIApplication sharedApplication];
[app setStatusBarHidden:YES];
[app setIdleTimerDisabled:YES];
```

### SEPARATING DYNAMIC AND STATIC VIEWS

We looked at drawing custom views in Chapter 5. However, that chapter focused on drawing a single, static view. Now we need to create a dynamic view. Our view needs to change over time—ideally, we would like to update it at 60 frames per second. That means we need to update it frequently, and each time we update it, we need to redraw it quickly.

Fortunately, not everything changes. At any given time, most of our view remains static, and only a small section changes. We need to update our cursor's position, and we need to draw a line from our old position to our new one. Other than that, everything else remains untouched.

We will create a new UIView subclass, Canvas, to handle our custom drawing. However, we will actually split the drawing into three sections: the background, the line, and the cursor. The background will remain static. It won't change at all. Our line will change. We continue to add new segments to it, but the existing portions remain untouched. We simply accumulate new line segments as time passes. Finally, the cursor will change its location but not its appearance as it moves about the screen.

Let's start by looking at the Canvas class and its companion CanvasViewController. View and view controller pairs are typically created in one of two ways. They are either loaded from a nib (possibly as part of a storyboard) or created in code. In this case, we will do everything in code.

We instantiate our view controller by calling its designated initializer, initWithNibName:bundle:. Now, when we pass a nil-valued nib name, the system expects that we will either provide a nib file whose name matches our view controller (in this case, CanvasViewController.nib) or override the controller's loadView method. In our case, we simply use loadView to instantiate our Canvas view and set its background color.

```objc
// Implement loadView to create a view hierarchy programmatically,
// without using a nib.
- (void)loadView
{
    self.view = [[Canvas alloc] init];
    self.view.backgroundColor = [UIColor lightGrayColor];
}
```

Here, the background color acts as our static background. As we saw in the “Performing Custom Drawing” section of Chapter 5, the system automatically draws the background color before calling drawRect:.

> **NOTE**: You must either provide a nib file or override loadView, but not both. If you provide a nib, you cannot override loadView.

### DRAWING THE LINE SEGMENTS

For our Canvas class, we have a slight problem. We want to incrementally draw our line over time. Every frame, we will add a new line segment to our image. Drawing the new segment is easy enough. We just calculate the bounds around the line segment, and call setNeedsDisplayInRect: to redraw those bounds. The problem is, any old line segments that also intersect any part of our bounding box also need to be redrawn or they will be erased.

Now, we could simply keep a list of all our line segments, then iterate over our list and redraw any that might be affected by the bounds. This works well enough at first but quickly bogs down as our drawing gets more and more complex. After a minute or so, the application becomes noticeably sluggish. Instead, we need a way to save and access subsections of our entire line in constant time.

We'll do this by creating an offscreen context and then drawing our new line to this context. We can then convert the context to an image and use the image to update only the region of the screen that has changed.

Our offscreen context needs to be the same size as our screen—so let's set it whenever our Canvas view's frame size changes. Override its setFrame: accessor as shown:

```objective-c
- (void)setFrame:(CGRect)frame {
    // If the frame is the same, do nothing.
    if (CGRectEqualToRect(self.frame, frame)) return;
    // If the frame size has changed, generate a new image context.
    if (!CGSizeEqualToSize(self.frame.size, frame.size)) {
        UIGraphicsBeginImageContextWithOptions(
            frame.size, NO, 0.0f);
        [[UIColor blackColor] setStroke];
        CGContextRef context = UIGraphicsGetCurrentContext();
        NSAssert(context != nil, @"Created a nil context");
        CGContextSetLineWidth(context, 1.0f);
        dispatch_sync(self.serialQueue, ^{
            self.imageContext = context;
        });
        UIGraphicsEndImageContext();
    }
    [super setFrame:frame];
}
```

We could use the Core Graphics function `CGBitmapContextCreate()` to create our offscreen context; however, setting up a correctly formatted bitmap context is not trivial. We also want to make sure our context’s coordinates and scale match our main screen. The easiest way to do this is to call UIKit’s `UIGraphicsBeginImageContextWithOptions()` function.

`UIGraphicsBeginImageContextWithOptions()` takes just three parameters. The first is the desired size—we pass in our view’s frame size. The second determines whether the context is opaque. By passing in `NO`, we create a transparent context. Finally, the third parameter determines the context’s scale. By passing in `0.0f`, we set the scale equal to our device’s main view (2.0 for a Retina display, 1.0 for older iPhones).

This function will create a correctly formatted context and set it as our current context. We can then set the stroke color, grab a reference to the context, and set the line width. Finally, we use a property to store this context, and we clean up after ourselves by calling `UIGraphicsEndImageContext()`.

OK, if you were paying attention, you may have noticed that I just skimmed over something sort of important. What the heck is the whole `dispatch_sync()` function doing in there?

Here’s the problem. We will add new line segments to our image context on a background thread. However, we will update our view using the image context in the main thread. As a result, we need to synchronize these reads and writes.
