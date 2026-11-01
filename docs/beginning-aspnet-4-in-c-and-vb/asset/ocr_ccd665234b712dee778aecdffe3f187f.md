If the ambient transaction is different from the enlisted transaction, an exception is thrown. The implementation does not support changing the same value from within two different transactions. If you have this requirement, you can create a lock and wait for the lock to be released from one transaction before changing it within another transaction:

```
public Transactional(T value)
{
    if (Transaction.Current == null)
    {
        this.liveValue = value;
    }
    else
    {
        this.liveValue = default(T);
        GetEnlistment().Value = value;
    }
}

public Transactional()
    : this(default(T)) {}

private ResourceManager<T> GetEnlistment()
{
    Transaction tx = Transaction.Current;
    Trace.Assert(tx != null, 'Must be invoked with ambient transaction');
    if (enlistedTransaction == null)
    {
        enlistment = new ResourceManager<T>(this, tx);
        tx.EnlistVolatile(enlistment, EnlistmentOptions.None);
        enlistedTransaction = tx;
        return enlistment;
    }
    else if (enlistedTransaction == Transaction.Current)
    {
        return enlistment;
    }
    else
    {
        throw new TransactionException(
            "This class only supports enlisting with one transaction");
    }
}
```

The property Value returns the value of the contained class and sets it. However, with transactions, you cannot just set and return the liveValue variable. This would be the case only if the object were outside a transaction. To make the code more readable, the property Value uses the methods GetValue() and SetValue() in the implementation:

```
public T Value
{
    get { return GetValue(); }
    set { SetValue(value); }
}
```

The method GetValue() checks if an ambient transaction exists. If one doesn’t exist, the liveValue is returned. If there is an ambient transaction, the GetEnlistment() method shown earlier returns the resource manager, and with the Value property, the temporary value for the contained object within the transaction is returned.