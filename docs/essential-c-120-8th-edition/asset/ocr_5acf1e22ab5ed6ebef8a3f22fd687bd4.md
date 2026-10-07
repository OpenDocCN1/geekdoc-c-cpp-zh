# Covariance and Contravariance

A question often asked by new users of generic types is why an expression of type List<string> may not be assigned to a variable of type List<object>: If a string may be converted to type object, surely a list of strings is similarly compatible with a list of objects. In reality, this is not. Generally speaking, either type-safe or legal. If you declare two variables with different type parameters using the same generic class, the variables are not type-compatible, even if they are assigning from a more specific type to a more generic type—in other words, they are not covariant.

Covariant is a technical term from category theory, but its underlying idea is straightforward: Suppose two X and Y have a special relationship—namely, every value of the type X may be converted to the type Y. If the I<X> and ICY> also have that special relationship, we say, “I<T> is covariant in T.” When dealing with generic types with only one type parameter, the type parameter can be understood such that when we say, “I<T> is covariant.” The conversion from I<X> to ICY is called a covariant conversion.

For example, two instances of a generic class, Pair<Contact> and Pair<PdaItem>, are not type-compatible even when the type arguments are themselves compatible. In other words, the compiler prevents the conversion (implicit or explicit) of Pair<Contact> to Pair<PdaItem>, even though Contact derives from PdaItem. Similarly, converting Pair<Contact> to the interface type IPair<PdaItem> will fail. See Listing 12.40 for an example.

# Listing 12.40: Conversion between Generics with Different Type Parameters

```
// ...
// Error: Cannot convert type
Pair<PdaItem> pair = (Pair<PdaItem>)new Pair<Contact>();nIPair<PdaItem> duple = (IPair<PdaItem>)new Pair<Contact>();
```

But why is this not legal? Why are List<T> and Pair<T> not covariant? Listing 12.41 shows what would happen if the C# language allowed unrestricted generic covariance.