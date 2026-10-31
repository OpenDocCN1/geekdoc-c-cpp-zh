```
```csharp
txtCustomerNumber.Text =
    _customer.CustomerNumber.ToString();
txtName.Text = _customer.Name;

//Paint the orders:
foreach (Order o in theOrders)
{
    //TODO...
}
```
```

Something that is worth pointing out is that I expect the usage of Null Object [Woolf Null Object] in the previous code when I paint the orders. Because of that, all orders will have a `ReferencePerson` (an empty one), even if it hasn't been decided yet, so I don't need any null checks. In my opinion, this is an example of a detail that shows how to increase the simplicity for the UI programmer.

Having to write the code by hand for filling the UI was a bit tedious. But looking back at it, isn’t it extremely simple to read so far? Sure, we are trying out simple things, but still.

# Add an Order

The other form example is one for making it possible to add an order. I’m envisioning that you have first selected the customer and then you get a form like the one shown in Figure 4-15.

**Figure 4-15. Form for adding an order**