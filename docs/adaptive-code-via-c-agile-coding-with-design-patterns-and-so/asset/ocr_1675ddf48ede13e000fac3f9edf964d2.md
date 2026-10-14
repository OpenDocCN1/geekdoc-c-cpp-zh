# Preconditions

Preconditions can be written succinctly by using code contracts. You will need to include the System.Diagnostics.Contracts namespace, which is part of the mscorlib.dll and so should not need an additional assembly reference. The static Contract class provides the majority of the functionality that is required to implement contracts.

# Note

If you make the decision to use code contracts, the static Contract class will permeate throughout almost all of your code base. This is less of a problem than it is with most static references because code contracts are ubiquitous infrastructure that, it is assumed, will not be removed or replaced. Thus, it is a significant undertaking to undo the decision to use code contracts, and it is best to use them from the outset of a project, or not at all.

Listing 7-15 shows the declarative nature of a code contract precondition.

# LISTING 7-15 The System.Diagnostics.Contracts namespace can provide guard clauses to methods.

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

This version of the Contract.Requires method throws an exception when the contract predicate is