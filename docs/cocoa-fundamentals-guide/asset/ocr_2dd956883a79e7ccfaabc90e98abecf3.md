# Cocoa Design Patterns

> Note: The target-action mechanism, which enables view objects to communicate user input and choices, however, the design of the mechanism differs in each controller type. For coordinating controllers, you connect the view object to its target (controller object) in Interface Builder and specify an action selector that must conform to a certain signature. Coordinating controllers, by virtue of delegating of windows and the global application object, can also be in the responder chain. The bindings mechanism used by mediating controllers allows action signatures with view objects to targets with a variable number of arbitrary types. Mediating controllers, however, arent in the responder chain.

There are practical reasons as well as theoretical ones for the revised compound design pattern depicted in Figure 4-7, especially when it comes to the Mediator design pattern. Mediating controllers derive from concrete subclasses of applications that should take advantage of,, such as the management of selections and placeholder values. If you do not use the bindings technology, your view object could use a mechanism such as the Cocoa notification center to receive notifications from a model object. But this would require you to create a custom subclass to add the knowledge of the notifications posted by the model object.

In a well-designed Cocoa MVC application, coordinating controller objects often owning mediating controllers, which are archived in nib files. Figure 4-8 shows the relationships between the two types of controller objects.

Figure 4-8 Coordinating controller as the owner of a nib file

![](bbox=[0.18, 0.452, 0.628, 0.755])

# Design Guidelines for MVC Applications

The following guidelines apply to Model-View-Controller considerations in the design of applications: