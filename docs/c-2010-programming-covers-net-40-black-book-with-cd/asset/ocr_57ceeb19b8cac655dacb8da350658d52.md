Table 2.4: Implicit Conversions

| From | To |
|------|----|
| short | int, long, float, double, or decimal |
| ushort | int, uint, long, ulong, float, double, or decimal |
| int | long, float, double, or decimal |
| uint | long, ulong, float, double, or decimal |
| long | float, double, or decimal |
| char | ushort, int, uint, long, ulong, float, double, or decimal |
| float | double |
| ulong | float, double, or decimal |

# Explicit Conversion/Type Casting

When one data type is converted explicitly to another data type, with the help of some pre-defined functions, it is called explicit conversion. Note that while performing explicit conversions, there are chances of data loss as such type of conversion is forceful. The following code snippet shows how to convert data types explicitly:

```
Single s = 123.45f;
int I = (int)s;
```

While converting the data types, you should know that the data type you are going to convert can be converted into the desired type or not. Table 2.5 lists the data types in the From column that C# allows to convert explicitly to the data types in the To column:

Table 2.5: Showing the Explicit Conversions

| From | To |
|------|----|
| sbyte | byte, ushort, uint, ulong, or char |
| byte | Sbyte or char |
| short | sbyte, byte, ushort, uint, ulong, or char |
| ushort | sbyte, byte, short, or char |
| int | sbyte, byte, short, ushort, uint, ulong, or char |
| uint | sbyte, byte, short, ushort, int, or char |
| long | sbyte, byte, short, ushort, int, uint, ulong, or char |
| ulong | sbyte, byte, short, ushort, int, uint, long, or char |
| char | sbyte, byte, or short |
| float | sbyte, byte, short, ushort, int, uint, long, ulong, char, or decimal |
| double | sbyte, byte, short, ushort, int, uint, long, ulong, char, float, or decimal |
| decimal | sbyte, byte, short, ushort, int, uint, long, ulong, char, float, or double |

The explicit conversion of data types may result in loss of precision or may throw unexpected exceptions. Therefore, you should always be careful while performing typecasting.

# Boxing and Unboxing

Boxing and unboxing are important concepts used in the C# type system. They are used to create a link between the two major data types in C#—value type and reference type. All value types are stored in stack, but in some situations they need to be referenced as heap. As reference types are stored in heap; therefore, you can convert the value type into reference type. This conversion is called boxing.