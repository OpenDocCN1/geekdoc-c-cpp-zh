AllowMultiple for an attribute class is false or it is unspecified, then that attribute class is a single-use attribute class, and can be specified at most once on an entity.

The example

```
```csharp
using System;
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;
    public AuthorAttribute(string name) {
        this.name = name;
    }
    public string Name {
        get { return name; }
    }
}
```
```

defines a multi-use attribute class named AuthorAttribute. The example

```
```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```
```

shows a class declaration with two uses of the Author attribute.

AttributeUsage has another named parameter called Inherited, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class. If Inherited for an attribute class is true, then that attribute is inherited. If Inherited for an attribute class is false then that attribute is not inherited. If it is unspecified, its default value is true.

An attribute class X not having an AttributeUsage attribute attached to it, as in

```
```csharp
using System;
class X: Attribute {...}
```
```

is equivalent to the following:

```
```csharp
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```
```

# 17.1.2 Positional and named parameters

Attribute classes can have positional parameters and named parameters. Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class. Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class.

The example

```
```csharp
using System;
```
```