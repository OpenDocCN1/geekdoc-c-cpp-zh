
WinRT. Consequently, UWP apps have access to only a reduced subset of the types and methods provided by the .NET Framework 4.6. (IntelliSense in Visual Studio 2015 automatically shows the restricted view of available features when you use C# to build UWP apps, omitting the types and methods not available through WinRT.)

On the other hand, WinRT provides a significant set of features and types that have no direct equivalent in the .NET Framework or that operate in a significantly different way to the corresponding features in the .NET Framework, and so cannot easily be translated. WinRT makes these features available to the CLR through a mapping layer that makes them look like .NET Framework types and methods, and you can invoke them directly from managed code.

So, integration implemented by the CLR and WinRT enables the CLR to transparently use WinRT types, but it also supports interoperability in the reverse direction: you can define types by using managed code and make them available to unmanaged applications as long as these types conform to the expectations of WinRT. Chapter 9 highlights the requirements of structs in this respect (instance and static methods in structs are not available through WinRT, and private fields are unsupported). If you are building classes with the intention that they be consumed by unmanaged applications through WinRT, your classes must follow these rules:

- Any public fields, and the parameters and return values of any public methods, must be WinRT types or .NET Framework types that can be transparently translated by WinRT into WinRT types. Examples of supported .NET Framework types include conforming value types (such as structs and enums) and those corresponding to the C# primitives (int, long, float, double, string, and so on). Private fields are supported in classes, and they can be of any type available in the .NET Framework; they do not have to conform to WinRT.
- Classes cannot override methods of System.Object other than ToString, and they cannot declare protected constructors.
- The namespace in which a class is defined must be the same as the name of the assembly implementing the class. Additionally, the namespace name (and therefore the assembly name) must not begin with “Windows”.
- You cannot inherit from managed types in unmanaged applications through WinRT. Therefore, all public classes must be sealed. If you need to implement polymorphism, you can create a public interface and implement that interface on the classes that must be polymorphic.
- You can throw any exception type that is included in the subset of the .NET Framework available to UWP apps; you cannot create your own custom exception classes. If your code throws an unhandled exception when called from an unmanaged application, WinRT raises an equivalent exception in the unmanaged code.

WinRT has other requirements concerning features of C# code covered later in this book. These requirements will be highlighted as each feature is described.

## Summary

In this chapter, you saw how to define and implement interfaces and abstract classes. The following table summarizes the various valid (yes), and invalid (no) keyword combinations when defining methods for interfaces, classes, and structs.

| Keyword | Interface | Abstract class | Class | Sealed class | Structure |
|---|---|---|---|---|---|
| abstract | No | Yes | No | No | No |
| new | Yes¹ | Yes | Yes | Yes | No² |
| override | No | Yes | Yes | Yes | No³ |
| private | No | Yes | Yes | Yes | Yes |
| protected | No | Yes | Yes | Yes | No⁴ |
| public | No | Yes | Yes | Yes | Yes |
| sealed | No | Yes | Yes | Yes | No |
| virtual | No | Yes | Yes | No | No |

1 An interface can extend another interface and introduce a new method with the same signature.
2 Structures do not support inheritance, so they cannot hide methods.
3 Structures do not support inheritance, so they cannot override methods.
4 Structures do not support inheritance; a structure is implicitly sealed and cannot be derived from.

If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 14.

- ■ If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Declare an interface | Use the *interface* keyword. For example:
```
interface IDemo
{
    string GetName();
    string GetDescription();
}
``` |
| Implement an interface | Declare a class by using the same syntax as class inheritance, and then implement all the member functions of the interface. For example:
```
class Test : IDemo
{
    public string IDemo.GetName()
    {
        ...
    }

    public string IDemo.GetDescription()
    {
        ...
    }
}
``` |
| Create an abstract class that can be used only as a base class, containing abstract methods | Declare the class by using the *abstract* keyword. For each abstract method, declare the method with the *abstract* keyword and without a method body. For example:
```
abstract class GrazingMammal
{
    abstract void DigestGrass();
    ...
}
``` |
| Create a sealed class that cannot be used as a base class | Declare the class by using the *sealed* keyword. For example:
```
sealed class Horse
{
    ...
}
``` |

## Chapter 14. Using garbage collection and resource management

After completing this chapter, you will be able to:

- Manage system resources by using garbage collection.
- Write code that runs when an object is destroyed.
- Release a resource at a known point in time in an exception-safe manner by writing a try/finally statement.
- Release a resource at a known point in time in an exception-safe manner by writing a using statement.
- Implement the IDisposable interface to support exception-safe disposal in a class.

You have seen in earlier chapters how to create variables and objects, and you should understand how memory is allocated when you create variables and objects. (In case you don’t remember, value types are created on the stack, and reference types are allocated memory from the heap.) Computers do not have infinite amounts of memory, so memory must be reclaimed when a variable or an object no longer needs it. Value types are destroyed and their memory reclaimed when they go out of scope. That’s the easy bit. How about reference types? You create an object by using the new keyword, but how and when is an object destroyed? That’s what this chapter is all about.

### The life and times of an object

First, let’s recap what happens when you create an object.

You create an object by using the new operator. The following example creates a new instance of the Square class that is discussed in Chapter 13, “Creating interfaces and defining abstract classes”

Click here to view code image

```
int sizeOfSquare = 99;
Square mySquare = new Square(sizeOfSquare); // Square is a reference type
```

From your point of view, the new operation is a single step, but underneath, object creation is really a two-phase process:

1. The new operation allocates a chunk of raw memory from the heap. You have no control over this phase of an object’s creation.
2. The new operation converts the chunk of raw memory to an object; it has to initialize the object. You can control this phase by using a constructor.

### Note

If you are a C++ programmer, you should note that in C#, you cannot overload the *new* operation to control allocation.

After you create an object, you can access its members by using the dot operator (.). For example, the *Square* class includes a method named *Draw* that you can call:

```
mySquare.Draw();
```

### Note

This code is based on the version of the *Square* class that inherits from the *DrawingShape* abstract class and does not implement the *IDraw* interface explicitly. For more information, refer to Chapter 13.

When the *mySquare* variable goes out of scope, the *Square* object is no longer being actively referenced. The object can then be destroyed, and the memory that it is using can be reclaimed. (This might not happen immediately, however, as you will see later.) Like object creation, object destruction is a two-phase process. The two phases of destruction exactly mirror the two phases of creation:

1. The common language runtime (CLR) must perform some tidying up. You can control this by writing a *destructor*.
2. The CLR must return the memory previously belonging to the object back to the heap; the memory that the object lived in must be deallocated. You have no control over this phase.

The process of destroying an object and returning memory back to the heap is known as *garbage collection*.

### Note

If you program in C++, keep in mind that C# does not have a delete operator. The CLR controls when an object is destroyed.

### Writing destructors

You can use a destructor to perform any tidying up that’s required when an object is garbage collected. The CLR will automatically clear up any managed resources that an object uses, so in many of these cases, writing a destructor is unnecessary.
