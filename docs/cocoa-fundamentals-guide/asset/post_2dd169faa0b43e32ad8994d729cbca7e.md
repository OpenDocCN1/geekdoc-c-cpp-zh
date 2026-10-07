
# Controls, Cells, and Menu Items

Most controls in AppKit inherit from the NSControl class. Although a control has the initial responsibility for sending an action message to its target, it carries the information needed to send the message. This, it usually relies on its cell or cells.

A control always has one or more cells—objects that inherit from NSCell—associated with it. Why is there this association? A control is a relatively "heavy" object that inherits all the combined instance variables of its ancestors, which include the NSView and NSResponder classes. Because cells are expensive, they are used to subdivide the real estate of a control into various functional areas. Cells are lightweight objects that can be used to overlay all or part of the control. It's not only a division of area, but a division of cells: cells handle the drawing that controls would otherwise have to do, and cells hold the data that controls them (instance variables for target and action). Figure 5-3 (page 184) depicts the control-cell architecture.

Abstract classes, NSControl and NSCell both implicitly handle the setting of the target and action instances. By default, NSControl simply sets the information in its associated cell, if one exists. NSControl itself supports, by default, one-to-one mapping between itself and subclasses of NSControl such as Matrix which support multiple cells.) In its implementation, NSCell simply raises an exception. You must go one step further down the inheritance chain to find the cell that implements the setting of target and action: NSActionCell.

Objects derived from NSActionCell provide target and action values to their controls so they can compose and send an action message to the proper receiver. An NSActionCell object handles mouse (cursor) tracking by highlighting its area and assisting its control in sending action messages to the specified target. In most cases, the responsibility for an NSControl object's appearance and behavior is given to a corresponding NSActionCell object (NSMatrix, and its subclass NSForm, are subclasses of NSControl that do not follow this.)

**Figure 5-3** How the target-action mechanism works in the control-cell architecture

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_183_0.png)

# CHAPTER 5
Communicating with Objects

When users choose an item from a menu, an action is sent to a target. Yet menus (NSMenu objects) and their items (NSMenuItem objects) are completely separate, in an architectural sense, from controls and cells. NSMenuItem implements the target-action mechanism for its own instances; an NS object has both target and action instance variables (and related accessor methods) and sends the action message to the target when a user chooses it.

> Note: See Control and Cell Programming for Cocoa and Application Menu and Pop-up List Listing
Topics for more information about the control-cell architecture.

# Setting the Target and Action

You can set the targets and actions of cells and controls programmatically or by using Interface Builder. For most developers and situations, Interface Builder is the preferred approach. When you use it to set controls and targets, Interface Builder provides visual confirmation, allows you to link the connections, and archives the connections to a nib file: procedure:

- 1. Declare an action method in the header file of your custom class that has the IBAction qualifier.
- 2. In Interface Builder, connect the control sending the message to the action of the target.

If the action is handled by a subclass of your custom class or by an off-the-shelf AppKit or UIKit class, you can make the connection without declaring any action method. Of, if you declare an action method yourself, you must be sure to implement it.

To set the action and target programmatically, use the following methods to send messages to a control or object:

```
(void)setTarget:(id)anObject:
(void)setAction:(SEL)aSelector:
```

The following example shows how you might use these methods:

```
[Cell setTarget:myController];
[control action:@selector(deleteRecord)];
[NSMenuItem action:@selector(showGuides:)]
```

Programmatically setting the target and action has its advantages and in certain situations it is the only possible approach. For example, you might want the target or action to vary according to some runtime condition, such as whether a network connection exists or an inspector window has been loaded. Another example is when you are dynamically populating the lists of a pop-up menu, and you want each pop-up item to have its own action.

# Actions Defined by AppKit

The AppKit framework not only includes many NSAction-based controls for sending action messages, it defines action methods in many of its classes. Some of these actions are connected to default targets when you create a Cocoa application project. For example, the Quit command in the application menu is connected to the terminate method in the global object (NSApp).

# CHAPTER 5
Communicating with Objects

The NSResponder class also defines many default action messages (also known as standard commands) for common operations on text. This allows the Cocoa text system to send these action messages up the screen to an application's responder chain—a hierarchical sequence of event-handling objects—where it can be handled by the first NSView, NSWindow, or NSApplication object that implements the corresponding method.

# Target-Action in UIKit

The UIKit framework also declares and implements a suite of control classes: the control classes in this framework inherit from UI class, which defines many of the target-action mechanism for iOS. However there are some fundamental differences in how the AppKit and UIKit frameworks implement-action. One of these differences is that UIKit does not have any true controls. Controls in UIKit do not rely upon their users for target and action.

A larger difference in how the two frameworks implement-action is in the nature of the event model. In the AppKit framework, the user typically uses a mouse and keyboard to register for events handling by the system. Events—such as clicking on a button—are discrete and connected. Consequently, a control object in AppKit recognizes a single physical event as the trigger for the action it sends to its target (In the case of buttons, this is a mouse-up event). In iOS, the user's fingers organize events instead of mouse clicks, drags or keystrokes. There can be more than one finger touching an object on the screen, and these can be going in different directions.

To account for multitouch event model, UIKit declares a set of control-constants inControlEvents.h which specify various gestures that users can make such as lifting a finger from a control, dragging into a control, and touching down within a text field. You can configure a control so that it responds to one or more of these touch events by sending an action to a target. Many of the control classes in UIKit are implemented to generate certain control events; for example, instances of the UISlider generate aControlEvents control event, which you can use to send an action to a target.

You set up a control so that it sends an action to a target by associating both target and one or more controls. To do this, use addTarget:forControlEvents: to the control for each action-pair you want to send. When the user touches the control in a designated fashion, the control forwards the action message to the global UIApplication object in sendAction:from: the UIApplication object is the centralized dispatch point for action messages. If the control specifies a nil for an action message the application queries objects in the responder chain until it finds one that is willing to handle the action message—that is, implementing one method corresponding to the action selector:

```
(void)action
(void)action:(id)sender
(void)action:(id)sender:(:(*)event
```

To learn more about the target-action mechanism in UIKit, read UIControl Reference.

The Target-Action Mechanism
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.
