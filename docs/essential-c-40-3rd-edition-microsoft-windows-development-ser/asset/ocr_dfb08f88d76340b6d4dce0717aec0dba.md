# Comparison Operators (==, !=, <, >, <=, >=)

Once Equals() is overridden, there is a possible inconsistency. Two objects could return true for Equals() but false for the == operator because == performs a reference equality check by default as well. To correct this it is important to overload the equals (==) and not equals (!=) operators as well.

For the most part, the implementation for these operators can delegate the logic to Equals(), or vice versa. However, some initial null checks are required first (see Listing 9.6).

```
LISTING 9.6: Implementing the == and != Operators

public sealed class Coordinate
{
    // ...

    public static bool operator ==(
        Coordinate leftHandSide,
        Coordinate rightHandSide)
    {
        // Check if LeftHandSide is null.
        // (operator== would be recursive)
        if (ReferenceEquals(leftHandSide, null))
        {
            // Return true if rightHandSide is also null
            // but false otherwise.
            return ReferenceEquals(rightHandSide, null);
        }

        return (leftHandSide.Equals(rightHandSide));
    }

    public static bool operator !=(
        Coordinate leftHandSide,
        Coordinate rightHandSide)
    {
        return !(leftHandSide == rightHandSide);
    }
}
```

Note that to perform the null checks, you cannot use an equality check for null (leftHandSide == null). Doing so would recursively call back into the method, resulting in a loop until overflowing the stack. To avoid this you call ReferenceEquals() to check for null.