function methods will be left as an exercise for the reader. The technique exposed here is easily extended to support exposure of class functions as well.

Properties are the central element in our reflection system. For the sake of definitions, a property is simply a data attribute whose access is controlled by read and write accessors. Often the accessors simply return or set a protected or private variable; other times they will compute a result or change an internal state. We will start by building the system around properties from the lower layers up, adding complexity as the need arises.

# Part I: Runtime Type Information

At the most basic level, no reflection system can work without some notion of runtime type information (RTTI), or determining an object's type dynamically at runtime. While the C++ runtime's innate RTTI could be used for this purpose, using our own RTTI system will simplify the implementation of the property system, help for extensibility, and will ensure the system is optimal. While it may look like we are making a rather large detour before getting to our main topic, the implementation of our custom RTTI system will become very handy later on. We will build upon the knowledge gathered here to implement the reflection support in the second part of this gem. We will be using templates for our RTTI system as well, so this will prepare us for the template work ahead for the reflection system itself.

To be able to find the type of an object at runtime, that object must implement a virtual function overridden at each level in the class hierarchy that returns information about the type of the object. Our type information structure will contain:

+   - The name of the class
+   - A unique class ID identifying the class
+   - A pointer to the ancestor's RTTI information
+   - A function callback to a factory function

The class name will be the undecorated name of the class stored in a string. @T:The class ID is a unique user-provided 32-bit number that will be provided for effectiveness in terms of comparing class types, and in terms of serializing class type information to a file or over a network protocol.

The pointer to the ancestor RTTI is self explanatory.

The function callback will point to a factory function that will create a new instance of an object of this class type. This can be quite useful when we want to create an instance of an unknown type at runtime while only having its class ID.

The RTTI structure information should look something like this:

```
typedef DWORD ClassID;
typedef CBaseObject* (*ClassFactoryFunc)( ClassID );
const DWORD CLASSNAME_LENGTH = 32;
```