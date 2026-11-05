# Section 22.10: Get all the members values of an enum

```
```csharp
enum MyEnum
{
    One,
    Two,
    Three
}

foreach(MyEnum e in Enum.GetValues(typeof(MyEnum)))
    Console.WriteLine(e);
```
```

This will print:

One
Two
Three

# Section 22.11: Bitwise Manipulation using enums

The FlagsAttribute should be used whenever the enumerable represents a collection of flags, rather than a single value. The numeric value assigned to each enum value helps when manipulating enums using bitwise operators.

**Example 1 : With [Flags]**

```
```csharp
[Flags]
enum Colors
{
    Red=1,
    Blue=2,
    Green=4,
    Yellow=8
}

var color = Colors.Red | Colors.Blue;
Console.WriteLine(color.ToString());
```
```

prints Red,Blue

**Example 2 : Without [Flags]**

```
```csharp
enum Colors
{
    Red=1,
    Blue=2,
    Green=4,
    Yellow=8
}
var color = Colors.Red | Colors.Blue;
Console.WriteLine(color.ToString());
```
```

prints 3