implied. If we used a value for speed in kilometers per hour, we’d certainly get unexpected results.

Similarly, we don’t currently specify the units for the Angle type. Code that deals with trigonometry commonly uses radians as the unit of measurement, and all the trigonometric functions in the Math class, such as Sin, expect angle values in radians. Most people, however, think of angles in degrees, and confusing the two is a common source of error.

This exposes the issue of usability: should our code require units that are more convenient for their implementation or more intuitive for the user? Let’s consider this question and investigate whether it’s possible to achieve both aims simultaneously.

C# has several features we can use to encode units, and one common approach is to represent the different units by using an enum. At first glance, this might seem the obvious solution, but it can cause issues. We’ll explore this option and then investigate an alternative solution using static methods to create our types with the required units.

# Itemizing Units with enums

An enumerated type, or enum, is a set of related strongly typed constants. Using an enum allows us to specify all the units our type supports. Listing 1-23 modifies our Speed type to use an enum to account for units.

```
public readonly struct Speed
{
    public enum Units
    {
        MetersPerSecond,
        KmPerSecond,
        KmPerHour
    }

    public Speed(double amount, Units unit)
    {
        if(amount < 0)
            throw new ArgumentOutOfRangeException(
                paramName: nameof(amount),
                message: "Speed must be positive");

        Amount = amount;
        In = unit;
    }

    public double Amount { get; }
    public Units In { get; }
}
```

Listing 1-23: Specifying units for Speed by using an enum

In this code, the Units enumeration is a public type nested within Speed, telling us that a speed can be represented in meters per second, kilometers per second, or kilometers per hour.