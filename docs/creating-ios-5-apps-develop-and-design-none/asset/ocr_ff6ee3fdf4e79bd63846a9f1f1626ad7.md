FIGURE 5.6  View automatically stretched when rotated

FIGURE 5.7  Redrawing on rotation

![](bbox=[0.281, 0.166, 0.838, 0.394])

![](bbox=[0.294, 0.412, 0.852, 0.639])

Fortunately, there’s an easy fix. Our view controller already receives a `willAnimateRotationToInterfaceOrientation:duration:` message when the view rotates. We just need to override this method and ask the view to redraw itself.

```
```objective-c
- (void) willAnimateRotationToInterfaceOrientation:
       (UIInterfaceOrientation) toInterfaceOrientation
       duration:(NSTimeInterval)duration {
    [self.view setNeedsDisplay];
}
```
```

Now run the application again. Add a few weights, and try to rotate it (Figure 5.7). If everything is working properly, commit these changes.