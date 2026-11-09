+   - Running the `makeObjectsPerformSelector:` method on the buttons in the array removes them all with a single line of code. No enumeration is needed.
+   - The geometry structures `NSRect` and `CGPoint` represent a rectangle and a point, respectively. These structures are explained in more detail next.

![](bbox=[0.104, 0.22, 0.172, 0.274])

**TIP**  
This application doesn’t try to avoid button collisions; sometimes buttons overlap. Try to modify the project so that buttons can never appear on top of each other. Various solutions are possible. Some enumeration may be needed.

# Handling mouse events in views

It's often useful to find the mouse position, either during a click or a drag event, or by following the cursor within a view. NSView supports a variety of mouse-tracking methods. Most are defined in NSResponder. To add them to a project, implement them with custom handlers as shown here. You can also download the mouse handler project from the Web site (www.wiley.com/go/cocoadeveloper) to see worked examples.

mouseDown: events are captured automatically. You can retrieve the coordinates within the window with

```
```objective-c
- (void) mouseDown: (NSEvent *) theEvent {
    NSPoint mouseLocation = [theEvent locationInWindow];
    NSLog (@"Mouse position: %.0f, %.0f", mouseLocation.x,
        mouseLocation.y);
}
```
```

It’s often useful to translate the coordinates to those of a subview and to limit clicks so that the application ignores them when they’re outside the subview. To translate coordinates, use

```
```objective-c
NSPoint mousePositionInPanel =
    [self convertPoint: mouseLocation toView: aTargetSubview];
```
```

After the translation, clicking at the bottom left of aTargetSubview returns 0,0.

To hit test the subview, use the mouse: inRect: method:

```
```objective-c
NSRect targetBounds = [aTargetSubview bounds];
if ( [self mouse: mousePositionInPanel inRect: targetBounds]) {…
```
```

The code in the conditional runs if the mouse is clicked inside the subview. Clicks outside the subview are ignored.

Use mouseDragged: to receive left-button drag events. You can read the mouse position using the same code as shown previously.