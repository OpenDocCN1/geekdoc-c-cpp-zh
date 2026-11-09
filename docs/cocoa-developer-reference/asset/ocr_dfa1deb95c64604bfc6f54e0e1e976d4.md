*continued*

The simplest way to manage view swaps is through a subclassed instance of UIViewController. Instead of passing a UIView directly to the window, pass it indirectly through the controller. Boilerplate code is included in the Xcode templates:

```
    [window addSubview:
        aViewController.view];
    [window makeKeyAndVisible];
```

To display a different view, update a UIViewController.view with a pointer to a UIView.

Views can be swapped semiautomatically. Navigation controllers and tab bar controllers implement standardized navigation solutions, swapping view controllers and their associated views as needed. Views can also be swapped manually with custom code managed by a view controller. Swaps can be triggered by almost any OS event. In many applications, views are swapped after a button tap. More complex effects are possible; for example, a location-aware app can display a new view when the user gets close to a geographical location. Subviews in a view are stored in an NSArray. UIView includes methods for inserting and removing views from the array and rearranging their order.

Because view swapping and controller subclassing is a key iOS design pattern, Xcode includes a convenient UIViewController subclass file template, with an associated nib file. To create new views in your app, create as many different subclasses of UIViewController as you need, and swap their views in as required. You can populate the nib files with user options — buttons, labels, graphics and contexts, text editable text fields, among others — and then add code to the view controller subclass to manage each item, linking outlets and actions as needed. For more on outlets, actions, and links, see Chapter 7.

index:0 of the UIView array is the root view. To implement a manual view swap, allocate an instance of the incoming view controller and load its nib using the initWithNibName: method. Alternatively, you can alloc and init instances of UIView dynamically in your code, adding features and setting options as needed. You can then swap in the new view by calling the insertSubview:atIndex:0 method on the currently visible

view. To remove and release a view, call the removeFromSuperview: method on the visible view.

Optionally, you can preload the new controller with data or link it to a data source so that it automatically loads and displays the data when it appears. Data is often processed for display in the viewDidLoad method in the new controller, which is triggered as soon as the view loads. You can also use the loadView method to populate the view dynamically from your code, or by loading a nib at runtime.

Modal views pop up or slide in temporarily — for example, to display app credits or contact information — and disappear when dismissed, revealing the original view. You cannot use modal views for navigation. To display a modal view, allocate an instance of the new view controller and call presentModalViewController: in the main view, passing the new controller as a parameter. To dismiss the modal view, call dismissModalViewController: in the main view.

All view swaps can be animated. Modal view swaps offer a small selection of preset animation, controlled by a constant loaded into the modalTransitionStyle property of the main view controller. Non-modal view swaps can be animated with a custom animation block that selects a preset animation effect, such as a page curl or cross fade, and sets an animation duration.

Because views can be swapped, they must be able to exchange messages and data with each other. Your app can use the protocol/delegate design pattern to implement message passing, or it can make direct connections between objects in the interface and a root controller using the responder chain.

The view system can seem complex, but it does not have to be difficult to work with. To avoid confusion, remember that the instance of UIViewController included in the app delegate sets which view is visible. Other instances of UIViewController can be loaded and released from memory. They can handle events, but their views remain invisible unless they are linked into the master controller's view property.

Apps typically use boilerplate code to implement view swapping. An example of this appears later in this chapter in the section on building a simple application.