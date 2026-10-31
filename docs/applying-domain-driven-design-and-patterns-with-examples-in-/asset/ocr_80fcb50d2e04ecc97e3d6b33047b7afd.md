not OK. In these cases, the proactive method could return a list of broken rules instead, something like this:

```
```csharp
[Test]
public void CanMakeStateTransitionSafely()
{
    Order o = new Order(new Customer());

    Assert.AreEqual(0, o.BrokenRulesIfAccept.Count);
    //We can now safely do this without getting an exception...
    o.Accept();
}
```
```

I prefer to do this on a case-by-case basis. There is no standard interface or anything to implement, just a principle for interface design. So this is actually just a protocol for making it possible to be proactive regarding broken rules detection.

# The Transaction Abstraction

The transaction abstraction is a powerful one, and one that is underutilized. An alternative solution to the transition problem would be to use the transaction abstraction for the Domain Model and validations as well. Then during the transaction, it wouldn't matter if the state wasn't correct; and before and after you would matter. For example, the API could then look like this:

```
```csharp
//Some consumer...
DMTransaction dMTx = Something.StartTransaction();
c.Name = string.Empty;
c.Name = "Volvo";
dMTx.Commit();
```
```

In the code snippet, the rules weren't checked until `Commit()`. As you understand, this opens up a can of worms that needs to be dealt with, but it might be an interesting solution for the future.

The solution becomes even more interesting if you consider the new `System.Transaction` namespace of .NET 2.0. In the future, we might get transactional list classes, hash tables, and so on. It gets even more interesting considering transactions spanning both the Domain Model and the database. Again, loads of problems, but interesting.

Obviously there are lots of variations to the problem of state transitions. One such problem is deciding when an action should be taken as well. Stay tuned.