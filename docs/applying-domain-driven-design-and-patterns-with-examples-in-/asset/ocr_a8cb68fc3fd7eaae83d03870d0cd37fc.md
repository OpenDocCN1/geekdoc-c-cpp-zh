OrderRepository like this:

```
[Test]
public void CanGetOrdersForCustomer()
{
    Customer newCustomer = _CreateACustomerAndAnOrder
    ("Ronneby", 20000);

    IList ordersForTheNewCustomer =
    _repository.GetOrders(newCustomer);

    Assert.AreEqual(1, ordersForTheNewCustomer.Count);
}
```

I could let the Customer have an OrderList property and implicitly talk to the Repository, but I think the explicitness is better here. I also avoid coupling between the Customer and the OrderRepository.

The total value of each order is worth a separate mention. It's probably trickier than first expected as the calculation needs all orderLines of the order. Sure, that's not tricky, but it does alarm me. I know this is premature, but I can't help it (because loading the orderLines will be expensive when you just want to show a pretty large list of orders for a certain customer, for example). I think one helpful strategy is that if the orderLines aren't loaded, a simple amount field, which probably is stored in the Orders table, is used for the TotalAmount property. If orderLines are loaded, a complete calculation is used instead for the TotalAmount property.

This isn't something we need to think about right now. And no matter what, for consumers, it's as simple as this:

```
[Test]
public void CanGetTotalAmountForOrder()
{
    Customer newCustomer = _CreateACustomerAndAnOrder
    ("Ronneby", 420);

    Order newOrder = (Order)_repository.GetOrders
    (newCustomer)[0];

    Assert.AreEqual(420, newOrder.TotalAmount);
}
```

In my opinion, the "right" way to think about this is that lines are there because we work with an Aggregate and the lines are an intimate part of the order. That might mean that performance would suffer in certain situations. If so, we might have to solve this with the Lazy Load pattern [Fowler PoEAA] (used to load lists from the database just in time, for example) or a read-only, optimized view.

But, as I said, that's something we should deal with when we have found out that the simple and direct solution isn't good enough.