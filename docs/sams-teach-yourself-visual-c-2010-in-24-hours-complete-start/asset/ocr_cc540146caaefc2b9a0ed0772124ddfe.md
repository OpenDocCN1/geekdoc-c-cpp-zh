whether an attribute applies to a method, its parameter, or its return value, as shown in Listing 20.4.

# LISTING 20.4  Attribute Parameters

```
```csharp
[CustomAttribute]
string Method()
{
    return String.Empty;
}

[method: CustomAttribute]
string Method()
{
    return String.Empty;
}

[return: CustomAttribute]
string Method()
{
    return String.Empty;
}
```
```

# # Working with the Common Attributes

The .NET Framework defines many attributes that you can use in your own applications. The most common ones are the *Obsolete* attribute, the *Conditional* attribute, and the set of global attributes.

# ## The Obsolete Attribute

The *Obsolete* attribute indicates that a code declaration should no longer be used and causes the compiler to generate a warning or error, depending on how the attribute is configured. This attribute can be used with no parameters, but it is recommended to supply an explanation and indicate if a compiler warning or error should be generated. Listing 20.5 shows an example of using the *Obsolete* attribute.

# LISTING 20.5  Obsolete Attribute

```
```csharp
public class Example
{
    [Obsolete("Consider using OtherMethod instead.", false)]
    public string Method()
    {
        return String.Empty;
    }
}
```
```