
```csharp
: base(flatRate)
{
}

public new decimal FlatRate
{
    get
    {
        return base.FlatRate;
    }
    set
    {
        base.FlatRate = value;
    }
}
}
// . . .
public class ShippingStrategy
{
    public ShippingStrategy(decimal flatRate)
    {
        if (flatRate <= decimal.Zero)
            throw new ArgumentOutOfRangeException("flatRate", "Flat rate must be positive and non-zero");

        this.flatRate = flatRate;
    }

    protected decimal FlatRate
    {
        get
        {
            return flatRate;
        }
        set
        {
            if (value <= decimal.Zero)
                throw new ArgumentOutOfRangeException("value", "Flat rate must be positive and non-zero");

            flatRate = value;
        }
    }
}
```

Tightening the visibility of the field and instead providing access only through the property setter protects the invariant with a guard clause. Doing this at subclass level is also preferable because it means that all future subclasses are absolved of this responsibility and simply cannot directly write to the field at all.

A new unit test can be created that asserts this new behavior, as shown in Listing 7-14.

## LISTING 7-14 With the invariant maintained, this unit test passes.

Click here to view code image

```
[Test]
public void ShippingFlatRateCannotBeSetToNegativeNumber()
{
    strategy.Invoking(s => s.FlatRate = decimal.MinusOne)
        .ShouldThrow<ArgumentOutOfRangeException>("Flat rate must be positive and non-zero")
        .And.ParamName.Should().Be("value");
}
```

If a client tries to set the FlatRate property to a negative value, or even to zero, the guard clause prevents the assignment and an ArgumentOutOfRangeException is thrown.

## Code contracts

Throughout the previous section, the guard clauses that formed the basis of the contracts were all written in long form, using if statements and exceptions. It is worth exploring an alternative to these manual guard clauses: code contracts.

Previously a separate library, code contracts were integrated into the .NET Framework 4.0 main libraries. In addition to being easier to read, write, and comprehend than manual guard clauses, code contracts bring with them the possibility of using static verification and automatic generation of reference documentation.

With static contract verification, code contracts are able to check for contract violations without executing the application. This helps expose implicit contracts such as null dereferences and problems with array bounds, in addition to the explicitly coded contracts shown throughout this section.

Generating reference documentation relating to the contract of a method or class is important because client code has no other way of knowing the expectations. When more detail is included in the XML comments that form the documentation to methods and classes, clients can view the expectations via IntelliSense. This makes working with classes that use contracts a bit easier.

## Preconditions

Preconditions can be written succinctly by using code contracts. You will need to include the System.Diagnostics.Contracts namespace, which is part of the mscorlib.dll and so should not need an additional assembly reference. The static Contract class provides the majority of the functionality that is required to implement contracts.

### Note

If you make the decision to use code contracts, the static Contract class will permeate throughout almost all of your code base. This is less of a problem than it is with most static references because code contracts are ubiquitous infrastructure that, it is assumed, will not be removed or replaced. Thus, it is a significant undertaking to undo the decision to use code contracts, and it is best to use them from the outset of a project, or not at all.

Listing 7-15 shows the declarative nature of a code contract precondition.

## LISTING 7-15 The System.Diagnostics.Contracts namespace can provide guard clauses to methods.

Click here to view code image

```
using System.Diagnostics.Contracts;

public class ShippingStrategy
{
    public decimal CalculateShippingCost(float packageWeightInKilograms, Size<float> packageDimensionsInInches, RegionInfo destination)
    {
        Contract.Requires(packageWeightInKilograms > 0f);
        Contract.Requires(packageDimensionsInInches.X > 0f && packageDimensionsInInches.Y > 0f);

        return decimal.MinusOne;
    }
}
```

The Contract.Requires method accepts a Boolean predicate value. This represents the state that the method requires in order to proceed. Note that this is the exact opposite of the predicate used in an if statement in manual guard clauses. In that case, the clauses were checking for state that was invalid before throwing an exception. With code contracts, the predicate is closer to an assertion: that the Boolean value must return true, otherwise the contract fails. This example requires that the packageWeightInKilograms parameter is non-zero and positive and that the packageDimensionsInInches parameter is non-zero and positive for both its X and Y properties.

This version of the Contract.Requires method throws an exception when the contract predicate is not met, but the type of exception is a ContractException, which does not match the expected exception in the existing unit tests. Therefore, they fail.

Click here to view code image

Expected System.ArgumentOutOfRangeException because Package dimension must be positive and non-zero, but found System.Diagnostics.Contracts.__ContractsRuntime+ContractException with message

"Precondition failed: packageDimensionsInInches.X > 0f && packageDimensionsInInches.Y > 0f"

Furthermore, if you run this example while passing in an invalid value for one of the parameters, you will get the message shown in Figure 7-2. This informs you that you have not properly configured code contracts for use.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_260_0.png)

## FIGURE 7-2 Code contracts must be configured before use.

The property pages of each project include a Code Contracts tab on which you can configure code contracts. A minimal working setup is shown in Figure 7-3.

## FIGURE 7-3 The property pages for code contracts contain a lot of settings.

When they are configured correctly, the contract preconditions can be rewritten to use an alternative version of the Contract.Requires method. Listing 7-16 shows this version.

## LISTING 7-16 This version of the Requires method accepts the type of the exception to be thrown.

Click here to view code image

```
public class ShippingStrategy
{
    public decimal CalculateShippingCost(float packageWeightInKilograms, Size<float> packageDimensionsInInches, RegionInfo destination)
    {
        Contract.Requires<ArgumentOutOfRangeException>(packageWeightInKilograms > 0f, "Package weight must be positive and non-zero");
        Contract.Requires<ArgumentOutOfRangeException>(packageDimensionsInInches.X > 0f && packageDimensionsInInches.Y > 0f, "Package dimensions must be positive and non-zero");

        return decimal.MinusOne;
    }
}
```

This generic version of the Requires method accepts the type of exception that you would like the contract to throw when the predicate fails. This, along with the exception message included in a subsequent method parameter, will cause the existing unit tests to pass.

## Postconditions

Code contracts can similarly provide a shortcut to defining postconditions. The Contract static class contains an Ensures method that is the postcondition complement to the precondition’s Requires method. This method also accepts a Boolean predicate that must be true in order to progress through to the return statement. It is worth noting that the return statement must be the only line that follows a call to Contract.Ensures. This makes intuitive sense because, otherwise, it would be possible to further modify state in a way that might break the postcondition.

Listing 7-17 reiterates the ShippingCostMustBePositive unit test and includes a rewritten CalculateShippingCost implementation that uses the Contract.Ensures method as a postcondition.

**LISTING 7-17** The Ensures method creates a postcondition that should be true on exiting the method.

[Click here to view code image](#)

```
```csharp
[Test]
public void ShippingCostMustBePositive()
{
    strategy.CalculateShippingCost(1, ValidSize, null)
        .Should().BeGreaterThan(decimal.MinusOne);
}
// ...
public class ShippingStrategy
{
    public decimal CalculateShippingCost(float packageWeightInKilograms, Size<float> packageDimensionsInInches, RegionInfo destination)
    {
        Contract.Requires<ArgumentOutOfRangeException>(packageWeightInKilograms > 0f, "Package weight must be positive and non-zero");
        Contract.Requires<ArgumentOutOfRangeException>(packageDimensionsInInches.X > 0f &&
            packageDimensionsInInches.Y > 0f, "Package dimensions must be positive and non-zero");

        Contract.Ensures(Contract.Result<decimal>() > 0m);

        return decimal.MinusOne;
    }
}
```
```
