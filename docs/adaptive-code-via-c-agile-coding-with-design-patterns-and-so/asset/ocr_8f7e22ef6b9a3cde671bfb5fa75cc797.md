# LISTING 3-9 Explicitly implementing an interface to avoid clashing method signatures.

Click here to view code image

```
public class ClassAvoidingMethodSignatureClash : IInterfaceOne
{
    public void MethodOne()
    {
        // original implementation
    }

    void IInterfaceOne.MethodOne()
    {
        // new implementation
    }
}
```

In a similar regard, if a class needs to implement two different interfaces that are unrelated but that both contain a method with the same signature, you can implement them both implicitly and share the same method implementation. Or, as shown in Listing 3-10, you can implement them both explicitly—for clarity—to demarcate which implementation belongs to which interface.

# LISTING 3-10 When implementing two interfaces with a common method signature, only explicit implementation is sufficient.

Click here to view code image

```
public class ClassImplementingClashingInterfaces : IInterfaceOne, IAnotherInterfaceOne
{
    void IInterfaceOne.MethodOne()
    {

    }

    void IAnotherInterfaceOne.MethodOne()
    {
    }
}
```