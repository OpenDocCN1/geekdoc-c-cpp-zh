For checking collections that are used as arguments, the Contract class offers Exists() and ForAll() methods. ForAll() checks every item in the collection if the condition succeeds. In the example, it is checked if every item in the collection has a value smaller than 12. With the Exists() method, it is checked if any one element in the collection succeeds the condition.

```
static void ArrayTest(int[] data)
{
    Contract.Requires(Contract.ForAll(data, i => i < 12));
}
```

Both the methods Exists() and ForAll() have an overload where you can pass two integers, fromInclusive and toExclusive, instead of IEnumerable<T>. A range from the numbers (excluding toExclusive) is passed to the delegate Predicate<int> defined with the third parameter. Exists() and ForAll() can be used with preconditions, postconditions, and also invariants.

# Postconditions

Postconditions define guarantees about shared data and return values after the method has completed. Although they define some guarantees on return values, they must be written at the beginning of a method; all contract requirements must be at the beginning of the method.

Ensures() and EnsuresOnThrow<TException>() are postconditions. The following contract ensures that the variable sharedState is lower than 6 at the end of the method. The value can change in between.

![](bbox=[0.18, 0.6, 0.28, 0.75])

```
private static int sharedState = 5;
static void Postcondition()
{
    Contract.Ensures(sharedState < 6);
    sharedState = 9;
    Console.WriteLine("change sharedState invariant {0}", sharedState);
    sharedState = 3;
    Console.WriteLine("before returning change it to a valid value {0}", sharedState);
}
```

Pro C# 4 9780470302259 code snippet CodeContractsSamples/Program.cs

With EnsuresOnThrow<TException>(), it is guaranteed that a shared state succeeds a condition if a specified exception is thrown.

To guarantee a return value, the special value Result<T> can be used with an Ensures() contract. Here, the result is of type int as is also defined with the generic type T for the Result() method. The Ensures() contract guarantees that the return value is lower than 6.

```
static int ReturnValue()
{
    Contract.Ensures(Contract.Result<int>() < 6);
    return 3;
}
```

You can also compare a value to an old value. This is done with the OldValue<T>() method that returns the original value on method entry for the variable passed. The following ensures that the