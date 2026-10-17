# UNDERSTANDING NIBS

Cocoa applications load their graphic user interfaces from Interface Builder files (called nibs, or xibs if using XML format, which is the new default). The files are essentially “freeze-dried” object graphs representing the user interface you’ve constructed and the connections between the UI elements and one or more controller objects. Several key concepts are important to grasp when designing and working with a Mac OS or iOS application.

# FILE’S OWNER AND CONTROLLER OBJECTS

A nib and its content always have an owner. Whether it’s an instance of NSWindowController, NSViewController, NSDocument, or any other object, the owner serves as the top-level object that serves as the primary point to which to wire the user interface elements found in the nib.

Generally speaking, File’s Owner is intended to be a controller object (or, in the case of NSDocument, a model-controller). There can be and often are multiple controller objects within a single nib, any of which can provide outlets or actions.

# ACTIONS AND OUTLETS

Two types of connections exist between your code and a nib’s contents: actions and outlets. Both types of connection are established by drag and drop.

An action is a method that is called by a control. That is, depending on the type of control, some form of user input has triggered the control to perform its function. In the case of a button, a mouse click would trigger the button’s action. Any given control’s action requires two elements: the action itself and a target. Actions are defined in source code as follows:

```
- (IBAction)performSomeAction: (id)sender;
- (IBAction)performSomeOtherAction: (id)sender;
```

An outlet is an instance variable of an object (typically a controller or view object) that serves as a pointer to an element in a nib. Outlets are used to communicate

> **NOTE:** The file extension `.nib` stands for NextStep Interface Builder, which is a holdover from the original creators of these tools—Next, Inc. The newer file extension `.xib` stands for XML Interface Builder.