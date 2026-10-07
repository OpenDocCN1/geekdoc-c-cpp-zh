
# Cocoa Design Patterns

## Keys

You specify properties of a model using a simple key, often a string. The corresponding view or controller uses the key to look up the corresponding attribute value. This design enforces the notion that the attribute itself doesn't necessarily contain the data—the value can be indirectly obtained or derived.

Key-value coding is used to perform this lookup; it is a mechanism for accessing an object's properties indirectly in, in certain contexts, automatically. Key-value coding works by using the name of the object's properties—typically its instance variables or accessor methods—as keys to access the values of those properties.

For example, you might obtain the name of a Department object using a key. If the Department object either has an instance variable or a method called name then a value for the key can be returned (if it either, an error is returned). Similarly, you might obtain Employee attributes using the firstName, lastName, and salary keys.

# Values

All values for a particular attribute of a given entity are of the same data type. The type of an attribute is specified in the declaration of its corresponding instance variable or in the return of its accessor method. For example, the type of the Department object name may be an NSString object in Objective-C.

Note that key-value coding returns only object values. If the return type or the data type for the specific accessor method or instance variable used to supply the value for a specified key is not an object, then an NSNumber or NSValue object is created for that value and returned in its place. If the name attribute of Department is of NSString, then using key-value coding, the value returned for the name key of Department object is an NSString object. If the budget attribute of Department is of float, then using key-value coding, the value returned for the budget key of a Department object is NSNumber object.

Similarly, when you use key-value coding, if the data type required by the appropriate accessor instance variable for the specified key is not an object, then the value is extracted from the passed object using the appropriate typeValue method.

The value of a to-one-relationship is simply the destination of relationship. For example, the value of the department property of an Employee object is a Department object. The value of a to-many relationship is the collection object. The collection can be a set or an array. If you use Core Data it is a set; otherwise, it is typically an array) that contains the destinations of that relationship. For example, the value of the employees property of an Department object is a collection containing Employee objects. Figure 4-13 shows an example object graph for the employee management application.

# CHAPTER 4

Cocoa Design Patterns

**Figure 4-13** Object graph for the employee management application

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_171_0.png)

# Key Paths

**A key path** is a string of dot-segmented keys that specify a sequence of object properties to traverse. The property of the first key is determined by, and each subsequent key is evaluated relative to, the previous property. Key paths allow you to specify the properties of related objects in a way that is independent of the model implementation. Using key paths you can specify the path through an object graph, of whatever depth, to a specific attribute of a related object.

The key-value coding mechanism implements the lookup of a value given a key path similar to key-value pairs. For example, in the employee-management application you might access the name of a Department via an Employee object using the `department.name` key path where `department` is a relationship of Employee and `name` is an attribute of Department. Key paths are useful if you want to display an attribute of a destination entity. For example, the table view in Figure 4-14 is configured to display the name of the employee's department object, not the department object itself. Using Cocoa bindings, the value of the Department column is bound to `department.name` of the Employee objects in the displayed array.

# CHAPTER 4
Cocoa Design Patterns

Figure 4-14 Employees table view showing department name

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_172_0.png)

Not every relationship in a key path necessarily has a value. For example, the manager relationship can be nil if the employee is the CEO. In this case, the key-value coding mechanism does not break—it simply stops traversing the path and returns an appropriate value, such as nil.

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

# CHAPTER 5

Communicating with Objects

Because it is an instance variable, an outlet becomes part of an object's encapsulated data. An outlet is more than a simple instance variable. The connection between an object and its outlets is always available in a nib whenever the file is loaded, each connection is unconnected and reestablished, and whenever it becomes necessary to send messages to the other object. The type qualifier `IBOutlet` is a tag applied to an instance-variable declaration that the Interface Builder application can recognize the instance variable as an outlet and synchronize the connection and interface of Xcode.

You connect an outlet in Interface Builder, you must first declare an outlet in the header file of your custom class by tagging the variable with the `IBOutlet`.

An application typically sets outlets between its controller objects and objects on the user interface, but they can be made between any objects that be represented as instances in Interface Builder, even between two custom objects. With any instance variable, you should be able to justify its inclusion in a class; the more instance variables an object has, the more memory takes. If there are other ways to obtain a reference to an object, such as finding it through its index position in a matrix, or through its inclusion as a function parameter, or using a tag (assigned unique identifier), you should do that instead.

Outlets are a form of object composition, which is a dynamic pattern that requires an outlet to somehow acquire references to its objects so that it can send messages to them. It typically holds these other objects as instance variables. These variables must be initialized with the appropriate references at some point during the execution of the program.

# Delegates and Data Sources

A delegate is an object that acts on behalf of, or in coordination with, another object when that object encounters an event. The delegating object is often a responder—that is, an object inheriting from `Responder` in AppKit or `Responder` in UIKit—that is responding to a user event. The delegate is an object delegated control of the user interface for that event, or is at least to interpret the event in an application-specific manner.

To better appreciate the value of delegation, it helps to consider an off control such as a text field (instance of `NSTextField` or `UITextField`) or a view (instance of `NSView` or `UIView`). These objects are designed to fulfill a specific role in a generic fashion; however the AppKit framework allows for manipulation of controls and handles such as closing, resizing, and moving the physical view. This restricted and generic behavior necessarily limits what the object can know about how an event (or will affect) something in the application, especially when the affected behavior is specific to your application. Delegation provides a way for your custom to communicate application-specific behavior to the off-shelf.

The programming mechanism of delegation gives objects a chance to coordinate their appearance and state with changes elsewhere usually by user actions. More importantly, delegation makes it possible for one object to alter the behavior of another object without the need to inherit from it. The delegate is almost always one of your custom objects, and by definition it incorporates application-specific logic that the generic and delegating object cannot possibly know.
