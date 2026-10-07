# Communicating with Objects

Several of the Cocoa adaptations of design patterns assist communication between objects in an application. These mechanisms and paradigms include delegation, notification, target-action, and the bindings toplology. This chapter describes these mechanisms and paradigms.

# Communication in Object-Oriented Programs

With Cocoa and Objective-C, the object-oriented language for Cocoa, one way of adding the behavior that is specific to your program is through inheritance. You create a subclass of an existing class that either augments the attributes and behavior of an instance of that or modifies them in some way. There are other ways of adding the special logic that characterizes your program. There are other mechanisms for reusing and extending the capabilities of Cocoa objects.

The relationships between objects in a program exist in more than one dimension. The hierarchical structure of inheritance, but objects in a program also exist dynamically in a network of objects that must communicate with one another at runtime to get the work of the program done. In fashion similar to a musician in an orchestra, each object in a program has a role, a limited set of behaviors it contributes to the program. It displays an oval view to respond to clicks, or it manages a collection of objects, or it coordinates the major events of the application—it is designed to do one or more. But for its contributions to be realized in the program, it must be able to communicate with other objects. It must be able to send messages to other objects or receive messages from other objects.

Before your object can send a message to another, it must either have a reference to it or have some delivery mechanism and techniques, which are based on design patterns described in "Cocoa Design Patterns" (page 137), "Cocoa Design Patterns" (page 137), make it possible to construct robust applications efficiently. They range from the simple to the slightly more elaborate, and often are a preferable alternative to subclassing. You can configure them programmatically and sometimes graphically in Interface Builder.

# Outlets

An object is an instance variable—that is, an instance variable of an object that references another object. With outlets, the reference is configured and archived through Interface Builder. The connections between the connecting object and its outlets are reestablished every time the object is unarchived from its nib file. The containing object holds an outlet as an instance variable with the type qualifier of IBOutlet. For example:

```
@interface ViewController : NSObject
  IBOutlet NSArray *keywords;


```