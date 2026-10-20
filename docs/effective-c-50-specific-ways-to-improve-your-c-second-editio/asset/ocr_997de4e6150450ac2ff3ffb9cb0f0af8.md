derived from the requested type, they fail. Casts, on the other hand, can use conversion operators to convert an object to the requested type. This includes any built-in numeric conversions. Casting a long to a short can lose information.

The same problems are lurking when you cast user-defined types. Consider this type:

```
public class SecondType
{
    private MyType _value;

    // other details elided

    // Conversion operator.
    // This converts a SecondType to
    // a MyType, see item 9.
    public static implicit operator
    MyType(SecondType t)
    {
        return t._value;
    }
}
```

Suppose an object of SecondType is returned by the Factory.GetObject() function in the first code snippet:

```
object o = Factory.GetObject();
// o is a SecondType:
MyType t = o as MyType; // Fails. o is not MyType
```

```
if (t != null)
{
    // work with t, it's a MyType.
}
else
{
    // report the failure.
}
```