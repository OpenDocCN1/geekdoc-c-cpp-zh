# The IsNull property anti-pattern

Sometimes the Null Object pattern involves adding a Boolean IsNull property to the interface. All real implementations of this interface return the value false for this property. The Null Object implementation of the interface returns true. Listing 4-15 shows how this might work, given the previous example.

**LISTING 4-15** The IsNull property is true only for Null Object implementations.

```
public interface IUser
{
    void IncrementSessionTicket();

    bool IsNull
    {
        get;
    }
}
// . . .
public class User : IUser
{
    // . . .
    public bool IsNull
    {
        get
        {
            return false;
        }
    }

    private DateTime sessionExpiry;
}
// . . .
public class NullUser : IUser
{
    public void IncrementSessionTicket()
    {
        // do nothing
    }

    public bool IsNull
    {
        get
        {
            return true;
        }
    }
}
```

The problem with this property is that it causes logic to spill out of the objects whose purpose is to encapsulate behavior. For example, if statements will start to creep into client code to differentiate