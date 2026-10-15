```
public static int tele_no;
```

In the preceding code snippet, employee is the static class and id and tele_no are its members. A class that is static indicates that its members are also static. You cannot instantiate a static class using the new keyword. .NET Framework's CLR loads the static classes automatically when the program or namespace, which contains the static classes, is loaded.

Static class does not contain instance constructors, which are used to create and initialize instances. Static classes are sealed, which means that you cannot inherit these classes. You can declare a static class member using the static keyword, as shown in the following code snippet:

```
public static class student
{
    public static int roll_no = 4;
    public static int rank;
}
```

The preceding code snippet shows a student class, which is not static. However, the members of this class, roll_no and rank, are static. These static class members are initialized before they are accessed for the first time or before the static constructor is called.

Table 5.1 lists some differences between static and non-static members:

Table 5.1: Difference Between Static and Non-Static Members
| Parameter for Difference | Static Members | Non-Static Members |
| Belongs | Belongs to a class. This means that a static member can be called by a class and by the object of the class. | Belongs to an object of a class. This means that a non-static member can be called only by the object of the class. |
| Accessibility | Accesses only other static members of a class. | Accesses both static and non-static members of a class. |
| Instantiation | Creates only one copy of a static variable and its value remains the same even when the class is instantiated. | Creates a copy of the variables for their objects, every time the class is instantiated. |

# Properties

In C#, a property is a member that provides a flexible mechanism to read, write, or compute the value of a private field. C# is one of the first languages to offer direct support for properties. C++ Builder and Delphi languages offered this feature as an extension to the languages they supported (C++ and Object Pascal).

To the users of a class, a property looks similar to a public variable on which they can perform the get or set operations. The following code snippet shows how to use a property:

```
// Set the color property
Foo.Color = Color.white;
// Get the color property
Color c = Foo.Color;
```

However, you can implement properties with the type-safe get and set methods. You can create a property by defining an externally available name and then writing the set and get methods. Depending upon the input of the caller of the property, you can decide whether to allow the user to modify the property or not.

The following code snippet shows you the general syntax used for writing a property:

```
// Define the property accessors
public <type> <PropertyName> {
    get
    {
        return <var>;
    }
    set
    {
        // validate the input, found in value
        if ( Isvalid(value) )
```