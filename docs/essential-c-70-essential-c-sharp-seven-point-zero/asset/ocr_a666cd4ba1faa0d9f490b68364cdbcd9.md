# ADVANCED TOPIC

# Defining Custom Conversions

Conversion between types is not limited to types within a single inheritance chain. It is possible to convert between unrelated types as well, such as converting from an Address to string, and vice versa. The key is the provision of a conversion operator between the two types. C# allows types to include either explicit or implicit conversion operators. If the operation could possibly fail, such as in a cast from long to int, developers should choose to define an explicit conversion operator. This warns developers performing the conversion to do so only when they are certain the conversion will succeed, or else to be prepared to catch the exception if it doesn’t. They should also use an explicit conversion over an implicit conversion when the conversion is lossy. Converting from a float to an int, for example, truncates the decimal, which a return cast (from int back to float) would not recover.

Listing 7.5 shows an example of an implicit conversion operator signature.

# LISTING 7.5: Defining Cast Operators

```
```
class GPSCoordinates
{
    // ... }

    public static implicit operator UTMCoordinates(
        GPSCoordinates coordinates)
    {
        // ... }
}
```
```

In this case, you have an implicit conversion from GPSCoordinates to UTMCoordinates. A similar conversion could be written to reverse the process. Note that an explicit conversion could also be written by replacing implicit with explicit.

# private Access Modifier

All members of a base class, except for constructors and destructors, are inherited by the derived class. However, just because a member is inherited, that does not mean it is accessible. For example, in Listing 7.6, the