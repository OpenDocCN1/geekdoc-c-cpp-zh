

```csharp
// i and j are both of type int
i = 20;
j = i;
```

However, consider the following example. For this code, assume you have defined a class called Vector and that Vector is a reference type and has an int member variable called Value:

```csharp
Vector x, y;
x = new Vector();
x.Value = 30; // Value is a field defined in Vector class
y = x;
WriteLine(y.Value);
y.Value = 50;
WriteLine(x.Value);
```

The crucial point to understand is that after executing this code, there is only one Vector object: x and y both point to the memory location that contains this object. Because x and y are variables of a reference type, declaring each variable simply reserves a reference—it doesn’t instantiate an object of the given type. In neither case is an object actually created. To create an object, you have to use the new keyword, as shown. Because x and y refer to the same object, changes made to x will affect y and vice versa. Hence, the code will display 30 and then 50.

If a variable is a reference, it is possible to indicate that it does not refer to any object by setting its value to null:

```csharp
y = null;
```

If a reference is set to null, then clearly it is not possible to call any nonstatic member functions or fields against it; doing so would cause an exception to be thrown at runtime.

In C#, basic data types such as bool and long are value types. This means that if you declare a bool variable and assign it the value of another bool variable, you will have two separate bool values in memory. Later, if you change the value of the original bool variable, the value of the second bool variable does not change. These types are copied by value.

In contrast, most of the more complex C# data types, including classes that you yourself declare, are reference types. They are allocated upon the heap, have lifetimes that can span multiple function calls, and can be accessed through one or several aliases. The CLR implements an elaborate algorithm to track which reference variables are still reachable and which have been orphaned. Periodically, the CLR destroys orphaned objects and returns the memory that they once occupied back to the operating system. This is done by the garbage collector.

C# has been designed this way because high performance is best served by keeping primitive types (such as int and bool) as value types, and larger types that contain many fields (as is usually the case with classes) as reference types. If you want to define your own type as a value type, you should declare it as a struct.

## .NET Types

The C# keywords for data types—such as `int`, `short`, and `string`—are mapped from the compiler to .NET data types. For example, when you declare an `int` in C#, you are actually declaring an instance of a .NET struct: `System.Int32`. This might sound like a small point, but it has a profound significance: It means that you can treat all the primitive data types syntactically, as if they are classes that support certain methods. For example, to convert an `int i` to a `string`, you can write the following:

```csharp
string s = i.ToString();
```

It should be emphasized that behind this syntactical convenience, the types really are stored as primitive types, so absolutely no performance cost is associated with the idea that the primitive types are notionally represented by .NET structs.

The following sections review the types that are recognized as built-in types in C#. Each type is listed, along with its definition and the name of the corresponding .NET type. C# has 15 predefined types, 13 value types, and 2 (`string` and `object`) reference types.

### Predefined Value Types

The built-in .NET value types represent primitives, such as integer and floating-point numbers, character, and Boolean types.

#### Integer Types

C# supports eight predefined integer types, shown in the following table.

| Name | .NET Type | Description | Range (min:max) |
|------|-----------|-------------|-----------------|
| `sbyte` | `System.SByte` | 8-bit signed integer | −128:127 (−2⁷:2⁷−1) |
| `short` | `System.Int16` | 16-bit signed integer | −32,768:32,767 (−2¹⁵:2¹⁵−1) |
| `int` | `System.Int32` | 32-bit signed integer | −2,147,483,648:2,147,483,647 (−2³¹:2³¹−1) |
| `long` | `System.Int64` | 64-bit signed integer | −9,223,372,036,854,775,808:9,223,372,036,854,775,807 (−2⁶³:2⁶³−1) |
| `byte` | `System.Byte` | 8-bit unsigned integer | 0:255 (0:2⁸−1) |
| `ushort` | `System.UInt16` | 16-bit unsigned integer | 0:65,535 (0:2¹⁶−1) |
| `uint` | `System.UInt32` | 32-bit unsigned integer | 0:4,294,967,295 (0:2³²−1) |
| `ulong` | `System.UInt64` | 64-bit unsigned integer | 0:18,446,744,073,709,551,615 (0:2⁶⁴−1) |

Some C# types have the same names as C++ and Java types but have different definitions. For example, in C# an `int` is always a 32-bit signed integer. In C++ an `int` is a signed integer, but the number of bits is platform-dependent (32 bits on Windows). In C#, all data types have been defined in a platform-independent manner to allow for the possible future porting of C# and .NET to other platforms.

A `byte` is the standard 8-bit type for values in the range 0 to 255 inclusive. Be aware that, in keeping with its emphasis on type safety, C# regards the `byte` type and the `char` type as completely distinct types, and any programmatic conversions between the two must be explicitly requested. Also be aware that unlike the other types in the integer family, a `byte` type is by default unsigned. Its signed version bears the special name `sbyte`.

With .NET, a `short` is no longer quite so short; it is now 16 bits long. The `int` type is 32 bits long. The `long` type reserves 64 bits for values. All integer-type variables can be assigned values in decimal or hex notation. The latter requires the `0x` prefix:

```csharp
long x = 0x12ab;
```

If there is any ambiguity about whether an integer is `int`, `uint`, `long`, or `ulong`, it defaults to an `int`. To specify which of the other integer types the value should take, you can append one of the following characters to the number:

```csharp
uint ui = 1234U;
long l = 1234L;
ulong ul = 1234UL;
```

You can also use lowercase u and l, although the latter could be confused with the integer 1 (one).

### Floating-Point Types

Although C# provides a plethora of integer data types, it supports floating-point types as well.

| Name | .NET Type | Description | Significant Figures | Range (Approximate) |
|------|-----------|-------------|---------------------|---------------------|
| `float` | `System.Single` | 32-bit, single-precision floating point | 7 | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ |
| `double` | `System.Double` | 64-bit, double-precision floating point | 15/16 | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ |

The float data type is for smaller floating-point values, for which less precision is required. The double data type is bulkier than the float data type but offers twice the precision (15 digits).

If you hard-code a non-integer number (such as 12.3), the compiler will normally assume that you want the number interpreted as a double. To specify that the value is a float, append the character F (or f) to it:

```csharp
float f = 12.3F;
```

### The Decimal Type

The decimal type represents higher-precision floating-point numbers, as shown in the following table.

| Name | .NET Type | Description | Significant Figures | Range (Approximate) |
|------|-----------|-------------|---------------------|---------------------|
| `decimal` | `System.Decimal` | 128-bit, high-precision decimal notation | 28 | ±1.0 × 10⁻²⁸ to ±7.9 × 10²⁸ |

One of the great things about the .NET and C# data types is the provision of a dedicated decimal type for financial calculations. How you use the 28 digits that the decimal type provides is up to you. In other words, you can track smaller dollar amounts with greater accuracy for cents or larger dollar amounts with more rounding in the fractional portion. Bear in mind, however, that decimal is not implemented under the hood as a primitive type, so using `decimal` has a performance effect on your calculations.

To specify that your number is a `decimal` type rather than a `double`, a `float`, or an integer, you can append the `M` (or `m`) character to the value, as shown here:

```csharp
decimal d = 12.30M;
```

### The Boolean Type

The C# `bool` type is used to contain Boolean values of either `true` or `false`.

| Name | .NET Type | Description | Significant Figures | Range |
|------|-----------|-------------|---------------------|-------|
| `bool` | `System.Boolean` | Represents true or false | NA | true or false |

You cannot implicitly convert `bool` values to and from integer values. If a variable (or a function return type) is declared as a `bool`, you can only use values of `true` and `false`. You get an error if you try to use zero for `false` and a nonzero value for `true`.

### The Character Type

For storing the value of a single character, C# supports the `char` data type.

| Name | .NET Type | Values |
|------|-----------|--------|
| `char` | `System.Char` | Represents a single 16-bit (Unicode) character |

Literals of type `char` are signified by being enclosed in single quotation marks—for example, `'A'`. If you try to enclose a character in double quotation marks, the compiler treats the character as a string and throws an error.

As well as representing `chars` as character literals, you can represent them with four-digit hex Unicode values (for example, `'\u0041'`), as integer values with a cast (for example, `(char)65`), or as hexadecimal values (for example, `'\x0041'`). You can also represent them with an escape sequence, as shown in the following table.

