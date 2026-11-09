# Figure 16.3

Creating a subclass of `NSView`. Selecting the `NSView` template generates a file with extra features that aren’t included in the standard blank `NSObject` template.

![](bbox=[0.185, 0.206, 0.72, 0.518])

> **NOTE**
> 
> Because you never — or hardly ever — generate more than one instance of a root view subclass, the `initWithFrame:` method is never called. This code block isn’t notable for its usefulness, although it sometimes holds initialization code in a multi-document application.

The `drawRect:` method is a fundamental feature of `NSView`, and it is used as a wrapper for custom graphics code. The method is triggered automatically to refresh the view when the surrounding window is moved, opened, or resized. You can also trigger it on demand when you need to refresh the graphics for some other reason, such as a user event.

> **TIP**
> 
> You can create animations by triggering `drawRect:` repeatedly using a timer. For more on this, see the next chapter.