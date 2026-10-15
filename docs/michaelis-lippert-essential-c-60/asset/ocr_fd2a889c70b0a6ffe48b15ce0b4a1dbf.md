For example, string provides a + operator that concatenates two strings. This is perhaps not surprising, because string is a predefined type, so it could possibly have special compiler support. However, C# provides for adding + operator support to a class or struct. In fact, all operators are supported except x.y, f(x), new, typeof, default, checked, unchecked, delegate, is, as, =, and =>. One particularly noteworthy operator that cannot be implemented is the assignment operator; there is no way to change the behavior of the = operator.

Before going through the exercise of implementing an operator overload, consider the fact that such operators are not discoverable through IntelliSense. Unless the intent is for a type to act like a primitive type (a numeric type, for example), you should avoid overloading an operator.

# Comparison Operators (==, !=, <, >, <=, >=)

Once Equals() is overridden, there is a possible inconsistency. That is, two objects could return true for Equals() but false for the == operator because == performs a reference equality check by default. To correct this flaw, it is important to overload the equals (==) and not equals (!=) operators as well.

For the most part, the implementation for these operators can delegate the logic to Equals(), or vice versa. However, for reference types, some initial null checks are required first (see Listing 9.6).

# LISTING 9.6: Implementing the == and != Operators

```
public sealed class ProductSerialNumber
{
    // ...

    public static bool operator ==(
        ProductSerialNumber leftHandSide,
        ProductSerialNumber rightHandSide)
    {
        // Check if leftHandSide is null.
        // (operator== would be recursive)
        if(ReferenceEquals(leftHandSide, null))
        {
            // Return true if rightHandSide is also null
            // and false otherwise.
            return ReferenceEquals(rightHandSide, null);
        }
```