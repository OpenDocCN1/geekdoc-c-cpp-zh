from the second type. A derived class is syntactically substitutable for its base class because there’s a natural implicit conversion from a specific type to any of its parent types.

We can implement our own type conversions to mimic substitutability between two otherwise unrelated types. Casting—or coercing—a variable to a different type can be convenient, whether via implicit or explicit conversions, but doing so may mask problems beneath the surface. However, applied carefully, conversions between unrelated types can be an effective and concise way to express a design.

To demonstrate some of the problems with implicit conversions that we haven’t yet explored, Listing 7-33 implements an implicit conversion operator in TranslucentColor to convert an instance to a Color type.

```
public readonly record struct TranslucentColor(Color Color, int Alpha)
{
    --snip--
    public static implicit operator Color(TranslucentColor color)
        => color.Color;
}
```

Listing 7-33: Implicit conversion operator

The conversion operator in TranslucentColor is an outward conversion: we’re converting from an instance of the implementing type to something else. It will allow us to call a method expecting a Color value when we have a TranslucentColor at hand, as we do when we call the EqualViaColor method in Listing 7-34.

```
public bool EqualViaColor(Color left, Color right)
    => left.Equals(right);

var red = new TranslucentColor(0xFF, 0, 0, 0);
var blue = new TranslucentColor(0, 0, 0xFF, 0);

Assert.That(EqualViaColor(red, blue), Is.False);
```

Listing 7-34: Implicit conversions in action

Owing to the implicit conversion operator, the red and blue variables are converted to Color instances when we pass them as arguments to the EqualViaColor method. The conversion happens invisibly because the conversion operator is defined as implicit.

We could achieve the same effect by defining an inward conversion operator on the Color type taking a TranslucentColor parameter. The difference is merely about where we choose to define the operator. Since TranslucentColor already depends on the Color type, and Color otherwise has no knowledge of TranslucentColor, the outward conversion defined in TranslucentColor makes better sense here.

However, we must be careful with all conversions, especially implicit ones. As you saw in Chapter 1, implicit conversions may hide complexity