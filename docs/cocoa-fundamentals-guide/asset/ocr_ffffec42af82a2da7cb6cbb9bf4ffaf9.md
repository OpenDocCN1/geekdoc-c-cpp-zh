# CHAPTER 3
Adding Behavior to a Cocoa Program

*Objects* (page 175). When deciding on a candidate superclass, scan the header file of the class (or scan the reference documentation) to see if there is a delegation method, a notification, or some other mechanism that will enable you to do what you want without subclassing.

In a similar vein, you can also examine the header files or documentation for the framework protocols. By adopting a protocol, you might be able to accomplish your goal while avoiding the difficulties of a complex subclass. For example, if you want to manage the enabled states of menu items, you can adopt the NSMenuValidation protocol in a custom controller class; you don't have to subclass NSMenuItem or NSMenu to get this behavior.

Just some framework methods are not intended to be overridden, some framework classes (such as NSFileManager in AppKit and UIView in UIKit) are not intended to be subclassed. If you do attempt such a subclass, you should proceed with caution. The implementations of certain framework classes are complex and tightly integrated into implementations of other classes and different parts of the operating system. It is difficult to duplicate correctly what a framework method does or anticipate effects the method might have. Changes that you make in some implementations could have far-reaching, unforeseen, unpleasant consequences.

In some cases, you can get around these by using object composition, a general technique of assembling objects in a "host" object, which manages them to complex and highly customized behavior. Instead of inheriting directly from a complex framework subclass, you could create a custom class that holds instances of that as an instance variable. The custom class itself could be fairly simple inheriting from the root class NSObject; although without inheritance, the class manages, extends the instance itself. To clients it could appear to be a subclass of the complex subclass, although it probably won't share the interface of the subclass. The framework class NSAttributedString gives an example of object composition. NSAttributedString holds an NSString as an instance variable, is a class with complex behaviors, including string encoding, string searching, and path manipulation. NSAttributedString augments these behaviors with the capability for attaching attributes such as font, color, alignment, and paragraph style to a range of characters. And it does so without subclassing.

# Figure -3 Object composition

![](bbox=[0.176, 0.615, 0.755, 0.765])

| MyCompositeClass |
| Instance variables:
| NSString *string;
| NSFont *font;
| NSColor *color;
| Methods:
| - (void) drawString; |
| instantiate | string = "@Hello World"
font = Helvetica bold 12
color = dark grey | drawString
| Hello World! |

116 Inheriting from a Cocoa Class
2010-12-13 | ©2010 Apple Inc. All Rights Reserved.