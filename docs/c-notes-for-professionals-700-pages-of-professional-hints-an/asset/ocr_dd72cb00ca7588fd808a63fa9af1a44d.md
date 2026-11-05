```
```csharp
    All = Option1 | Option2 | Option3,
}
```
```

To avoid spelling out the decimal values of powers of two, the left-shift operator (<<) can also be used to declare the same enum

```
```csharp
[Flags]
enum FlagsEnum
{
    None = 0,
    Option1 = 1 << 0,
    Option2 = 1 << 1,
    Option3 = 1 << 2,

    Default = Option1 | Option3,
    All = Option1 | Option2 | Option3,
}
```
```

Starting with C# 7.0, binary literals can be used too.

To check if the value of enum variable has a certain flag set, the HasFlag method can be used. Let's say we have

```
```csharp
[Flags]
enum MyEnum
{
    One = 1,
    Two = 2,
    Three = 4
}
```
```

And a value

```
```csharp
var value = MyEnum.One | MyEnum.Two;
```
```

With HasFlag we can check if any of the flags is set

```
```csharp
if(value.HasFlag(MyEnum.One))
    Console.WriteLine("Enum has One");

if(value.HasFlag(MyEnum.Two))
    Console.WriteLine("Enum has Two");

if(value.HasFlag(MyEnum.Three))
    Console.WriteLine("Enum has Three");
```
```

Also we can iterate through all values of enum to get all flags that are set

```
```csharp
var type = typeof(MyEnum);
var names = Enum.GetNames(type);

foreach (var name in names)
{
    var item = (MyEnum)Enum.Parse(type, name);

    if (value.HasFlag(item))
        Console.WriteLine("Enum has " + name);
}
```
```