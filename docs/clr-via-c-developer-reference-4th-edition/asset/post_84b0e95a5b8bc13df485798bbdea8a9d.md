
of a SecureString to a String; if you do, the String lives unencrypted in the heap and will not have its characters zeroed out until the memory is reused after a garbage collection. The Secure-Class does not override the ToString method specifically to avoid exposing the sensitive data (converting it to a String would).

Here is some sample code demonstrating how to initialize and use a SecureString (when compiling, you'll need to specify the /unsafe switch with the C# compiler).

```c
using System;
using System.Security;
using System.Runtime.InteropServices;

public static class Program {
    public static void Main() {
        using (SecureString ss = new SecureString()) {
            Console.Write("Please enter password:
```

The System.Runtime.Interop.Marshal class offers five methods that you can call to decrypt a SecureString's characters into an unmanaged memory buffer. All of these methods are static, all accept a SecureString argument, and all return an IntPtr. Each of these methods has a corresponding method that you must call in order to zero the internal buffer and free it. Table 14-4 shows the System.Runtime.Interop.Marshal class's methods to decrypt a Secure-String into a memory buffer and the corresponding method to zero and free the buffer.

## TABLE 14-4- Methods of the Marshal Class for Working with Secure Strings

| Method to Decrypt SecureString to Buffer | Method to Zero and Free Buffer |
| --- | --- |
| SecureStringToBSTR | ZeroFreeBSTR |
| SecureStringToCoTaskMemAnsi | ZeroFreeCoTaskMemAnsi |
| SecureStringToCoTaskMemUnicode | ZeroFreeCoTaskMemUnicode |
| SecureStringToGlobal1AllocAnsi | ZeroFreeGlobal1AllocAnsi |
| SecureStringToGlobal1AllocUnicode | ZeroFreeGlobal1AllocUnicode |

## CHAPTER 15

## Enumerated Types and Bit Flags

- In this chapter:
- Enumerated Types ................................................................ 361
- Bit Flags ................................................................................ 367
- Adding Methods to Enumerated Types ...................................... 371

In this chapter, I'll discuss enumerated types and bit flags. Because Windows and many programming languages have used these constructs for so years, I'm sure that many of you are already familiar with how to use enumerated types and bit flags. The common language runtime (CLR) and the Framework Class Library (FCL) work together to make enumerated types and bit flags object-oriented types that offer features that I must inspect most developers aren't familiar with. It's amazing to me how these features, which are the focus of this chapter, make developing code so much easier.

## Enumerated Types

An enumerated type is a type that defines a set of symbolic name and value pairs. For example, the Color type shown here defines a set of symbols, with each symbol identifying a single color.

```c
internal enum Color {
    White // Assigned a value of 0
    Red // Assigned a value of 1
    Green // Assigned a value of 2
    Blue // Assigned a value of 3
    Orange // Assigned a value of 4
}
```

Of course, programmers can always write a program using 0 to represent white, 1 to represent red, and so on. Why use an enumerated type instead, for at least two reasons:

- Enumerated types make the program much easier to write, read, and maintain. With enumerated types, the symbolic name is used throughout the code, and the programmer doesn't have to mentally map the meaning of each hard-coded value (for example, where white is 0 or vice versa). Also, should a symbol's numeric value change, the code can be recompiled without requiring any changes to the source code. In addition, documentation tools and other utilities, such as a debugger, can show meaningful symbolic names to the programmer.

- Enumerated types are strongly typed. For example, the compiler will report an error if I attempt to pass Color.Orange as a value to a method requiring a Fruit enumerated type as a parameter.

In the Microsoft .NET Framework, enumerated types are more than just symbols the compiler cares about. Enumerated types are treated as first-class citizens in the type system, which allows for very powerful operations that can't be done with enumerated types in other environments (such as in unmanaged C++, for example).

Every enumerated type is derived from System.Enum, which is derived from System.ValueType, which in turn is derived from System.Object. So enumerated types are value types (described in Chapter S, "Primitive, Reference and Value Types") and can be represented as unboxed and boxed forms. However, unlike other value types, an enumerated type can't define any methods, properties, or events. However, you can use C#'s extension methods to simulate adding methods to an enumerated type. See the "Adding Methods to Enumerated Types" section at the end of this chapter for an example of this.

When an enumerated type is compiled, the C# compiler turns every symbol into a constant field of the type. For example, the compiler treats the Color enumeration earlier as if you had written code similar to the following:

```c
internal struct Color : System.Enum {
// Following are public constants defining Color's symbols and values
public const Color White = (Color) 0;
public const Color Red = (Color) 1;
public const Color Green = (Color) 2;
public const Color Blue = (Color) 3;
public const Color Orange = (Color) 4;

// Following is a public instance containing a Color variable's field
// You cannot write code that references this instance directly
public Int32 value__;
}
```

The C# compiler doesn't actually compile this because it forbids from defining a type derived from System.Enum. Basically, an enumerated type is just a structure with a bunch of constant fields and one instance field. The constant fields are emitted to the metadata and can be accessed via reflection. This means that you can get all the symbols associated with an enumerated type. These operations are available to you by the System base type, which offers several static and instance methods. I'll discuss some of these next.

Important Symbols defined by enumerated type are constant values. When a compiler sees code that references an enumerated type, the compiler substitutes the symbol's numeric value at compile time, and this code no longer references the enumerated type. If you have code that references the enumerated type—rather than having symbols defined by the type—the assembly containing the enumerated type will be required at runtime. Some versioning issues arise because enumerated type symbols are constants instead of read-only values. I explained these in the "Constants" section.

For example, the System.Enum has a static method GetUnderlyingType, and the System.Type has an instance method called GetUnderlyingType.

```csharp
public static Type GetUnderlyingType(Type enumType); // Defined in System.Enum
public Type GetUnderlyingType();                                 // Defined in System.Type
```

These methods use the core type to hold an enumerated type's value. Every enumerated type has an underlying type, which can be a byte, sbyte, short, int (the most common type and C# choices by default), uint, long, or long. Of course, the C# primitive types correspond to FOL. However, to make the implementation of the compiler itself, the C# compiler requires you to specify a primitive type here; using an FCL name (such as Int32) uint, long, or long expected. The following code shows how to declare an enumerated type with an underlying type of byte (System.Byte).

```csharp
internal enum Color : byte {
    White,
    Red,
    Green,
    Blue,
    Orange
}
```

With the Color enumerated type defined in this way, the following code shows what GetUnderlyingType will return.

```csharp
// The following line displays "System.Byte".
Console.WriteLine(Enum.GetUnderlyingType(typeof(Color)));
```

The C# compiler treats enumerated types as primitive types. As such, you can use many of the familiar operators (==, !=, <, >=, =, -, |, ++, --) to manipulate enumerated type instances. All of these operators actually work on the value__ instance field inside each enumerated type
