```
public readonly struct Speed
{
    public Speed(double amount)
        => Amount = amount;

    public double Amount { get; }
}
```

Listing 1-6: Making Speed immutable

To ensure that the Speed instance can’t change, we also make it readonly. The compiler will then ensure that no members of Speed can modify the state and will fail to compile any attempt to change an instance.

Designing our types to be immutable makes our code easier to reason about during code inspection because we don’t need to consider the various ways that instances of our type might change. This is especially important in multithreaded programs, but making value types read-only can also improve performance in some circumstances by enabling the compiler to use certain optimizations.

# Value Validation

Having introduced constructors for our types, we can use those constructors to check for invalid arguments and raise exceptions if the user passes illegal values. For example, sensible values for a speed must be nonnegative. In Listing 1-7, we check that the value given the constructor is not less than 0 and throw an exception if it is.

```
public Speed(double amount)
{
    if(amount < 0)
        throw new ArgumentOutOfRangeException(
            paramName: nameof(amount),
            message: "Speed must be positive");
    Amount = amount;
}
```

Listing 1-7: Prohibiting out-of-range values

The constructor of Speed validates the value provided, and since the constructor is the only way to provide a value for Speed, we ensure that only legal Speed values can be created. We should use the constructor to prohibit other illegal argument values, such as double.NaN, and perhaps even add an upper limit of the speed of light. If we attempt to create a Speed with an illegal value, we get a run-time exception.

The ArgumentOutOfRangeException type is defined in the Standard Library and is a good example of a descriptively named type. Note that in Listing 1-7, we name the arguments for the ArgumentOutOfRangeException constructor, which takes two plain string parameters (paramName: and message:). Otherwise, the order of those arguments is easily muddled, especially since the similarly named ArgumentException takes the same parameters in the reverse order!