![](bbox=[0.12, 0.128, 0.188, 0.183])

# CAUTION

**mouseDragged:** events continue to arrive even if the mouse is dragged out of the window frame. Hit testing becomes more critical for drag events; otherwise, you can drag values and objects all over the screen, even when you don't want to.

Use **mouseMoved:** events to capture the mouse cursor position when the left button isn’t pressed. **mouseMoved:** tracking is not enabled by default. To enable it, add the following code to the view’s `awakeFromNib:` method:

```
```objc
- (void) awakeFromNib {
    [[self window] setInitialFirstResponder: self];
    [[self window] makeFirstResponder: self];
    [[self window] setAcceptsMouseEvents: YES];
}
```
```

This tells the root window object to pass mouse moved messages to the view for processing. **mouseMoved:** tracking is active across the entire screen, and you should hit test the window bounds to limit the mouse action.

This is a small selection of the available mouse methods. The full list is defined in the NSResponder and NSView Class References. Other useful methods include:

+   - `mouseUp:` Sent when the left button is released.
+   - `mouseEntered:` Sent when the cursor enters a tracking area.
+   - `mouseExited:` Sent when the cursor exits a tracking area.

Use the `NSTrackingArea` class to define tracking area objects.

# Understanding the Cocoa Graphics System

To create Cocoa graphics, you must understand:

+   - How points, rectangles, and other basic data are packed into data structures, and how to set and read data from them
+   - How points and other elements are combined to create shape objects
+   - How shape objects are drawn into a view
+   - How colors and gradients are created and managed
+   - How images are loaded and drawn into a view

The rest of this section introduces these basic techniques and concepts.