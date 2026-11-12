# ABSTRACT CLASSES

In our sample class hierarchy, Vehicle, Boat, Airplane, and Car may be implemented as abstract classes. An abstract class is a class that cannot be instantiated into an object (or, at least, one that is not typically instantiated). Often it leaves one or more methods undefined. To use the abstract class, you first create a subclass that fully defines all the required methods. You can then create instances of that subclass.

Objective-C does not provide explicit support for abstract classes. However, we can create informal abstract classes by throwing exceptions in the undefined methods. Check out the documentation for NSCoder to see an abstract class in action.

Let’s look at a concrete example. UIView has a method called addSubview:. This lets you add another UIView to be displayed inside the current view. Since UILabel, UIButton, and UITextField all inherit from UIView (either directly or indirectly), they can all be added using the addSubview: method. In addition, they also inherit addSubview:. In theory, you could add a subview to your button or text field (though it’s hard to imagine a situation where this would be useful). More practically, the subclasses also inherit the UIView’s frame property. This allows you to set its size and position within the superview’s coordinate system. Everything that inherits from UIView (either directly or indirectly) has a frame.

# BROWSING THE SUPERCLASS’S METHODS

If you look at UIButton’s class reference, you will not find any information about a frame property. That’s because the class reference only shows the new methods declared for that particular class. So, how do you find all the inherited methods?

At the very top of the class reference, you see a line labeled “Inherits from.” This lists the complete chain of superclasses going all the way back to NSObject. By slowly walking back along the inheritance chain, you can look through all available methods and properties.