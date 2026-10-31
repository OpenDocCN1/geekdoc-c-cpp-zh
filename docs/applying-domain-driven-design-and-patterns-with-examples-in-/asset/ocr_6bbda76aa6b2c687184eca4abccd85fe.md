# Figure A-13. The relationship between `POrderBuilder` and `ItemStore`

![](bbox=[0.192, 0.146, 0.807, 0.231])

I've implemented the client version of `ItemStore` as a simple "read all items from store and cache." This strategy is fine as long as the number of items isn't too great. If it comes to that, it's no big deal to implement a version that queries the middle tier "smarter." In the client, when the order taker has the privilege to "work with an order," a `POrderBuilder` is instantiated and assigned an instance of the client side `ItemStore` implementation. At any time, a `CheckDiscrepancies()` against the client `ItemStore` is possible.

If the customer accepts, the next step is submission of the order to the middle tier. The `POrderBuilder` instance is serialized over the wire, but not the `ItemStore` instance. The reference to `ItemStore` is marked as `[NonSerialized]`. In the facade object, a connection/transaction is created and the job to take the order is handed over to the process object (the business object). This is shown in here:

```
```csharp
public POrderDiscrepancyReport TakeOrder(POrderBuilder order)
{
    POrder bo = new POrder();
    CnTxWrap cn =
        CnTxWrap.BeginTransaction(bo.CreateConnectionForMe() );
    try
    {
        POrderDiscrepancyReport res = bo.TakeOrder(cn, order);
        cn.Commit();
        return res;
    }
    catch
    {
        cn.Rollback();
        throw;
    }
}
```
```

While we're at it, let's take a look at the process object's `TakeOrder()` method in the following listing:

```
```csharp
[PrincipalPermission(SecurityAction.Demand, Role = Roles.User)]
[PrincipalPermission(SecurityAction.Demand, Role =
    @"InternalUnitTesting")]
public POrderDiscrepancyReport TakeOrder(CnTxWrap cn,
    POrderBuilder order)
```
```