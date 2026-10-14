# Reference-Based Comparisons

Most objects have some state, whether that’s private instance fields or public property values. We might be tempted to override the default reference equality behavior for all our classes and always use that state as an object’s value for comparisons. However, although we can model values by using a class, as C# does with string, having a value and being a value are very different. Most types aren’t intended to be values, and the default reference comparison is more appropriate for the majority of the classes we create.

As an example of reference-based comparisons being important for an object, consider the Login class in Listing 6-1 for a system tracking logged-in users. Since Login is a class, the semantics of reference comparisons makes sense for it because we need to be able to distinguish between individual instances.

```
public sealed class Login
{
    public string UserName { get; }
    public DateTime Established { get; }
    public bool Active { get; private set; }
    --snip--

    public void Disconnect()
    {
        Active = false;
    }
}
```

Listing 6-1: Reference-based equality matters for class types.

Even though the public properties directly expose the state of a Login instance, using those properties to implement equality would be a mistake. Two instances of Login with the same property values might easily represent different connections. Even if we presume that the UserName property is unique across all users, we may still need to identify an individual login in systems that allow multiple connections by the same user. The same user might even log in twice at exactly the same moment, so distinguishing different connections by their Established property isn’t sufficient.

If we overrode the Equals method for Login to compare its property values, we couldn’t use Equals to distinguish between different instances with identical properties. If we needed to forcibly disconnect a specific connection by calling its Disconnect method, we’d want to be certain we were disconnecting the right one! We therefore need to be able to identify a specific instance of a login, regardless of the values of its public properties.

We could use a mechanism other than Equals to distinguish between different instances with identical state, but we’d be adding extra complexity to support functionality that a normal reference-based comparison already provides.

# Reference Semantics and Side Effects

The difference between value semantics and reference semantics is also defined partly by the potential for side effects via aliasing references, which