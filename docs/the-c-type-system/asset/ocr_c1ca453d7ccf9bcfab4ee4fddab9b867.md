```
```csharp
private const double C = 299792458;

public static double Distance(Speed speed, double time)
{
    if(speed.InMetersPerSecond > C ||
       speed.InMetersPerSecond < 0 ||
       speed.InMetersPerSecond is double.NaN)
    {
        throw new ArgumentOutOfRangeException(...
    }
    //--snip--
}
public static double Time(Speed speed, double distance)
{
    if(speed.InMetersPerSecond > C ||
       speed.InMetersPerSecond < 0 ||
       speed.InMetersPerSecond is double.NaN)
    {
        throw new ArgumentOutOfRangeException(...
    }
    //--snip--
}
```
```

*Listing 6-10: Duplicated validation code*

To protect these methods from invalid speed values being passed as arguments, we must validate the parameter to ensure that it’s not larger than the maximum allowed value, it’s not negative, and it’s a real number. The tests we use are the same for every method using a `Speed`, and we should also validate the values for the time and distance parameters. It would be easy to forget one of these checks when we write a new function that uses a speed, time, or distance, or to accidentally use the wrong value for the maximum allowable speed.

The duplication of the validation code is also a maintenance problem. If we need to alter the acceptable range of values for speeds, we have to make sure we change it everywhere it occurs. We also need to test the validation logic in every method where it’s applied, so those tests will also be duplicated.

If we instead encapsulate the validation logic within a constructor for `Speed`, we can test its characteristics in only one place and in isolation from other tests we need. We won’t need to worry that the values might be out of range for methods using `Speed` values. Any method using a `Speed` can rely on the validation it encapsulates. We can remove the duplicated validation code as well as any duplicated tests.

# Establishing Class Invariants

Having a constructor that performs all the necessary validation for a type’s value is an example of establishing a *class invariant* (where *class* has to do with type theory rather than the class keyword). This approach ensures that all instances have values that make sense for the type.

Listing 6-11 shows how we can combine a switch expression with pattern matching to efficiently perform numeric validation in a constructor.