Unboxing, the reverse of boxing, copies the value inside a box on the heap into an instance of its original value type. Unboxing must always be done explicitly and is syntactically the same as an explicit cast from the boxed value to the target type, as shown in Listing 4-11.

```
var original = new Coordinate( --snip-- );
object box = original.Clone();

Coordinate clone = (Coordinate)box;
```

Listing 4-11: Unboxing to the original type

When a value type implements one or more interfaces, instances can also be referred to by a variable of any of those interface types, and this also requires the instance to be boxed.

# To an Interface

A value can be boxed only when it can be implicitly converted to the target reference type. Since all value types are sealed—meaning inheritance is prohibited—that valid conversion can be to an object variable reference, a System.ValueType (which itself is not a value type), or an interface implemented by the value type. If the value is an enum member, it can also be converted to the System.Enum class or any of the interfaces implemented by System.Enum.

We need a direct object reference to a value in only a very few cases, and there’s no excuse for boxing to a System.ValueType, except perhaps for purely didactic examples. A value type variable can implicitly convert to any interface implemented by the type, such as the IComparable interface implemented by the Color struct in Listing 4-12.

```
public readonly struct Color : IComparable<Color>
{
    public Color(uint val) => rgb = val;

    int IComparable<Color>.CompareTo(Color other)
        => rgb.CompareTo(other.rgb);

    private readonly uint rgb;
}
```

Listing 4-12: The IComparable interface implemented by the Color struct

The IComparable<T> interface specifies a single method named CompareTo, in which we define the comparison operation allowing collections of T to be sorted. The implementation for Color here simply defers to its uint field, which implements the IComparable<uint> interface.

Note that the implementation of IComparable<Color>.CompareTo is an explicit implementation, meaning we can invoke CompareTo only by using a reference to the interface type. Any attempt to call CompareTo directly on a Color variable results in a compile error. If we cast a Color variable