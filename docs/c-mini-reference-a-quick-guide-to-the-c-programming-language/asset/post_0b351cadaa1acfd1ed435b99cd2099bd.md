
⑤ The method argument `a` in this call is called the "non-trailing named argument" because it precedes a positional argument, `'d'` (for example).

⑥ Both `a` and `b` in this call must use the named argument syntax.

## 9.3. The `params` Parameter

The last parameter in a formal parameter list in C# can be a `params` array parameter, which consists of

- Optional
- The `params` keyword
- A one-dimensional array type, and
- A parameter name.

The `params` parameter is a value parameter. (But note that an array is a reference type.) In a method invocation, an argument for the `params` parameter can be specified either as an array value or as zero, one, or more arguments of the array’s element type. For example, given the following function,

```csharp
static int AddAll(params int[] operands) => operands.Sum();
```

It can be called with an int array argument,

```csharp
var ints = new int[] { 1, 2, 3 };
var sum1 = AddAll(ints);
Console.WriteLine($"sum = {sum1}");
```

## 9.4. Value Parameters

A formal parameter declared without any parameter modifiers is a value parameter by default. A value parameter corresponds to a local variable that gets its initial value from the corresponding argument supplied in the function. The argument therefore should be an expression that is implicitly convertible to the parameter type.

## 9.5. `in` Parameters

Parameters with the `in` or `ref` modifiers are passed by reference. The `in` keyword specifies that the called method does not modify the value. An `in` parameter corresponds to a local `ref readonly`. The `in` parameter is declared using the `in` modifier in the parameter specification, and it can include a default value. For example,

```csharp
static void PrintCoord(in Coord cord) =>
    Console.WriteLine($"Lat = {cord.Lat}; Lon = {cord.Lon}");
record struct Coord(float Lat, float Lon);
```

① The `in` parameter `cord` uses the call-by-reference semantics. The `PrintCoord` function cannot modify its value.

This function can be called with or without the `in` keyword.

```csharp
var coord = new Coord(40.0f, -100.0f);
PrintCoord(coord);
PrintCoord(in coord);
```

Although it uses reference semantics, it cannot change the value of the `in` argument. Therefore, one can expect certain performance increase without having to worry about data mutability.

## 9.6. `out` Parameters

A parameter declared with the `out` modifier is an output parameter. The corresponding argument is passed by reference. For example,

```csharp
static void SetCoord(out Coord c) =>
    c = new(0.0f, 0.0f);
```

① The `out` parameter cannot be referenced before it is assigned, and it must be assigned a value before the function returns.

To use an `out` parameter, both the method definition and the calling method must explicitly use the `out` keyword. You can declare a new `out` variable in the argument list of a method invocation. For instance,

```csharp
SetCoord(out var c);
Console.WriteLine($"Lat = {c.Lat}; Lon = {c.Lon}");
```

① We can also use the explicit type, e.g., `SetCoord(out Coord c)`. This is more or less equivalent to `Coord c; SetCoord(out c);`.

## 9.8. Returns by Reference

### 9.8.1. Ref returns

C# methods, by default, return values in the similar way that arguments are passed by value. In contrast, `ref` returns are values that a method returns by reference to the caller. That is, instead of copying the value returned by a method, its reference is returned. (Or, more precisely, its reference is copied.) There are three aspects for the `ref` returns to work.

The return type in the method signature needs to be prefixed with `ref`. For example, `public ref MyStruct`.

The expression of the `return` statement in the method body needs to be marked as `ref`. For example, `return ref`.

In order for the caller to modify the object's state, the `ref` return value needs to be assigned to a `ref` local.

### 9.8.2. Ref readonly returns

The called method may also declare the return value as `ref readonly` to return the value by reference, and at the same time enforce that the calling code cannot modify the returned value. The calling method can avoid copying the returned value by storing the value in a local `ref readonly`. For example,

```csharp
static class RefReturnDemo {
    static ref readonly Coord Move(ref Coord moving) =>
        ref moving; // return ref
    public static void PrintAfterMove(Coord here) {
        ref readonly var t = ref Move(ref here);
        Console.WriteLine($"Lat = {t.Lat}; Lon = {t.Lon}");
    }
}
```

## 10. Built-in Value Types

We will go through a few simple types in this chapter. The built-in `string` type is discussed in the next chapter.

## 10.1. The `bool` Type

The C# `bool` type is an alias for the .NET `System.Boolean` struct type, whose value can be either `true` or `false`. The default value of the `bool` type is `false`. That is, `default(bool)` returns `false`.

### 10.1.1. The nullable `bool?` type

The nullable `bool?` type can be used for the three-valued logic, for example, when you work with databases that support a three-valued Boolean type. The predefined `&` and `|` operators support the three-valued logic for the `bool?` operands.

## 10.2. The `char` Type

The C# `char` type is an alias for the .NET `System.Char` struct type, which represents a Unicode character in UTF-16 encoding. The default value of the `char` type is `'\0'`; that is, `default(char)` returns `'\0'`.

### 10.2.1. Char literals

You can specify a `char` value with:

- A character literal.
- A Unicode escape sequence; or
- A hexadecimal escape sequence, e.g., `\x` followed by the hexadecimal representation of a character code.

## 10.3. Integral Types

C# supports 11 integral types: four unsigned integer types and four signed integer types, which are represented using two’s complement format. The `char` type is also an integral type. In addition, C# includes two native integer types, `nint` and `nuint`.

| Type | Description |
| --- | --- |
| `byte` | Unsigned 8-bit integers with values from 0 to 255 |
| `sbyte` | Signed 8-bit integers with values from -128 to 127 |
| `ushort` | Unsigned 16-bit integers with values from 0 to 65535. |
| `short` | Signed 16-bit integers with values from -32768 to 32767. |
| `uint` | Unsigned 32-bit integers with values from 0 to 4294967295. |
| `int` | Signed 32-bit integers with values from -2147483648 to 2147483647. |
| `ulong` | Unsigned 64-bit integers with values from 0 to 18446744073709551615. |
| `long` | Signed 64-bit integers with values from -9223372036854775808 to 9223372036854775807. |

The `checked` and `unchecked` operators and statements are used to control overflow checking for integral-type arithmetic operations and conversions.

## 10.4. Native Integer Types

C# now includes two new contextual keywords, `nint` and `nuint`, which represent native signed and native unsigned integer types, respectively, which are intended for use in low-level libraries. These contextual keywords are only treated as keywords when name lookup does not find a viable result at that program location.

The C# types `nint` and `nuint` correspond to the underlying .NET types `System.IntPtr` and `System.UIntPtr`, respectively, with compiler support for additional conversions and operations for those types as native integer types on a specific platform, or operating system.

## 10.5. Floating Point Types

C# supports two floating-point types, `float` and `double`, which are represented using the 32-bit single-precision and 64-bit double-precision IEC 60559 formats, respectively. Floating point number literals are described in the Lexical Analysis chapter.

## 10.6. The `decimal` Type

The `decimal` type is a 128-bit real number type, suitable for high-precision calculations. Internally a `decimal` is represented as an integer scaled by a power of ten. Decimal numbers are guaranteed to have at least 28-digit precision. The `decimal` type has greater precision but may have a smaller range than the floating-point types.

If a `decimal` arithmetic operation produces a result whose magnitude is too large for a `decimal`, a `System.OverflowException` is thrown.
