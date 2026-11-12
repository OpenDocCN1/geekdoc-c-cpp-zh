![](bbox=[0.065, 0.145, 0.72, 0.485])

**FIGURE 8.2** Resetting the canvas

Our reset method looks deceptively simple, but this hides a subtle feature. When we instantiate our new CanvasViewController, we are not calling the designated initializer. Instead, we're calling the generic init method. This will then call [self initWithNibName:nil bundle:nil]. When the system goes to create our view hierarchy, it will call our controller's loadView method. Since we passed in a nil value for the nib name, the default implementation would normally look for a nib file named CanvasViewController.xib. However, as we saw earlier, we've overridden loadView to programmatically create our view hierarchy instead.

# CREATING POP-UP VIEWS

GSRootViewController will also be able to display pop-up views over the top of our canvas. We will use this to display a number of support views, including custom alert messages, a pause indicator, our acceleration control, and an export menu. GSRootViewController will also provide different animation options for when the view appears. It could slide in from the sides (with an animated bounce at the end), drop down from the top (also with a bounce), or simply fade in and out.

The pop-ups themselves consist of view and controller combinations. All of them use the same UIView subclass, PopupView. This is a simple, non-opaque view that draws a semi-transparent, rounded-rectangle backdrop, on which we will place our labels and other controls.