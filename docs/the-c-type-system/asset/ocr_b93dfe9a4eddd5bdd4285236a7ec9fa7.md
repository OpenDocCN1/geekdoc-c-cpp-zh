to the IComparable<Color> interface, the value will be boxed into an IComparable<Color> reference, as in Listing 4-13.

```
var red = new Color(0xFF0000);
var green = new Color(0x00FF00);

IComparable<Color> compare = red;
var less = compare.CompareTo(green);
```

Listing 4-13: Explicitly boxing to an interface type

When we initialize this compare variable, the value of red is boxed, because variables of any interface type are references. We could avoid the box by making CompareTo nonexplicit, allowing us to call it directly using the red variable without casting to the interface. That’s not to say that we should prefer nonexplicit implementations; explicit interface methods are a good way to segregate the public interface of a type.

We can call an explicit interface implementation by using a generic type parameter that has been constrained to the interface type. In this case, no cast is needed, and no boxing takes place. To demonstrate, the generic LessThan method in Listing 4-14 doesn’t box its parameters, even when we pass Color values as arguments for it, because the generic parameter T is constrained to the IComparable<T> interface.

```
public static bool LessThan<T>(T left, T right)
    where T : IComparable<T>
{
    return left.CompareTo(right) < 0;
}

var red = new Color(0xFF0000);
var green = new Color(0x00FF00);

Assert.That(LessThan(green, red), Is.True);
```

Listing 4-14: Constraining the generic type parameter T to the IComparable<T> interface type

When a generic type parameter is constrained in this way, a variable of the generic type is considered to be of the type used for the constraint. In this example, left is used as if it were an IComparable<T> variable. We can invoke the method directly on whatever value T represents, even when the implementing method is an explicit implementation.

# In Method Calls

Boxing a value type instance by assigning it to a reference variable is often conspicuous in our code, but boxing also occurs when we pass a value type instance as an argument for a reference type method parameter. As with assigning to a reference variable, the value is boxed implicitly if an implicit conversion to the type of the parameter exists. Since boxing is usually