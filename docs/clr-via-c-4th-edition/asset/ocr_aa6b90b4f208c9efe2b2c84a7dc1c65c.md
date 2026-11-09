**Important** Symbols defined by an enumerated type are constant values. So when a compiler sees code that references an enumerated type's symbol, the compiler substitutes the symbol's numeric value at compile time, and this code no longer references the enumerated type that defined the symbol. This means that the assembly that defines the enumerated type may not be required at run time; it was required only when compiling. If you have code that references the enumerated type—rather than just having references to symbols defined by the type—the assembly containing the enumerated type's definition will be required at run time. Some versioning issues arise because enumerated type symbols are constants instead of read-only values. I explained these issues in the "Constants" section of Chapter 7, "Constants and Fields."

For example, the System.Enum type has a static method called GetUnderlyingType, and the System.Type type has an instance method called GetEnumUnderlyingType.

```
```csharp
public static Type GetUnderlyingType(Type enumType);      // Defined in System.Enum
public          Type GetEnumUnderlyingType();            // Defined in System.Type
```
```

These methods return the core type used to hold an enumerated type's value. Every enumerated type has an underlying type, which can be a byte, sbyte, short, ushort, int (the most common type and what C# chooses by default), uint, long, or ulong. Of course, these C# primitive types correspond to FCL types. However, to make the implementation of the compiler itself simpler, the C# compiler requires you to specify a primitive type name here; using an FCL type name (such as Int32) generates the following message: error CS1008: Type byte, sbyte, short, ushort, int, uint, long, or ulong expected. The following code shows how to declare an enumerated type with an underlying type of byte (System.Byte).

```
```csharp
internal enum Color : byte {
    White,
    Red,
    Green,
    Blue,
    Orange
}
```
```

With the Color enumerated type defined in this way, the following code shows what GetUnderlyingType will return.

```
```csharp
// The following line displays "System.Byte".
Console.WriteLine(Enum.GetUnderlyingType(typeof(Color)));
```
```

The C# compiler treats enumerated types as primitive types. As such, you can use many of the familiar operators (==, !=, <, >, <=, >=, +, -, ^, &, |, ~, ++, and --) to manipulate enumerated type instances. All of these operators actually work on the value__ instance field inside each enumerated