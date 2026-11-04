example is the IDisposable interface where multiple calls to Dispose should have no further effect beyond the first call (the property of idempotency) and where no further interactions with the object should be possible after it has been disposed (by throwing an ObjectDisposedException).

One example of an interface contract gone bad is ICloneable, which is used to indicate that instances of a type can be cloned. However, the designers never specified whether a shallow clone (just copying a reference for reference typed members) or a deep clone (recursively cloning reference-typed members) is desired. As a result, the interface has a limited value:

```
public interface ICloneable {
    object Clone();
}
```

# Implementing Interfaces

To implement an interface, you specify the interface name on the class or struct definition after the colon:

```
class Resource : IDisposable
{
    public void Dispose() { ... }
}
```

When doing so, provide implementations for the interface's members or mark them as abstract, deferring to a subclass. Two ways to implement interface members are available. The one shown in the preceding snippet is sometimes referred to as implicit interface implementation. When defining the Dispose method, we didn't state we're going to satisfy the contract provided by IDisposable. As a result, we can call the interface method in a variety of ways:

```
Resource res = new Resource();
res.Dispose();
((IDisposable)res).Dispose();
```

In the second case, we're using virtual dispatch mechanisms to deliver the call through the interface contract. The runtime facilities to materialize the call are similar to the ones we saw before but involve an additional concept of “interface maps,” which are beyond the scope of this book. For the first call to Dispose, we're invoking the method as it is exposed on the Resource type's public “interface.” You learn later how we can hide the method from an implementing type's public interface.

Notice how the accessibility of the Dispose method provided for the implicit interface implementation is declared to be public. This is a requirement because every interface