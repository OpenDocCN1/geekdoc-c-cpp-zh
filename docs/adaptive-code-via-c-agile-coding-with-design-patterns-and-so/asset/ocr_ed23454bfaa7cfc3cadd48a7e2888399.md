method must implement a *precondition*.

# 💡 **Tip**

Although contracts as outlined in this chapter add run-time protection against many invalid calls to methods, the importance of good method and parameter naming is hard to exaggerate. If the formal parameters of the CalculateShippingCost method did not specify that they are in inches or kilograms, clients could, for example, call the method with values representing centimeters and pounds, respectively.

# ## Preconditions

*Preconditions* are defined as all of the conditions necessary for a method to run reliably and without fault. Every method requires some preconditions to be true before it should be called. By default, interfaces force no guarantees on any of the implementers of their methods. [Listing 7-1](#listing-7-1) shows how you can implement a precondition by using a guard clause at the start of a method.

**LISTING 7-1** Throwing an exception is an effective way of enforcing precondition contracts.

![](bbox=[0.008, 0.54, 0.252, 0.557])

```
```csharp
public decimal CalculateShippingCost(
    float packageWeightInKilograms,
    Size<float> packageDimensionsInInches,
    RegionInfo destination)
{
    if (packageWeightInKilograms <= 0f) throw new
    Exception();

    return decimal.MinusOne;
}
```
```

The if statement at the very start of the method is one way to enforce a precondition, such as the requirement for a positive weight. If the condition packageWeightInKilograms <= 0f is met, an exception is thrown and the method stops executing immediately. This certainly prevents a method from being executed unless all parameters have valid values. By using a more descriptive exception, you can provide more context to the caller, as shown in [Listing 7-2](#listing-7-2).

**LISTING 7-2** It is important to provide as much context as possible about why the precondition caused a failure.