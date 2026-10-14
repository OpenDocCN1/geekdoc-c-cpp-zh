NOTE While it’s tempting to abbreviate all the names, shortening MetersPerSecond to Ms might be confused with milliseconds, so it’s best to spell out the unit in this case.

The constructor for Speed takes a number for the magnitude, and the user must provide one of the enum values for the required units. The user can use the In property later to discover which units were used when a particular Speed instance was created. By supporting several units of measurement, we make Speed more generally useful in other applications.

Representing supported units with an enum is superficially appealing because it seems simple to implement. However, this approach suffers from drawbacks that become apparent when we need to decide how to handle two values that have different units.

# Value Comparisons and Unit Conversions

We need to consider conversions between units in several places in our Speed implementation. For instance, these two Speed values use different units but nevertheless represent the same speed:

```
var limit = new Speed(3.6, Speed.Units.KmPerHour);
var unit  = new Speed(1,   Speed.Units.MetersPerSecond);
```

These two Speed variables do not compare equal by default, because their Amount and In properties have different values. We can address that problem by customizing the behavior of equality comparisons for Speed, perhaps by converting both values to meters per second and comparing those values for equality. However, we have other, more subtle problems to solve too.

Earlier, we added operator overloads to Speed to support multiplying them by a scalar value or a time. Adding support for other arithmetic operations, including adding two Speeds, would be reasonable. We’d have to convert both values to a common unit in order to add them together, but what unit should the result be in?

One option would be to always scale every Speed value to meters per second—as we do in Listing 1-24 by using Speed’s constructor to convert the parameter value according to the required units—but this approach introduces different problems.

```
public Speed(double amount, Units unit)
{
    if(amount < 0)
        throw new ArgumentOutOfRangeException(
            paramName: nameof(amount),
            message: "Speed must be positive");

    Amount = unit switch
    {
        Units.KmPerHour      => amount * 1000 / 3600,
        Units.KmPerSecond    => amount * 1000,
        Units.MetersPerSecond => amount,
```