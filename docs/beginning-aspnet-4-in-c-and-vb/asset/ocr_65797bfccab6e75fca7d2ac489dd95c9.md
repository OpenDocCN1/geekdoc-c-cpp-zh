Finally, the serviced component class OrderControl is created to invoke the method NewOrder ():

```
var order = Order.Create("PICCO", DateTime.Today, "Georg Pipps",
    "Salzburg", "Austria");
order.AddOrderLine(OrderLine.Create(16, 17.45F, 2));
order.AddOrderLine(OrderLine.Create(67, 14, 1));
using (var orderControl = new OrderControl())
{
    orderControl.NewOrder(order);
}
```

code snippet ClientApplication/Program.cs

You can try to write products that don't exist to the OrderLine (using a product ID that is not listed in the table Products). In this case, the transaction is aborted, and no data is written to the database.

While a transaction is active, you can see the transaction in the Component Services Explorer by selecting Distributed Transaction Coordinator in the tree view (see Figure 51-10).

![](bbox=[0.2, 0.43, 0.85, 0.5])

![](bbox=[0.15, 0.5, 0.88, 0.85])

# FIGURE 51-10