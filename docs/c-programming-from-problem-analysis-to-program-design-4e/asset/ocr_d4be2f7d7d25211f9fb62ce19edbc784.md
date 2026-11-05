# **EXAMPLE 10.1**

```
```csharp
delegate string ReturnsSimpleString( );
```
```

When you define a `delegate` type, you identify what types of methods the `delegate` represents. This identification is accomplished through the `delegate` signature, which is very important. It indicates what the method signatures must look like if they are to be referenced by the `delegate`.

> > **NOTE**
> >
> > In C#, you can think of the `delegate` as a way of defining or naming a method signature.

Given the signature for the `delegate` defined in Example 10-1, any method that has zero parameters and returns a `string` could be referenced by the `ReturnsSimpleString` `delegate`. Example 10-2 shows the heading and body for a prospective method.

# **EXAMPLE 10.2**

```
```csharp
// Method that returns a string.
static string EndStatement( )
{
    return " in 10 years.";
}
```
```

Compare the heading for the `EndStatement( )` method shown in Example 10-2 with the `delegate` in Example 10-1. Both return strings. Both have zero parameters. The `delegate` does not specify what the statements must be in the body of the method, and it does not specify what the name of the method must be, just what the signature must look like.

> > **NOTE**
> >
> > A `delegate` is implemented in C# as a `class`; however, an instance of the `delegate` class is also referred to as a `delegate`, rather than as an object. The fact that both the `class` type and the instance type go by the same name can be confusing.

# ## Creating Delegate Instances

To associate the `delegate` with the method, a `delegate` instance is defined using the method name as the argument inside the parentheses. One way you have previously identified methods from field and property instances is by recognizing that the method name identifier is followed by a set of parentheses. When you write a method name without parentheses, you are referencing the address of the method. Example 10-3