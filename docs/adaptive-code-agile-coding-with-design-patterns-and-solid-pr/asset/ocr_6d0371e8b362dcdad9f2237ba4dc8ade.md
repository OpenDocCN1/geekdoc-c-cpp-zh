```
```csharp
protected override ShippingStrategy CreateShippingStrategy()
{
    return new WorldwideShippingStrategy(decimal.One);
}
}
// . . .
public abstract class ShippingStrategyTestsBase
{
    [Test]
    public void ShippingWeightMustBePositive()
    {
        strategy.Invoking(s => s.CalculateShippingCost(1f, ValidSize, null))
            .Should().Throw<ArgumentOutOfRangeException>("Package weight must be positive and non-zero")
            .And.ParamName.Should().Be("packageWeightInKilograms");
    }
}
```
```

# Postconditions cannot be weakened

When applying postconditions to subclasses, the opposite rule applies. Instead of not being able to strengthen postconditions, you cannot weaken them. As for all the Liskov substitution rules relating to contracts, the reason that you cannot weaken postconditions is because existing clients might break when presented with the new subclass. Theoretically, if you comply with the LSP, any subclass you create should be usable by all existing clients without causing them to fail in unexpected ways.

One such example of causing an unexpected failure in an existing client is explored in Listing 9-10. The unit test and implementation relate to the WorldwideShippingStrategy, the Shipping-Strategy subclass for international packages.

**LISTING 9-10**  The new implementation requires a weakening of the postcondition.

```
```csharp
[Test]
public void ShippingDomesticallyIsFree()
{
    strategy.CalculateShippingCost(1f, ValidDimensions, RegionInfo.CurrentRegion)
        .Should().Be(decimal.Zero);
}
// . . .
public override decimal CalculateShippingCost(float packageWeightInKilograms, Size<float> packageDimensionsInInches, RegionInfo destination)
{
    if (destination == null)
        throw new ArgumentNullException("destination", "Destination must be provided");

    if (packageWeightInKilograms <= 0f)
        throw new ArgumentOutOfRangeException("packageWeightInKilograms", "Package weight must be positive and non-zero");
}
```
```