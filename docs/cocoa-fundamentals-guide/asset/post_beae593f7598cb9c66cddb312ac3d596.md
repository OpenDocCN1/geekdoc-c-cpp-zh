
# CHAPTER 4

# Cocoa Design Patterns

to communicate with specific purposes. For example, the Foundation framework includes `NSObject`, `NSCopying`, and `NSCoding` protocols, which are all very important ones. AppKit protocols include `NSDraggingInfo`, `NSTextInput`, and `NSChangeSpelling`. UIKit protocols include `UITextInputTraits`, `UIWebViewDelegate`, and `UITableViewDataSource`

Formal protocols imply the conforming class to implement all declared methods. However, they can mark single methods or groups of methods with the `@optional` directive, and the conforming class may choose to implement them. They are also fragile; if you define a protocol and make it available to other classes, further changes to it (except for additional optional methods) can break classes.

> **Further Reading:** More information on formal protocols, see "Protocols" in The Objective-C Programming Language.

# Chain of Responsibility

The Chain of Responsibility design pattern decouples the sender of a request from its receiver by giving more than one object to handle the request. The pattern chains the receiving objects together and passes the request along the chain until an object handles it. Each object in the chain either handles the request or passes it to the next object in the chain.

# Responder Chain

The application frameworks use an architecture known as the responder chain. This chain consists of a series of responder objects (that, inheriting from `Responder` or, in UIKit, `Responder`) along which an event (for example, a mouse click) or action message is passed and (usually) eventually handled. If a responder object doesn't handle a message, it passes the message to the next responder in the chain. The order of responder objects in the chain is generally determined by the view hierarchy, with the progression from lower-level to higher-level responders in the hierarchy, culminating in the view object that manages the view hierarchy, the delegate of the view, or the global application object. The paths of event and action messages up the responder chain differ. An application can have many responder chains as it has windows (or local hierarchies of views); but only one responder chain can be active—the one with the currently active window.

The AppKit framework implements a similar chain for handling error.

> **IOS Note:** UIKit implements the responder chain differently than AppKit. If a view is managed by a `UIViewController` object, the view becomes the next responder in the chain (and from there an event or action message passes to the view's superview). In addition, UIKit does not support a document architecture per; therefore there are no document objects or window-controllers in the responder chain. There is no error-handling responder chain in iOS.

The design of the view hierarchy, which is closely related to the responder chain, adapts the Composite pattern ("Composite" (page 143)). Action messages—messages originating from control objects—are based on the target-action mechanism, which is an instance of the Command pattern ("Command" (page 142)).

# CHAPTER 4
Cocoa Design Patterns

# Uses and Limitations

When you construct a user interface for a program either by using Interface Builder programmatically, you get one or more responders for "free". The responder chain goes in hand with a view hierarchy, which you get when you make a viewSubview of a window's content view. If you have a custom added to a view hierarchy, it becomes part of the responder chain. If the appropriate NSRResponder or UIResponder methods, you can receive and handle event messages. A custom object that is a delegate of a view object or the global object (NSApp in AppKit) can also receive and handle those messages.

You can also programmatically inject custom responders into the responder chain and you can programmatically manage the order of responders.

> Further Reading: The AppKit responder chains for handling events and action messages for handling errors are described in Cocoa Event Handling Guide and Error Handling Programming Guide. The UIKit responder chain is described in Event Handling Guide for iOS. The view hierarchy is a related design pattern that is summarized in Composite (page 143).

# Command

The Command design pattern encapsulates a request as an object, letting you parameter clients with different requests, query or log requests, and support undo operations. The request object binds together one or more actions on a specific receiver. The Command pattern separates an object making a request from the object that receive and execute that request.

# Invocation Objects

An instance of the NSInvocation class encapsulates an Objective-C message. An invocation object contains a target object, selector, and method parameters. You can dynamically change the target of the message dispatched by the invocation as well as its parameters; once the invocation is executed, you can also return the value from the object. With a single invocation object, you can repeatedly invoke the message with parameters.

The creation of NSInvocation requires a MethodSignature, which is an object of the runtime. The target-action mechanism can work on the basis of a selector (and not a method signature) because of the signature of an action method in AppKit by convention is always.

# Uses and Limitations

Invocation objects are used in contexts where you need to decouple an object sending a message from the object that receives it. The distributed objects technology is for communication. See "Proxy" (page 154) for more.

# CHAPTER 4
Cocoa Design Patterns

> Further Reading: See NSInvocation Class Reference for details on invocation objects. Also, consult the following documents for information about related technologies: Undo Architecture, Timer Programming Topics, and "The Runtime System".

# The Target-Action Mechanism

The target-action mechanism enables a control object—that is, a button, slider, or text field—to send a message to another object that can interpret the message and handle it. The receiving object, or target, is usually a custom controller object. The message—named an action message—is determined by a selector, a runtime identifier of method.

In the AppKit framework, the cell uniquely encapsulates the target and action. When the user clicks or activates the control, the control extracts the information from its cell and sends the message. (A menu item also encapsulates target and action and sends an action message when the user chooses it.)

# Uses and Limitations

When creating a Cocoa application, you can set a control's action and target through the Interface Builder application. You thereby let the control implement custom behavior without any code for the control itself. The selector and target connection are achieved in a nib and are restored when the nib is unarchived. You can change the target and action dynamically by setting the control or its cell `setTarget:` and `setAction:`.

In UIKit, the target-action mechanism does not rely on cells. Instead, a control maps a target and action to one or more events that the control can trigger.

A Cocoa program for Mac can use the target-action mechanism to instruct a custom controller object to transfer data from the user interface to a model object, or to display data in a model object. The Cocoa binding obligates the need to use target-action for purpose. Cocoa Bindings Programming Topics for more about this technology.

Controls and cells do not retain their targets. "Ownership of Delegates, Observers, and Targets" (page 196) for further information.

> Further Reading: See "The Target-Action Mechanism" (page 182) for further information.

# Composite

The composite design pattern composes related objects into tree structures to represent part-whole hierarchies. The pattern lets individual objects treat compositions of objects uniformly.

The Composite pattern is part of the Model-View-Controller aggregate pattern, which is described in "The Model-View-Controller Design Pattern" (page 160).
