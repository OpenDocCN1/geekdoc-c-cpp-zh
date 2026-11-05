```
```csharp
}
class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1); // M1 - one entry in invocation list
        D cd2 = new D(C.M2); // M2 - one entry
        D cd3 = cd1 + cd2;   // M1 + M2 - two entries
        D cd4 = cd3 + cd1;   // M1 + M2 + M1 - three entries
        D cd5 = cd4 + cd3;   // M1 + M2 + M1 + M1 + M2 - five entries
        D td3 = new D(cd3);  // [M1 + M2] - ONE entry in invocation
                             // list, which is itself a list of two methods.
        D td4 = td3 + cd1;   // [M1 + M2] + M1 - two entries
        D cd6 = cd4 - cd2;   // M1 + M1 - two entries in invocation list
        D td6 = td4 - cd2;   // [M1 + M2] + M1 - two entries in invocation list,
                             // but still three methods called, M2 not removed.
    }
}
```
```

When cd1 and cd2 are instantiated, they each encapsulate one method. When cd3 is instantiated, it has an invocation list of two methods, M1 and M2, in that order. cd4's invocation list contains M1, M2, and M1, in that order. For cd5, the invocation list contains M1, M2, M1, M1, and M2, in that order.

When cd1 and cd2 are instantiated, they each encapsulate one method. When cd3 is instantiated, it has an invocation list of two methods, M1 and M2, in that order. cd4s invocation list contains M1, M2, and M1, in that order. For cd5 the invocation list contains M1, M2, M1, M1, and M2, in that order.

When creating a delegate from another delegate with a delegate_creation_expression the result has an invocation list with a different structure from the original, but which results in the same methods being invoked in the same order. When td3 is created from cd3 its invocation list has just one member, but that member is a list of the methods M1 and M2 and those methods are invoked by td3 in the same order as they are invoked by cd3. Similarly when td4 is instantiated its invocation list has just two entries but it invokes the three methods M1, M2, and M1, in that order just as cd4 does.

The structure of the invocation list affects delegate subtraction. Delegate cd6, created by subtracting cd2 (which invokes M2) from cd4 (which invokes M1, M2, and M1) invokes M1 and M1. However delegate td6, created by subtracting cd2 (which invokes M2) from td4 (which invokes M1, M2, and M1) still invokes M1, M2 and M1, in that order, as M2 is not a single entry in the list but a member of a nested list. For more examples of combining (as well as removing) delegates, see §20.6. end example

Once instantiated, a delegate instance always refers to the same invocation list.

Note: Remember, when two delegates are combined, or one is removed from another, a new delegate results with its own invocation list; the invocation lists of the delegates combined or removed remain unchanged. end note

# 20.6 Delegate invocation

C# provides special syntax for invoking a delegate. When a non-null delegate instance whose invocation list contains one entry, is invoked, it invokes the one method with the same arguments it was given, and returns the same value as the referred to method. (See §12.8.9.4 for detailed information on delegate invocation.) If an exception occurs during the invocation of such a delegate, and that exception is not