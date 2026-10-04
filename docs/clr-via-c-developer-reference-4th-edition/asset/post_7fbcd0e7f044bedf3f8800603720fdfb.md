
Note You should be aware that some of the reflection types and some of the members defined by these types are designed specifically for use by developers who are producing compilers for the CLR. Application developers don't typically use these types and members. The Framework Class Library (FCL) documentation doesn't explicitly point out which of these types and members are for developers rather than application developers, but if you realize that not all reflection types and their members are for everyone, the documentation can be less confusing.

In reality, few applications will need to use the reflection types. Reflection is used by class libraries that need to understand a type's definition in order to provide some functionality. The FCL's serialization mechanism (described in Chapter 24, "Runtime Serialization") uses reflection to determine what a type defines. The serialization formatter can then obtain the values of these types and write them into a byte stream that is used across the Internet, saving to a file, or copying to the clipboard. Similarly, Visual Studio's designers use reflection to determine which properties should be shown to developers when laying out their controls on Web Forms or Windows Forms at design.

Reflection is used when an application needs to load a specific type from a specific assembly at run time to accomplish such task. For example, an application might ask the user for the name of an assembly and a type. The application could then explicitly load the assembly, construct an instance of the type, and call methods defined in the type. This usage is conceptually similar to calling Win32 Loadlibrary GetProcAddress functions. Binding to types and calling methods in this way is referred to as late binding. (Early binding is when the types and methods used by an application are determined at compile time.)

## Reflection Performance

Reflection is an extremely powerful mechanism because it allows you to discover and use types and members at run time that you did not know at compile time. This power could come with two drawbacks:

- Reflection prevents type safety at compile time. Because reflection uses strings heavily, you lose type safety at compile time. For example, if you call Type.GetType("int"); to ask reflection to find a type called "int", the code compiles but returns at run because the CLR returns the "int" type as "System.Int32".
- Reflection is slow. When using reflection, the names of types and members are not known at compile time; you discover them at run time by using a string to identify each type and member. This means that reflection is constantly performing searches as the types in the System.Reflection namespace scan through an assembly's metadata. Often, the string searches are case-insensitive comparisons, which can slow this down even more.

Invoking member by reflection will also hurt performance. When using reflection to invoke a method, you must first package the arguments into an array; internally, reflection must unpack the arguments on the thread's stack. The CLR must check that the arguments are of the correct data type before invoking a method. Finally, the CLR ensures that the caller has the proper security permissions to access the member being invoked.

For all these reasons, it's best to avoid using reflection to access a field or invoke a method/property. If you're writing an application that will dynamically discover and construct type instances, you should take one of the following approaches:

- Have the types derive from a base type that is known at compile time. At run time, construct an instance of the derived type, place the reference in a variable that is of the base type (by way of a cast), and call virtual methods by the base type.
- Have the type implement an interface that is known at compile time. At run time, construct an instance of the type, place the reference in a variable that is of the interface type (by way of cast), and call the methods by the interface.

I prefer to using the interface technique over the base type technique because the base type technique doesn't allow the developer to choose the base type that works in a particular situation. Although the base type technique works better in versioning scenarios, because you could always add a member to the base type and the derived types just inherit; you cannot add a member to an interface without forcing all types that implement it to modify their code and compile it.

When you use either of these techniques, I strongly suggest that the interface or base type be defined in its own assembly. This will reduce versioning issues. For more information about how to do this, see the section titled "Designing an Application That Supports Add-Ins" later in this chapter.

## Discovering Types Defined in an Assembly

Reflection is frequently used to determine what types an assembly defines. The FCL opens many APIs to get this information. By far, the most commonly used API is Assembly's ExportedTypes property. Here is an example of code that loads an assembly and shows the names of all the publicly exported types in it.

```csharp
using System;
using System.Reflection;

public static class Program {
    public static void Main() {
        String dataAssembly = "System.Data,version=4.0.0.0, " +
            "culture=neutral, PublicKey=b77a5c561934e089";
        LoadAssemblyAndShowPublicTypes(dataAssembly);
    }

    private static void LoadAssemblyAndShowPublicTypes(String assem) {
        // Explicitly load an assembly in to this AppDomain
        Assembly a = Assembly.Load(assem);
    }
}
```

```csharp
// Execute this loop once for each Type
// publicly-exported from the loaded assembly
foreach (Type t in a.ExportedTypes) {
    // Display the full name of the type
    Console.WriteLine(t.FullName);
}
```

## What Exactly Is a Type Object?

Notice that the previous code iterates over a sequence of System.Type objects. The System.Type type is your starting point for doing type and object manipulations. A System.Type object represents a type reference (as opposed to a type definition).

Recall that System.Object defines a public, nonvirtual instance method named GetType. When you call this method, the CLR determines the specified object's type and returns a reference to it Type object. Because there is only one Type per type in an AppDomain, you can use equality and inequality operators to compare whether two objects are of the same type.

```csharp
private static Boolean AreSameType(Object o1, Object o2) {
    return o1.GetType() == o2.GetType();
}
```

In calling to object's GetType method, the FCL offers several ways to obtain a Type object:

- The System.Type offers several overloaded versions of the static GetType method. All versions of this type return a String. The string must specify the full name of the type (including its namespace). The primitive type names supported by the C# language (such as int, string, bool, and so) aren't alone because these names mean nothing to the CLR. If the string is simply the name of a type, the method checks the calling assembly to see whether it defines a type of the specified name. If it does, the appropriate Type object is returned.

If the calling assembly doesn't define the specified type, the types defined by MSCorLib.dll are checked. If there is a matching name still can't be found, null is returned or a System.TypeLoadException is thrown, depending on which overload of GetType you called and what parameters you passed to it. The FCL documentation fully explains this method.

You can pass an assembly-qualified type string, such as "System.Int32, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKey=b77a5c561934e089", to GetType. In this case, GetType will look for the type in the specified assembly (if necessary).

- The System.Type offers a static ReflectionOnGetType method. This method behaves similarly to the GetType method mentioned in the previous bullet, except that the type is loaded so that it can be reflected over but cannot executed.
