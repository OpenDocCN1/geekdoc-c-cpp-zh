One implication of Color being a reference type is that it’s possible for the other parameter to refer to the same instance as this. To handle this scenario, Listing 7-4 casts both this and other to object to make it clear that we intend a reference comparison. While the cast we used in Listing 7-3 from object to a more derived type is a relatively costly run-time conversion, the conversion from Color to its object base class is very efficient and allows the comparison to be made with the intrinsic ceq instruction introduced in Chapter 5. One alternative would be to use ReferenceEquals(this, other) here, making the reference-based comparison explicit.

Comparing the two variables to see whether they reference the same object is a simple but not mandatory optimization. The logical || operator short-circuits if its left-hand expression is true, so the rest of the comparisons are attempted only if this and other are references to different instances. Note that the order of comparisons in this code relies on operator precedence; the logical AND operator (&&) has a higher precedence than logical OR (||), so the comparisons on the right side of || all bind together as if they were explicitly grouped within a pair of parentheses. Although redundant, the extra parentheses don’t affect the behavior in any way, and some programmers prefer to add them to avoid having to remember the operator precedence rules.

Because Color is a reference type, the argument passed could be null, so we use the is not constant pattern to compare other with null and avoid the common trap of calling our own Equals method recursively.

The Color class is intentionally not sealed, so we also check that the other value is exactly the same type as this by using the GetType method, defined on the object base class. This method returns the run-time type of an instance, and the types won’t match if other is a reference to a more derived type such as TranslucentColor. Objects of different types don’t normally compare equal, even if their types are related by inheritance.

Finally, if the types match, we compare each property’s value in turn. If they all match, our Equals method returns true. We use == rather than Equals here because all the properties of a Color are simple int values. Built-in values such as these can be compared intrinsically, and much more compactly than calling the Equals method for each of them.

To make comparing Color instances natural, we also implement operator== and operator!=, which both defer to the type-safe Equals method, like this:

```
public static bool operator==(Color? left, Color? right)
    => left?.Equals(right) ?? right is null;

public static bool operator!=(Color? left, Color? right)
    => !left?.Equals(right) ?? right is not null;
```