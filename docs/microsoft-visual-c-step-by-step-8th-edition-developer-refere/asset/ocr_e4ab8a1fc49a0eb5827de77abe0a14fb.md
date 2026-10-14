example shows the definition of this delegate:

Click here to view code image

```
class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    ...
}
```

9. Add to the Shipper class a public event called ShipProcessingComplete based on the ShippingCompleteDelegate delegate as shown in bold in the following code:

Click here to view code image

```
class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    public event ShippingCompleteDelegate ShipProcessingComplete;
    ...
}
```

10. Find the doShipping method, which is the method that performs the shipping logic. In the method, after the catch block, add a finally block that raises the ShipProcessingComplete event, as shown here in bold:

Click here to view code image

```
private async void doShipping(Order order)
{
    try
    {
        ...
    }
    catch (Exception ex)
    {
        ...
    }
    finally
    {
        if (this.ShipProcessingComplete != null)
        {
            this.ShipProcessingComplete(
                $"Dispatch note generated for Order {order.OrderID}");
        }
    }
}
```

11. In the Delegates project, display the layout for the MainPage.xaml file in the Design View window. In the XAML pane, scroll down to the first set of RowDefinition items. The XAML code looks like this: