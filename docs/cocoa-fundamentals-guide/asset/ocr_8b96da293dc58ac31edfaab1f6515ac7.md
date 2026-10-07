# CHAPTER 4

# Cocoa Design Patterns

# Uses and Limitations

You can create or modify a view hierarchy whenever you add a view to another view, either programmatically or using Interface Builder. The AppKit framework automatically handles all relationships associated with the view hierarchy.

> Further Reading: Cocoa Drawing Guide discusses the view hierarchy in Mac OS X applications.

# Decorator

The decorator design pattern attaches additional responsibilities to an dynamic object. Decorators provide a flexible alternative to subclassing for extending functionality. As subclassing, adaptation of the Decorator pattern allows you to incorporate new behavior without modifying existing code. Decorators wrap an object of the class they behave to. They wrap and add their own behavior before or after delegating to the wrapped object. The Decorator pattern expresses the design principle that classes should be open to extension but closed to modification.

# General Comments

Decorator is a pattern for object composition, which is something that you are encouraged to do in your own code (see "When to Make a Subclass" (page 115)). Cocoa, however, provides some classes and mechanisms of its own (discussed in the following sections) that are based on the pattern. In these implementations, the extending object does not completely replace the interface of the object that it wraps, and the implementations use different techniques for interface sharing.

Cocoa uses the Decorator pattern in the implementation of several of its classes, including `NSAttributedString`, `NSScrollView`, and `UIDDatePicker`. The latter two classes are examples of compound views, which group together objects of other view classes and coordinate their interaction.

# Delegation

Delegation is a mechanism by which a host object employs a weak reference (in the sense that it is a simple pointer reference, unretained) to another object—the delegate—and periodically sends messages to the delegate when it requires its input for a task. The host object is generally an "off-the-shelf" framework object (such as `NSXMLParser` object) that is seeking to accomplish something, but can only do so in a generic fashion. The delegate, which is almost always an instance of a custom class, acts in coordination with the host object, supplying program-specific behavior at certain points in the task (Figure 4-3). Thus delegation makes it possible to modify or extend the behavior of another object without the need for subclassing.