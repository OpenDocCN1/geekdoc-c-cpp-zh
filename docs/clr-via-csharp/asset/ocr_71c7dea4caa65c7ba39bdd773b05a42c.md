At the heart of the code contracts is the static **System.Diagnostics.Contracts.Contract** class:

```
```csharp
public static class Contract {
    // Precondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Requires(Boolean condition);
    public static void EndContractBlock();

    // Preconditions: Always
    public static void Requires<TException>(Boolean condition) where TException : Exception;

    // Postcondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Ensures(Boolean condition);
    public static void EnsuresOnThrow<TException>(Boolean condition)
        where TException : Exception;

    // Special Postcondition methods: Always
    public static T Result<T>();
    public static T OldValue<T>(T value);
    public static T ValueAtReturn<T>(out T value);

    // Object Invariant methods: [Conditional("CONTRACTS_FULL")]
    public static void Invariant(Boolean condition);

    // Quantifier methods: Always
    public static Boolean Exists<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean Exists(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);
    public static Boolean ForAll<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean ForAll(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);

    // Helper methods: [Conditional("CONTRACTS_FULL")] or [Conditional("DEBUG")]
    public static void Assert(Boolean condition);
    public static void Assume(Boolean condition);

    // Infrastructure event: usually your code will not use this event
    public static event EventHandler<ContractFailedEventArgs> ContractFailed;
}```
```

As indicated above, many of these static methods have the **[Conditional("CONTRACTS_FULL")]** attribute applied to them. Some of the helper methods also have the **[Conditional("DEBUG")]** attribute applied to them. This means that the compiler will ignore any code you write that calls these methods unless the appropriate symbol is defined when compiling your code. Any methods marked with “Always” mean that the compiler always emits code to call the method. Also, the **Requires**, **`Requires<TException>`**, **Ensures**, **EnsuresOnThrow**, **Invariant**, **Assert**, and **Assume** methods have an additional overload (not shown) that takes a **String** message argument so you can explicitly specify a string message that should appear when the contract is violated.

By default, contracts merely serve as documentation as you would not define the **CONTRACTS_FULL** symbol when you build your project. In order to get some additional value out of using contracts, you must download additional tools and a Visual Studio property pane from http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx. The reason why all the