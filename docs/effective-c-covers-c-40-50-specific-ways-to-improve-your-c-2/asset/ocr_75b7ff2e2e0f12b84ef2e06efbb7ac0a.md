not properly copy the dValues array that was defined in Derived. When you implement ICloneable, you force all derived classes to implement it as well. In fact, you should provide a hook function to let all derived classes use your implementation (see Item 23). To support cloning, derived classes can add only member variables that are value types or reference types that implement ICloneable. That is a very stringent limitation on all derived classes. Adding ICloneable support to base classes usually creates such a burden on derived types that you should avoid implementing ICloneable in nonsealed classes.

When an entire hierarchy must implement ICloneable, you can create an abstract Clone() method and force all derived classes to implement it. In those cases, you need to define a way for the derived classes to create copies of the base members. That's done by defining a protected copy constructor:

```
```csharp
class BaseType
{
    private string label;
    private int[] values;

    protected BaseType()
    {
        label = "class name";
        values = new int[10];
    }

    // Used by derived values to clone
    protected BaseType(BaseType right)
    {
        label = right.label;
        values = right.values.Clone() as int[];
    }
}
```
```

```
```csharp
sealed class Derived : BaseType, ICloneable
{
    private double[] dValues = new double[10];

    public Derived()
    {
        dValues = new double[10];
    }
}
```
```