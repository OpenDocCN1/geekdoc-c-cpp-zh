
Next, implement the setWeightEntries:andUnits: method as shown here:

```
#pragma mark - Setting the weight data
- (void)setWeightEntries:(NSArray*)weightEntries
                  andUnits:(WeightUnit)units {
    self.graphStats =
      [[GraphStats alloc] initWithWeightEntryArray:weightEntries];
    self.units = units;
    [self setNeedsDisplay];
}
```

Here, we start by instantiating a new GraphStats object using the weightEntries argument. We then assign that object to our graphStats property. We also set the units property and call setNeedsDisplay.

The setNeedsDisplay method tells the system that the view's content has changed and needs to be redrawn. Notice that setNeedsDisplay does not trigger an immediate redrawing. Instead, the system just records the request and allows setNeedsDisplay to return. Then, during the next draw cycle, the view redraws itself.

## PERFORMING CUSTOM DRAWING

Now we get to the heart of this chapter: drawing our user interface.

When UIKit needs to draw a view (either entirely or just in part), it creates a graphics context whose origin matches the view's bounds (e.g., {0.0, 0.0} is located at the top left corner of the view). It also applies any transforms necessary to make the context match the view (rotation, scaling, etc.). Then, it calls the view's drawRect: method.

Of course, the default UIView's drawRect: method doesn't do anything at all, but we can override it to customize our view's appearance.

Please note, this is not the only way to draw a view. If you just want to change the background color, you do not need to implement drawRect:. Just change the view's backgroundColor property. The rest is automatic.

At the other extreme, if you are drawing the content directly in the view's layer, or if you plan to use OpenGL ES for your drawing, you do not need to override the drawRect: method. These approaches have their own drawing techniques.

## OPAQUE VIEWS

Each view has an opaque property. This property acts as a hint to the drawing system. If the property is set to YES, the drawing system will assume the view is completely opaque and will optimize the drawing code appropriately. If it is set to NO, the drawing system will composite this view over the top of any underlying views. This allows for fancier effects, but it can be a lot slower. By default, this property is set to YES. You should avoid changing this unless you actually need transparent or translucent areas in your view.

However, having an opaque view means our custom drawing code must completely fill the provided rectangle. We cannot leave any transparent or semi-transparent regions that might let underlying views show through. One approach is to simply assign an opaque backgroundColor, which will implicitly fill the entire view's rectangle. This may not be appropriate, however, if users (or other developers) can change the background colors, especially if they can select non-opaque background colors.

Still, if you plan to use the native drawing technologies in Core Graphics and UIKit, drawRect: is your best friend.

In our view, we will draw a simple graph. The y-axis will represent our weights; the x-axis will represent time. We will dynamically scale both axes to cover the full range from our array of WeightEntries. We will also draw a grid in the background, and reference lines to mark the maximum and minimum values. Finally, we will lay the weight's trend line over this background information.

Obviously, this isn't the best possible graph. Even small changes in weight can appear huge because of the autoscaling. A better approach would more intelligently select the scale so that it uses the entire space effectively, still shows the entire trend line, and also minimizes the natural daily variances. Additionally, we really should label both axes, not just the weights, and the reference lines should be spaced evenly throughout this range (every 2 pounds, 5 pounds, 10 pounds, whatever). It would also be nice if they aligned with the background grid.

Still, our quick and dirty implementation is relatively straightforward, while letting us explore a number of useful drawing techniques. So go ahead and uncomment the drawRect: method.

In theory, the first time this method is called, the rect argument should be set to the view's bounds, letting you fill the entire view. Subsequent calls may then only ask to redraw a small portion of that view. In practice, however, unless you are changing your view and explicitly calling setNeedsDisplay or setNeedsDisplayInRect:, you will probably only draw the view once. UIKit caches and reuses this original drawing.

The UIView draws onto its CALayer and then displays the CALayer as needed. As a result, we can resize the view, flip it, fade it in and out, and even cover it up and reveal it again without needing to redraw it.

If you are updating your view, you should try to make the update rectangle as small as possible. The system will automatically set the current context's clipping path to match the update rectangle. This prevents us from accidentally drawing outside the update rectangle. Still, we should avoid performing any unnecessary drawing, especially when frequently updating our views, since these can create significant performance bottlenecks.

In complex views, you often want to separate the content using multiple views or layers—one contains the static content, the others contain different dynamic elements. This allows us to selectively redraw only those elements that actually change.

In our case, the entire view is static; it should be drawn only once, when the system first displays it. This means we can safely ignore the rect argument and just draw the entire view. If, by some chance, the system happens to update just a portion of our view, everything will still work properly. Yes, we might waste a little computational effort trying to draw outside the clipping path—but those drawing commands are ignored and don't actually affect the application's appearance. Remember, there's no point in optimizing our code for edge cases that never occur in practice.

Also, notice that we don't ever draw our view's backgroundColor. The system automatically handles this for us before calling our drawRect: method. However, since our custom drawing code does not fill the entire view, we must either set a non-opaque background color or change our view's opaque property to NO. Anything else may result in unpredictable drawing errors.

### CORE GRAPHICS VS. UIKIT DRAWING

Our custom drawing code will use a combination of Core Graphics drawing functions and UIKit drawing methods. These methods and functions are (for the most part) completely compatible. In fact, the UIKit methods typically use Core Graphics functions to perform the actual drawing. Many duplicate methods exist between the two frameworks. For example, we set our current context's fill color using `[self.graphFillColor setFill]`. Alternatively, we could have called the Core Graphics function `CGContextSetFillColorWithColor(context, self.graphFillColor.CGColor)` instead.

Notice that there is an important difference here: UIKit uses UIColor classes, while Core Graphics uses CGColorRefs. Also, the UIKit methods implicitly use the current graphics context. Most Core Graphics methods require an explicit reference to the context. Still, while the details may differ, the end results are the same.

```
    #pragma mark - drawing
    - (void)drawRect:(CGRect)rect {
        // Calculate bounds with margin.
        CGRect innerBounds =
            CGRectInset(self.bounds, self.margin, self.margin);
        // Fill in the rounded rectangle.
        UIBezierPath* graphBorder =
            [UIBezierPath bezierPathWithRoundedRect:innerBounds
            byRoundingCorners:UIRectCornerAllCorners
            cornerRadii:self.cornerRadius];
        [self.graphFillColor setFill];
        [graphBorder fill];
```

Here we use the `CGRectInset()` method to create a smaller rectangle centered in the view's bounds. We use the margin property to determine the spacing between the inner bounds and the view's bounds. We set the default margin to 5.0f, so there should be a 5-point gap on all sides (left, right, top, and bottom).

Next, we use the `bezierPathWithRoundedRect:byRoundingCorners:cornerRadii:` convenience method to create a `UIBezierPath`. The `UIBezierPath` class lets us create a series of straight and curved line segments, then draw that path to the current context. Paths can be open or closed. You can build them either one
