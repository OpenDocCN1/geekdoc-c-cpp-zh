# How to create an interface

Figure 15-3 how to create an interface. As you see in the syntax diagram at the top of this figure, you declare an interface using the interface keyword. This keyword is followed by the interface name.

Within the body of an interface, you can declare one or more methods, properties, and events. Although these are similar to the declarations for a class, there are three important differences. First, because an interface doesn't provide the implementation for its members, method declarations and the get and set accessors within a property always end in a semi-colon. Second, you can't code access modifiers on a member declaration for an interface. Instead, all members are considered to be public and abstract. If you inadvertently code the public or abstract keyword on member declaration, the compiler will generate an error message. Third, interfaces can't define static members, so you can't use the static keyword.

To begin coding an interface, you can add a new interface to your project by selecting the Project→Add New Item command and select the Interface item from the resulting dialog box. This will generate the code for the beginning of the interface. Then, you can modify the generated code and add members to the.

In the first example, the IDisplayable interface has been declared as public, so it's available to all classes in the current namespace. In addition, a GetDisplayText method specifies that the method accepts a separator string as a parameter and returns a string that contains the display text for the object.

In the second example, the IPersistable interface defines two methods and a property. Here, the Read and Save methods can be used to read and write the object, and the HasChanges property can be used to determine if the object contains any unanswered changes.

If an interface inherits other interfaces, the interface name is followed by a colon and a list of the inherited interfaces. In the last example, for instance, the IDataAccessObject inherits the IDisplayable and IPersistable interfaces. As a result, any class that implements IDataAccessObject must implement all three of the methods and the one property defined by IDisplayable and IPersistable. Although it isn't shown in this figure, IDataAccessObject could also add additional members.