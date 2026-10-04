```
If I, has Invoke method would have internally looked like the following (again, in pseudocode).

public Int32 Invoke(Int32 value) {
    Int32 result;
    Delegate[] delegateSet = _invocationList as Delegate[];
    if (delegateSet != null) {
        // This delegate identifies the delegates that should be called
        foreach (Feedback d in delegateSet)
            result = d(value); // Call each delegate
    } else {
        // This delegate will be called back
        // Call the callback method on the target object.
        result = _methodPtr.Invoke(target, value);
        // The preceding line is an approximation of the actual code.
        // What really happens cannot be expressed in C#.
    }
    return result;
}
```

As each delegate in the array is called, its return value is saved in the result variable. When the loop is complete, it will contain only the result of the last delegate called (previous return values are discarded); this value is returned to the code that called Invoke.

# C#s Support for Delegate Chains

To make things easier for C developers, the C# compiler automatically provides overloads of += and -= operators for instances of delegate types. These operators call Delegate.Combine and Delegate.Remove, respectively. Using these operators simplifies the building of delegate chains. The ChainDelegateDemo1 and ChainDelegateDemo2 methods in the source code at the beginning of this chapter would produce almost identical IL. The difference between them is that the ChainDelegateDemo2 method simplifies the code by taking advantage of C#s += and -= operators.

If you require proof that the resulting IL code is identical for the two methods, you can build the code and look at IL for both methods by using ILasm.exe. This will confirm that the C# compiler did in fact replace all += and -= operators with calls to the Delegate type's public static Combine and Remove methods, respectively.

# Having More Control over Delegate Chain Invocation

At this point, you understand how to build a chain of delegate objects and how to invoke all of the objects in that. All items in the chain are invoked because the delegate's Invoke method includes code to iterate through all of the items in the array, invoking each item. This is obviously a very simple algorithm. Although this simple algorithm is good enough for a lot of scenarios, it has many limitations. For example, the return values of the callback methods are all discarded except for the last one. Using this simple algorithm, there is no way to get all the values of the callback methods called. But this isn't the only limitation. What if one of the invoked delegates throws an exception or blocks for a very long time? The algorithm invoked each delegate