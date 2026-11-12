
```objc
- (void)drawRect:(CGRect)rect {
    // Draw the dot.
    [[UIColor redColor] setFill];
    UIBezierPath* dot =
        [UIBezierPath bezierPathWithOvalInRect:self.bounds];
    [dot fill];
}
```

The designated initializer simply sets our Cursor view's opaque property to NO, while drawRect: simply draws a round circle to fill the provided frame.

> **NOTE**: Our Cursor class will call drawRect: once, when the view is first created. The result is then cached and reused. This means we can move our cursor without triggering any additional drawing calls.
>
> Additionally, having our cursor separated from the lines and background means we don't need to delete the old position from the image context. We simply change the cursor's center property, and UIKit handles the rest.

Then, we instantiate our Cursor object during our Canvas class's designated initializer.

```objc
CGRect dotFrame = CGRectMake(0.0f, 0.0f, 8.0f, 8.0f);
_cursor = [[Cursor alloc] initWithFrame:dotFrame];
[self addSubview:_cursor];
```

We also add a method to center the cursor in the screen. We then call this whenever the view is reset (e.g., in the CanvasViewController's viewDidLoad method).

```objc
-(void)centerCursor {
    self.cursor.center = self.center;
    self.currentDrawPoint = self.center;
}
```

While this more or less works, it creates a few problems. First and foremost, iOS expects both the views and the view controllers to be in well-formed hierarchies. The system uses the view controller hierarchy to pass along a number of appearance and rotation messages, including viewWillAppear:, viewDidAppear:, viewWillDisappear:, viewDidDisappear:, willRotateToInterfaceOrientation:duration:, willAnimateRotationToInterfaceOrientation:duration:, and didRotateFromInterfaceOrientation:.

Having an invalid controller hierarchy usually doesn't create an immediately obvious problem. Rather, issues begin to crop up much later in the development cycle. At that point, the bugs can be very difficult to resolve.

In iOS 5, Apple deals with this issue by providing an enhanced UIViewController class, letting us subclass it to make our own view controller containers. They have also formalized the timing of method calls when views appear and disappear, as well as explicitly defining their expectations for view and view controller hierarchies.

When creating a view controller container, we must perform all of the following steps to add a new child view controller.

1. Add the subview controller to the container by calling addChildViewController:. This will automatically trigger a call to the child view controller's willMoveToParentViewController: method.
2. In general, the container view should set the subview's frame to define where it should appear, how large it should be, and so on.
3. Add the subview to the container's view by calling addSubview:. This will automatically trigger the calls to viewWillAppear: (before adding the view) and viewDidAppear: (after adding).
4. Perform any animation accompanying the view's appearance.
5. When done, call the subview controller's didMoveToParentViewController: method. The subview controller is now properly attached to the container.

Removing the child controller follows a similar series of steps:

1. Call the subview controller's willMoveToParentViewController: method, passing in nil as an argument.
2. Perform any animation accompanying the view's disappearance.
3. Remove the subview from the container's view by calling the subview's `removeFromSuperview` method. This will trigger `viewWillDisappear:` and `viewDidDisappear:` before and after the view is actually removed from the view hierarchy.
4. Remove the subview controller from the container by calling the subview controller's `removeFromParentViewController` method. This will automatically call the subview controller's `didMoveToParentViewController:` method, passing in nil as an argument.

As we will see, UIView's transition... methods can be used to combine some of these steps (particularly adding a new view, removing an old view, and any state change animations). However, in general, you must follow all of the above steps to create a valid view controller hierarchy.

**NOTE:** Some of these methods should only be called within our container controller subclass. In particular, `addChildViewController:` and `removeFromSuperview` should only be called internally within our container. We must provide our own wrapper methods to add and remove the subview controller as necessary. As a corollary, we should never call `addChildViewController:` on another view controller—as it is undoubtedly not prepared to handle the new view controller appropriately.

![](img/fe9fea534a8e7868f811f7cd33da015f_465_0.png)

Apple still recommends using their pre-built container view controllers whenever possible. However, custom containers provide an excellent method for customizing an application's flow. In GravityScribbler, we will use a custom container to display pop-up messages in response to different gestures from the user.

We will start by creating a UIViewController subclass, GSRootViewController. As the name suggests, this will act as the root view controller for our application. It will contain both our canvas and our pop-ups as child view controllers.

## MANAGING THE CANVASVIEWCONTROLLER

Let's start by creating a property to hold our CanvasViewController. We'll then write a custom setter to properly set up our canvas.

```objc
#pragma mark - Background View Controller
- (void)setCanvasViewController:(CanvasViewController *)
canvasViewController {
    // If we are passing in the same background view, do nothing.
    if ([canvasViewController isEqual:_canvasViewController])
        return;
    // Make it the same size as our current view.
    canvasViewController.view.frame = self.view.bounds;
    // Then swap views.
    [self addChildViewController:canvasViewController];
    [self.canvasViewController willMoveToParentViewController:nil];
    [self
    transitionFromViewController:_canvasViewController
    toViewController:canvasViewController
    duration:1.0f
    options:UIViewAnimationOptionTransitionCurlUp
    animations:^() {/* Do nothing */}
    completion:^(BOOL finished)
    {
        [canvasViewController didMoveToParentViewController:self];
        [_canvasViewController removeFromParentViewController];
        _canvasViewController = canvasViewController;
    }];
}
```

![](img/fe9fea534a8e7868f811f7cd33da015f_468_0.png)

**FIGURE 8.2** Resetting the canvas

Our reset method looks deceptively simple, but this hides a subtle feature. When we instantiate our new CanvasViewController, we are not calling the designated initializer. Instead, we're calling the generic init method. This will then call [self initWithNibName:nil bundle:nil]. When the system goes to create our view hierarchy, it will call our controller's loadView method. Since we passed in a nil value for the nib name, the default implementation would normally look for a nib file named CanvasViewController.xib. However, as we saw earlier, we've overridden loadView to programmatically create our view hierarchy instead.

## CREATING POP-UP VIEWS

GSRootViewController will also be able to display pop-up views over the top of our canvas. We will use this to display a number of support views, including custom alert messages, a pause indicator, our acceleration control, and an export menu. GSRootViewController will also provide different animation options for when the view appears. It could slide in from the sides (with an animated bounce at the end), drop down from the top (also with a bounce), or simply fade in and out.

The pop-ups themselves consist of view and controller combinations. All of them use the same UIView subclass, PopupView. This is a simple, non-opaque view that draws a semi-transparent, rounded-rectangle backdrop, on which we will place our labels and other controls.
