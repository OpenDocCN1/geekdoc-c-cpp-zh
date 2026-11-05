# Chapter 35: Dynamic type

# Section 35.1: Creating a dynamic object with properties

```
```csharp
using System;
using System.Dynamic;

dynamic info = new ExpandoObject();
info.Id = 123;
info.Another = 456;

Console.WriteLine(info.Another);
// 456

Console.WriteLine(info.DoesntExist);
// Throws RuntimeBinderException
```
```

# Section 35.2: Creating a dynamic variable

```
```csharp
dynamic foo = 123;
Console.WriteLine(foo + 234);
// 357
Console.WriteLine(foo.ToUpper())
// RuntimeBinderException, since int doesn't have a ToUpper method

foo = "123";
Console.WriteLine(foo + 234);
// 123234
Console.WriteLine(foo.ToUpper());
// NOW A STRING
```
```

# Section 35.3: Returning dynamic

```
```csharp
using System;

public static void Main()
{
    var value = GetValue();
    Console.WriteLine(value);
    // dynamics are useful!
}

private static dynamic GetValue()
{
    return "dynamics are useful!";
}
```
```

# Section 35.4: Handling Specific Types Unknown at Compile Time

The following output equivalent results:

```
```csharp
class IfElseExample
{
    public string DebugToString(object a)
    {
        if (a is StringBuilder)
```
```