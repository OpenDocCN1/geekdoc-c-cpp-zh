# C#’s Support for Delegate Chains

To make things easier for C# developers, the C# compiler automatically provides overloads of the `+=` and `-=` operators for instances of delegate types. These operators call `Delegate.Combine` and `Delegate.Remove`, respectively. Using these operators simplifies the building of delegate chains. The `ChainDelegateDemo1` and `ChainDelegateDemo2` methods in the source code shown at the beginning of this chapter produce absolutely identical IL code. The only difference between the methods is that the `ChainDelegateDemo2` method simplifies the source code by taking advantage of C#’s `+=` and `-=` operators.

If you require proof that the resulting IL code is identical for the two methods, you can build the code and look at its IL for both methods by using ILDasm.exe. This will confirm that the C# compiler did in fact replace all `+=` and `-=` operators with calls to the Delegate type’s public static Combine and Remove methods, respectively.

# Having More Control over Delegate Chain Invocation

At this point, you understand how to build a chain of delegate objects and how to invoke all of the objects in that chain. All items in the chain are invoked because the delegate type’s Invoke method includes code to iterate through all of the items in the array, invoking each item. This is obviously a very simple algorithm. And although this simple algorithm is good enough for a lot of scenarios, it has many limitations. For example, the return values of the callback methods are all discarded except for the last one. Using this simple algorithm, there’s no way to get the return values for all of the callback methods called. But this isn’t the only limitation. What happens if one of the invoked delegates throws an exception or blocks for a very long time? Because the algorithm invoked each delegate in the chain serially, a “problem” with one of the delegate objects stops all of the subsequent delegates in the chain from being called. Clearly, this algorithm isn’t robust.

For those scenarios in which this algorithm is insufficient, the `MulticastDelegate` class offers an instance method, `GetInvocationList`, that you can use to call each delegate in a chain explicitly, using any algorithm that meets your needs:

```
public abstract class MulticastDelegate : Delegate {
    // Creates a delegate array where each element refers
    // to a delegate in the chain.
    public sealed override Delegate[] GetInvocationList();
}
```

The `GetInvocationList` method operates on a `MulticastDelegate`-derived object and returns an array of Delegate references where each reference points to one of the chain’s delegate objects. Internally, `GetInvocationList` constructs an array and initializes it with each element referring to a delegate in the chain; a reference to the array is then returned. If the `_invocationList` field is null, the returned array contains one element that references the only delegate in the chain: the delegate instance itself.

You can easily write an algorithm that explicitly calls each object in the array. The following code