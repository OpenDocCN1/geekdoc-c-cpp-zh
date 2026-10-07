# ADVANCED TOPIC

# Cast Operator (())

Implementing the explicit and implicit conversion operators is not technically overloading the cast operator (()). However, this action is effectively what takes place, so defining a cast operator is common terminology for implementing explicit or implicit conversion.

Defining a conversion operator is similar in style to defining any other operator, except that the “operator” is the result type of the conversion. Additionally, the operator keyword follows a keyword that indicates whether the conversion is implicit or explicit (see Listing 10.6).

Listing 10.6: Providing an Implicit Conversion between Latitude and double

```
public readonly struct Latitude
{
    // ...
    public double DecimalDegrees(double decimalDegrees)
    {
        DecimalDegrees = Normalize(decimalDegrees);
    }
    public double DecimalDegrees { get; }

    // ...
    public static implicit operator double(Latitude latitude)
    {
        return latitude.DecimalDegrees;
    }
    public static implicit operator Latitude(double degrees)
    {
        return new Latitude(degrees);
    }

    // ...
}
```

With these conversion operators, you now can convert doubles implicitly to and from Latitude objects. Assuming similar conversions exist for Longitude,