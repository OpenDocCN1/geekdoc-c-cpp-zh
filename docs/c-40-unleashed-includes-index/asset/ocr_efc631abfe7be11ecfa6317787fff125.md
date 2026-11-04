The declaration of a constant uses the `const` keyword and cannot include the `static` keyword. The value supplied to the constant should permit to be fully evaluated at compile time. This includes primitive types like numbers and Booleans, string literals, and null references for reference types. Calling a constructor (or another other kind of method) is not permitted because it would involve runtime execution of code.

When using a constant, the compiler copies its value verbatim to the use site. For example, consider the following piece of code used to calculate the surface of a circle:

```
```csharp
class Circle
{
    private double _radius;

    public Circle(double radius)
    {
        _radius = radius;
    }

    public double Surface()
    {
        return Math.PI * _radius * _radius;
    }
}
```
```

Looking in `Reflector` for the `Surface` method, we see no trace whatsoever of `Math.PI`. Figure 11.7 shows how the constant got burned into the use site at compile time.

![](bbox=[0.069, 0.623, 0.41, 0.693])

Because constants are copied to places where they're used, you cannot change a constant after it's been exposed. For example, if the .NET Framework developers were to change the value of Pi (and no, they don't have such a mandate, contrary to the stories about American states trying to legislate the value of Pi in the late 1800s), every application that picked up the original value would have to be recompiled. This is in contrast to (static) read-only fields, which are accessed at runtime:

```
```csharp
class IndianaMath
{
    public static readonly double PI = 3.2;
}
```
```