
![](img/2b293e29fc15b0797f113b85dd429b6e_460_0.png)

## Creating Animations and 3D Graphics

Animations are often associated with games, but Cocoa makes it easy to animate almost any element in a user interface. Objects can move smoothly, pulse with color or brightness, jiggle, or change their size with one click or mouse over. Aqua includes standard animated effects, such as slide-out panes and pulsing buttons. In part, these are automatic. When you create a file open/save pane, the animation is embedded in the class and runs without further code.

You can add further animations to improve the look and feel of your application, make it more professional, and add value by subtly highlighting important features.

It’s also possible to create animated transitions when replacing one object with another. View swapping of this type is a key skill in iPhone app design, where swapped views replace the windows, panels, and panes of a desktop application.

![](img/2b293e29fc15b0797f113b85dd429b6e_460_1.png)

> **CROSS-REF**
> For a practical example of view swapping, see Chapter 19.

To use animations effectively, you must become familiar with Cocoa’s different animation classes and features. Many applications underutilize animations or add them in an unimaginative way. A key design goal is to use animations to create a genuine user benefit. A successful animation should do more than look impressive; it should also offer visual hints to the user to help him or her understand the application and use it in a more intuitive way.

For example, on the iPhone, views are swapped by finger movements accompanied by matching animations. The animation suggests a metaphor, such as a page curl, pop-up, swipe, or twirl, that implies something about the organization of the app. An app that swipes into a view but returns with a page curl feels inconsistent.

Cocoa includes a selection of classes and techniques that support animation. In outline, there are three options: direct property access; Core Animation, which is Cocoa’s main animation framework; and OpenGL, which is a complex low-level language that supports 3D scene rendering.

### 17 In This Chapter

- Creating direct property animations
- Using animators
- Creating custom animation objects
- Creating a simple OpenGL animation in Cocoa

### Creating a timer for animation

An animation timer is simply a timer that runs a dedicated animation method. There are no special animation timers in Cocoa. To create a timer, use the standard `NSTimer` object. The target is often `self`, but can be a different object.

```objective-c
NSTimer *theTimer = [NSTimer scheduledTimerWithTimeInterval:0.05
                     target: anObject
                     selector: @selector(theAnimationMethod:)
                     userInfo: anOptionalObject
                     repeats: YES];
```

Implement the animation timer method in the target object:

```objective-c
- (void) theAnimationMethod: (NSTimer *) theTimer {
    //Do something to a property here
}
```

Figure 17.1 illustrates a simple example. The view includes a single button. The code moves the button in a tight cycle around the center of the view and modifies its size dynamically. The button is always active: if you can catch it, you can click it. It could be connected to a selector action in the usual way.

**Figure 17.1**

The flying button, an unusual UI design you’re unlikely to see in a finished application

![](img/2b293e29fc15b0797f113b85dd429b6e_462_0.png)

### Creating property animation code

With direct property animation, you have complete freedom over how you implement the animation features. The key section of code for this example follows:

```objc
@synthesize window, theButton;
float bOffX, bOffY, currX, currY, centerX, centerY, timeCount,
      radius, theta;
CGPoint currPoint;
- (void)applicationDidFinishLaunching:
(NSNotification *)aNotification {
    NSTimer *aTimer =
    [NSTimer scheduledTimerWithTimeInterval:0.017
        target: self selector: @selector(timerMethod)
        userInfo: nil repeats: YES];
}
- (void)timerMethod
{
    timeCount += 0.05;
    theta = timeCount/6.283;
    bOffX = NSMidX(theButton.bounds);
    bOffY = NSMidY(theButton.bounds);
    centerX = window.frame.size.width/2;
    centerY = window.frame.size.height/2;
    radius = centerY*0.6;
    currX = centerX+radius*cos(theta)-bOffX;
    currY = centerY+radius*sin(theta)-bOffY;
    currPoint = NSMakePoint(currX, currY);
    [theButton setFrameOrigin:currPoint];
    [theButton setFrameSize:
    NSMakeSize(50+25*cos(2*theta), 50+25*cos(3*theta))];
}
```

The timer method updates the position counter, calculates the center of the view, and then uses simple trigonometry to create a circular path for the button. The button is repositioned by updating its frame origin with `setFrameOrigin:`; and it is resized by updating the frame size with `setFrameSize:`. An offset term corrects for the lower-left origin of the button’s frame and moves the draw point to the center of the button.

This is moderately complex code for a simple effect. It’s also heavily load dependent. If your Mac is busy, the button will stutter. This approach also makes it difficult to manage multiple simultaneous animations. It’s a good solution when you need to animate a small number of related properties, but it’s difficult to work with if you have more than one independent animation happening at once. You can create a separate timer for each animation, but this approach soon starts to become unwieldy.

![](img/2b293e29fc15b0797f113b85dd429b6e_463_0.png)

> **TIP**
> When animating position and size, set an object’s frame property, not its bounds. This also applies to rotation. A full rotation solution requires a backing layer, which is described later in this chapter.

### Using drawRect:

You can use a similar technique to create customized animated 2D graphics, using the paths and drawing objects described in the previous chapter. Use the timer method to initialize relevant path and object values for each update, and end the timer method with

```objc
[theView setNeedsDisplay];
```

![](img/2b293e29fc15b0797f113b85dd429b6e_464_0.png)

> **NOTE**
> If the view is refreshing itself, replace `theView` with `self`.

This generates an indirect call to the view's drawRect: method and refreshes the view. The drawRect: code can read the updated values to create a refreshed view for each timer update. You can use this technique to create complex effects. It's fast enough for simple games, but can stutter when the drawing code is dense and is updated at typical game refresh rates.

For more complex effects, you can get smoother results using one of Cocoa's other animation options.

### Using Animators

You can create very simple animation effects by adding a proxy — a simple drop-in animation controller that automatically adds an animation object, initializes it with useful default values, and runs the animation. Core Animation's proxy option gives you a lot of animation power for very little code. You can customize the animations with extra code, but a minimal implementation adds almost no code at all.

For example, to animate the position update for a button, replace

```objc
[theButton setFrameOrigin: newPosition];
```

with

```objc
[[theButton animator] setFrameOrigin: newPosition];
```

The animator creates a smooth change from the current position to the new position, with a default duration of 0.25 seconds.

### Creating a simple proxy animation

Figure 17.2 shows the nib from a very simple application that demonstrates proxy animation, using a button as a convenient animatable object.

**Figure 17.2**

The nib file for a simple animator demonstration application, with a subclassed view containing a button

![](img/2b293e29fc15b0797f113b85dd429b6e_465_0.png)

TheView is a subclass of NSView and includes the code shown below. When the user clicks the mouse, the mouseDown: handler reads the position and moves the button to the click position. Without an animator, the position of the button changes instantly. With an animator, the button glides between the old and new positions.

The code is straightforward. As in the previous example, an offset term corrects for the lower-left frame origin of the button; otherwise, the code reads the window coordinates of the mouse click, corrects for the offset, and sets the button’s position with the animator.

```objc
#import "TheView.h"
#import <QuartzCore/QuartzCore.h>

@implementation TheView
@synthesize theButton;
NSPoint oldPosition;
float bOffX, bOffY;
```

