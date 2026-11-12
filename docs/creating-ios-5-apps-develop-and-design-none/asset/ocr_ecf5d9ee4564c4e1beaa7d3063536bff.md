Here, we just call animateWithDuration:animations:completion:. We set the duration argument to a quarter second. Inside the animation block, we simply set our alpha property to 1.0f. Core Animation will therefore animate the transition from 0.0f alpha (completely transparent) to 1.0f alpha (completely opaque), causing our view to fade in.

The completion block runs once the animation is done. Its finished argument is set to YES if the animation ran to completion and to NO if it stopped prematurely. In this block, we simply call didMoveToParentViewController to completely add our subview controller. Then we call our provided completion handler, if any.

For the drop down and slide animations, we want to add a little bounce at the end. To do this, we'll chain together several animation sequences. animateAppearDropDown:withCompletionHandler:, animateAppearSlideTowardsHome:withCompletionHandler:, and animateAppearSlideFromHome:withCompletionHandler: all calculate the horizontal or vertical bounce offset and then call animateWithBounce:verticalBounce:horizontalBounce:withCompletionHandler:.

This is where the real work is done. Basically, animateWithBounce:... defines three separate animation blocks. The first block's completion handler will call the second block, and the second block's completion handler will then call the third block. However, it's easiest to define these blocks in reverse order. Let's look at the method, one block at a time.

```
- (void)animateWithBounce:(UIViewController*)controller
           verticalBounce:(CGFloat)vBounce
        horizontalBounce:(CGFloat)hBounce
     withCompletionHandler:(void (^)(BOOL finished))completion {
    CGPoint center = self.view.center;
    // Chaining together animation blocks,
    // declare the bounce down animation block.
    void (^bounceDown)(BOOL) = ^(BOOL notUsed) {
      [UIView
       animateWithDuration:0.15f
       delay:0.0f
       options:UIViewAnimationCurveEaseIn
```