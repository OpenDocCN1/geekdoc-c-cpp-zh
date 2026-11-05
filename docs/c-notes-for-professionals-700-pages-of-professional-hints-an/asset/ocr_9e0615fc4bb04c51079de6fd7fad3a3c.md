# Chapter 86: Properties

# Section 86.1: Auto-implemented properties

Auto-implemented properties were introduced in C# 3.

An auto-implemented property is declared with an empty getter and setter (accessors):

```
public bool IsValid { get; set; }
```

When an auto-implemented property is written in your code, the compiler creates a private anonymous field that can only be accessed through the property's accessors.

The above auto-implemented property statement is equivalent to writing this lengthy code:

```
private bool _isValid;
public bool IsValid
{
    get { return _isValid; }
    set { _isValid = value; }
}
```

Auto-implemented properties cannot have any logic in their accessors, for example:

```
public bool IsValid { get; set { PropertyChanged("IsValid"); } } // Invalid code
```

An auto-implemented property can however have different access modifiers for its accessors:

```
public bool IsValid { get; private set; }
```

C# 6 allows auto-implemented properties to have no setter at all (making it immutable, since its value can be set only inside the constructor or hard coded):

```
public bool IsValid { get; }
public bool IsValid { get; } = true;
```

For more information on initializing auto-implemented properties, read the Auto-property initializers documentation.

# Section 86.2: Default Values for Properties

Setting a default value can be done by using Initializers (C#6)

```
public class Name
{
    public string First { get; set; } = "James";
    public string Last { get; set; } = "Smith";
}
```

If it is read only you can return values like this:

```
public class Name
{
    public string First => "James";
    public string Last => "Smith";
}
```