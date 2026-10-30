# LISTING 9-2 It is important to provide as much context as possible about why the precondition caused a failure.

```
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination
{
    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms",
            "Package weight must be positive and nonzero");

    return decimal.MinusOne;
}
```

This is an improvement on the first exception that was thrown. In addition to using an exception specifically for out-of-range arguments, this code tells the client which parameter is errant and provides a description of the problem.

You can add more conditions that must be fulfilled by chaining more guard clauses like this together. The changes shown in Listing 9-3 include exceptions that are thrown when the package dimensions are out of range, too.

# LISTING 9-3 As many preconditions as necessary can be added to prevent the method from being called with invalid parameters.

```
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination
{
    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and nonzero");

    if (packageDimensionsInInches.X <= 0f || packageDimensionsInInches.Y <= 0f)
        throw new ArgumentOutOfRangeException("packageDimensionsInInches",
            "Package dimensions must be positive and nonzero");

    return decimal.MinusOne;
}
```

With these preconditions in place, clients must ensure that the parameters they provide are within valid ranges before calling. One corollary from this is that all the state that is checked in a precondition must be publicly accessible by clients. If a client is unable to verify that the method it is about to call will throw an error due to an invalid precondition, the client won’t be able to ensure that the call will succeed. Therefore, private state should not be the target of a precondition; only method parameters and the class’s public properties should be referenced by preconditions.