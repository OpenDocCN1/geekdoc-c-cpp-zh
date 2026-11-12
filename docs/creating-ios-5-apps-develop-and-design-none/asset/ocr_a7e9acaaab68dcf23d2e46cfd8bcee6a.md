```
```objective-c
UIColor* fill = [UIColor colorWithPatternImage:self.tileImage];
[fill setFill];
UIBezierPath* path =
[UIBezierPath
    bezierPathWithRoundedRect:
    CGRectInset(self.bounds, 1.0f, 1.0f)
    byRoundingCorners:UIRectCornerAllCorners
    cornerRadii:CGSizeMake(20.0f, 20.0f)];
path.lineWidth = 2.0f;
[path fill];
[path stroke];
// Not strictly necessary since we're subclassing
// UIView directly
[super drawRect:rect];
}
```
```

UIKit will draw repeated copies of our image pattern both vertically and horizontally to fill the entire path. In this case, we’re filling in the rounded rectangle and then drawing a 2-point-wide border around it. Notice that we inset our rounded rectangle by half our line width. This gives us enough space to draw our entire line, while still filling the view. This is then used as the background for our pop-ups, like our acceleration control, giving us a nice tessellated background (Figure 8.9).

Next, let’s look at creating resizable images. We will use these for the buttons in our export menu. Just like the tile image, we need to create two versions, one for low-resolution screens, the other for Retina displays (Figure 8.10). This time they will be 20 x 20 pixels and 40 x 40 pixels.

To make a resizable image, we take a normal UIImage and call its resizableImageWithCapInsets: method. This takes a single argument, a UIEdgeInsets structure holding the value of the cap insets on the top, left, bottom, and right.

When this image is resized, the areas covered by the cap insets are drawn normally. Areas between the cap insets are tiled to fill in the remaining space both horizontally and vertically. In our application, we create resizable images for our buttons during the ExportViewController’s tableView:cellForRowAtIndexPath: method.