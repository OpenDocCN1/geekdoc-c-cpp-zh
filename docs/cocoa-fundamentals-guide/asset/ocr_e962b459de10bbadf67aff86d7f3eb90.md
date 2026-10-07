# CHAPTER 3

# Adding Behavior to a Cocoa Class

For example, displayName is ambiguous because it's unclear whether it displays the name or returns the display name.

+   - Use verbs in the names of methods or functions that represent actions.

+   - If a method returns an attribute or computed value, the name of the method is the name of the attribute.

These methods are known as "getter" accessor methods. For example, if the attribute background backgroundColor, the getter method should be named backgroundColor. Getter methods that return a Boolean are of a slight variation, using an "is" or "has" prefix—for example, hasColor.

+   - If a method sets the value of an attribute—that is, a "setter" accessor method—begins with "set" followed by the attribute name.

The first letter of the attribute name is in uppercase—for example, setBackgroundColor:

> Note: The implementation of setter and getter methods is discussed in detail in Storing and Accessing Properties (page 123) and in Model Implementation Guide.

+   - Do not abbreviate parts of API unless the abbreviation is well known (for example, HTML or TIFF).

For the complete set of naming guidelines for Objective-C interfaces, see Coding Guidelines for Cocoa.

A general, overarching API convention pertains to object ownership with memory-managed applications (versus garbage-collected collections). Briefly stated, the convention is that a client owns an object if it creates it (by allocation initialization), copies or retains it (by sending it retain). An owner of an object is responsible for its disposal using release or autorelease to the object when it no longer needs it. For more on this subject, see "How Memory Management Works" (page 73) and Memory Management Programming Guide.

# Inheriting from a Cocoa Class

A framework such as AppKit or UIKit defines a program model, because it is generic, many different types of applications can scale. Because the model is generic, it is not surprising that some framework classes are abstract or intentionally incomplete. A class often does much but leaves significant portions of the work unfinished or in a safe "default" fashion.

An application often needs to create a subclass that fills these gaps in its super, supplying the pieces the framework class missing. A subclass is the primary way to add application-specific behavior to a framework. It inherits the ability to work with other objects from the framework. For example, if you create a subclass of NSObject (AppKit), instances of this class will appear to appear in an NSString object, just as NSButton, UITextField, and other framework-defined class objects can.

When you make a subclass, one of your priorities is to implement a specific set of methods declared by a superclass (or in a protocol adopted by a subclass). Reimplementing an inherited method is known as overriding that method.