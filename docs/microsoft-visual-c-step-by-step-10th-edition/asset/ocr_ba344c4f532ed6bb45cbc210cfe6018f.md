```
CancellationToken tok = ...;
...
var orderInfoQuery =
    from c in CustomersInMemory.Customers.
    AsParallel()..WithCancellation(tok)
    join o in OrdersInMemory.Orders.AsParallel()
    on ...
```