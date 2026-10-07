
# CHAPTER 4
Cocoa Design Patterns

## View Hierarchy

The views (NSView or UIView objects) in a window are internally structured into a view hierarchy. At the root of the hierarchy is a window (NSWindow or UIWindow object) and its content view, transparent view that fills the window's content rectangle. Views that are added to the content view become subviews of it, and they become subviews of any views added to them. Except for the content view, a view has one (and only one) supervisor and zero or number of subviews. You perceive this as containment: a superview contains its subviews. Figure 4-2 shows the visual and structural aspects of the view hierarchy.

**Figure 4-2** The view hierarchy, visual and structural

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_143_0.png)

The view hierarchy is a structural architecture that plays a part in both drawing and event handling. A view has two bounding rectangles, its frame and its bounds, that affect how graphics operations with the view take place. The frame is the exterior boundary; it locates the view in its supervisor's coordinate system, defines its size, and clips to the view's edges. The bounds, the interior bounding rectangle, defines the internal coordinate system of the surface where the view draws itself.

When a window is asked by the system to prepare itself for display, views are asked to render themselves before their subviews. When you send some messages to a view—for example, a message that requests a view to redraw itself—the message is propagated to supervisors. You can then treat a branch of the view hierarchy as a unified view.

The view hierarchy is also used by the responder chain for handling events and action messages. See the summary of the responder chain in "Chain of Responsibility" (page 141).

# CHAPTER 4
Cocoa Design Patterns

## Uses and Limitations

You can create or modify a view hierarchy whenever you add a view to another view, either programmatically or using Interface Builder. The AppKit framework automatically handles all relationships associated with the view hierarchy.

> Further Reading: Cocoa Drawing Guide discusses the view hierarchy in Mac OS X applications.

## Decorator

The decorator design pattern attaches additional responsibilities to a dynamic object. Decorators provide a flexible alternative to subclassing for extending functionality. As subclassing, adaptation of the Decorator pattern allows you to incorporate new behavior without modifying existing code. Decorators wrap an object of the class they behave to. They wrap and add their own behavior before or after delegating to the wrapped object. The Decorator pattern expresses the design principle that classes should be open to extension but closed to modification.

## General Comments

Decorator is a pattern for object composition, which is something that you are encouraged to do in your own code (see "When to Make a Subclass" (page 115)). Cocoa, however, provides some classes and mechanisms of its own (discussed in the following sections) that are based on the pattern. In these implementations, the extending object does not completely replace the interface of the object that it wraps, and the implementations use different techniques for interface sharing.

Cocoa uses the Decorator pattern in the implementation of several of its classes, including `NSAttributedString`, `NSScrollView`, and `UIDDatePicker`. The latter two classes are examples of compound views, which group together objects of other view classes and coordinate their interaction.

## Delegation

Delegation is a mechanism by which a host object employs a weak reference (in the sense that it is a simple pointer reference, unretained) to another object—the delegate—and periodically sends messages to the delegate when it requires its input for a task. The host object is generally an "off-the-shelf" framework object (such as `NSXMLParser` object) that is seeking to accomplish something, but can only do so in a generic fashion. The delegate, which is almost always an instance of a custom class, acts in coordination with the host object, supplying program-specific behavior at certain points in the task (Figure 4-3). Thus delegation makes it possible to modify or extend the behavior of another object without the need for subclassing.

# CHAPTER 4
Cocoa Design Patterns

Figure 4-3 Framework object sending a message to the delegate

| Framework object | Task | Delegate |
| :--- | :--- | :--- |
| Step 1 | | |
| Step 2 | | object:willDoStep3: |
| Step 3 | | |
| Step 4 | | |
| Step 5 | | |

Delegation, in the simple sense of one delegating a task to another object, is a common technique in object-oriented programming. However, Cocoa implements delegation in a unique way. A host class uses a formal or an informal protocol to define what the delegate may choose to implement. All the methods in the informal protocol are optional, and the formal protocol may declare options, allowing the delegate to implement only some of the methods in the protocol. Before it attempts to send a message to its delegate, the host determines whether it implements the method (via a respondsToSelector message) to avoid runtime exceptions. For more formal and informal protocols, see "Protocols" (page 140).

Some classes in the Cocoa frameworks also send messages to their data sources. A data source is identical in all respects to a delegate, yet the intent is to provide the host object with data to populate a browser, a table view, or similar user-interface. A data source, unlike a delegate, may also be required to implement some methods of the protocol.

Delegation is not a strict implementation of the Decorator pattern. The (delegating) object does not wrap an instance of the class it wants to extend; instead, it may be a delegate around, in that the delegate is specializing the behavior of the delegating framework class. There is no sharing of interface either, other than the methods declared by the framework class.

Delegation in Cocoa is also part of the Template Method pattern ("Template Method" (page 158).

## Uses and Limitations

Delegation is a common design in the Cocoa frameworks. Many classes in the AppKit and UIKit frameworks send messages to delegates, including NSObject, UIApplication, UITableView, and several subclasses of NS. Some classes in the Foundation framework, such as NSParser and NSStream, also maintain delegates. You should always use a class's delegate mechanism instead of subclassing the class, unless the delegate does not allow you to accomplish your goal.

Although you can dynamically delegate, the only object can be informed of a particular event at the same time, you cannot use multiple objects. However, you can use the notification mechanism for this purpose. A delegate automatically receives notifications from its delegating framework object as long as the delegate implements one or more of the notification methods declared by the framework class. See the discussion of notifications in the Observer pattern ("Observer" (page 153).

Delegating objects in AppKit do not retain their delegates or data sources. See "Ownership of Delegates, Observers, and Targets" (page 196) for further information.

# CHAPTER 4
Cocoa Design Patterns

## Uses and Limitations

> Further Reading: For further information on delegation, see "Delegates and Data Sources" (page 176).

## Categories

A category is a feature of the Objective-C language that enables you to add methods (interface and implementation) to a class without having to make a subclass. There is no runtime difference—within the scope of your program—between the original methods of the class and the methods added by the category. The methods in the category become part of the class and are inherited by all subclasses.

As delegation, categories are not a strict adaptation of the Decorator pattern, fulfilling the intent but taking a different path to implementing that intent. The behavior added by categories is a compile-time artifact, and is not dynamically acquired. Moreover, categories do not encapsulate an instance of the class being extended.

The Cocoa framework defines numerous categories, most of them informal protocols (which are summarized in "Protocols" (page 140)). Often they use categories to group related methods. You may implement categories in your code without subclassing or to group related methods. However, you should be aware of these caveats:

- You cannot add instance variables to the class.
- If you override existing methods of the class, your application may behave unpredictably.

> Further Reading: See "Defining a Class" in The Objective-C Programming Language for more information on categories.

## Facade

The Facade design pattern provides a unified interface to a set of interfaces in subsystem. The pattern defines a higher-level interface that makes the subsystem easier to use by reducing complexity and hiding the communication and dependencies between subsystems.

## NSImage

The NSImage class of the AppKit framework provides a unified interface for loading and using images that can be bit-mapped (as those in JPEG, PNG, or TIFF format) or vector-based (as those in EPS or PDF format), NSImage can keep more than one representation of the same image; each representation is a kind of NSImageRep object. NSImage automates the choice of the representation that is appropriate for a particular type of data and for a given display device. It also holds the details of image manipulation and selection so that the client can use many different representations interchangeably.

How Cocoa Adapts Design Patterns
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

147
