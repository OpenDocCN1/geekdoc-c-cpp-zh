and can even lead to undesired behavior. A user-defined coercion is not quite the same as the implicit reference conversion from a derived type to its base type.

# Widening vs. Narrowing Conversions

When TranslucentColor inherited from Color, we could pass a TranslucentColor reference to a method expecting a Color, but it was still a reference to the same instance of a TranslucentColor, and only a copy of the reference would be made. In Listing 7-33, TranslucentColor and Color are record structs and therefore value types. When we invoke the conversion operator of TranslucentColor, we’re simply creating a new Color instance, so the copy has lost some of the information specific to TranslucentColor—namely, the Alpha property.

A conversion from a derived class reference to a base class reference is a widening conversion. We can refer to a specific instance by using a more general (base) type, but no loss of information occurs. We’re still able to explicitly cast the base class reference back to the original derived instance, although that’s a relatively expensive run-time operation. Our implicit conversion from a TranslucentColor struct to a Color via our own operator method is narrowing: neither type is really more specific or general than the other, and they’re independent values, but the act of conversion loses information.

While we’ve replicated the behavior of converting from a derived class to a base class, it doesn’t give us the same flexibility. The converted value really is just a Color, and we need other means of capturing the extra properties of a TranslucentColor if we need to reinstate them.

Conversions aren’t appropriate for trying to replicate the characteristics of inheritance, but they can be useful for other scenarios.

# For Representation

Conversions between unrelated types make more sense when the types have a common meaning with different representation. For instance, we might need to use an external API that uses the common int representation of the hexadecimal RGB value of colors. Changing a value’s representation is usually better implemented as an explicit rather than implicit conversion, as shown in Listing 7-35. However, any conversions—whether explicit or implicit—require careful consideration of alternate approaches.

```
public readonly struct Color
{
    --snip--
    public static explicit operator int(Color color)
        => color.Red << 16 | color.Green << 8 | color.Blue;
}
```

Listing 7-35: Converting to a different type representation