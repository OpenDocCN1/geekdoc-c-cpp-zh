5. Locate the AuditOrder method. This is the method that is run by using the delegate in the CheckoutController object. It invokes another private method called doAuditing to actually perform the audit operation. The method looks like this:

Click here to view code image

```
public void AuditOrder(Order order)
{
    this.doAuditing(order);
}
```

6. Scroll down to the doAuditing method. The code in this method is enclosed in a try/catch block; it uses the XML APIs of the .NET Framework class library to generate an XML representation of the order being audited and saves it to a file. (The exact details of how this works are beyond the scope of this chapter.)
After the catch block, add a finally block that raises the AuditProcessingComplete event, as shown in the following in bold:

Click here to view code image

```
private async void doAuditing(Order order)
{
    List<OrderItem> ageRestrictedItems =
    findAgeRestrictedItems(order);
    if (ageRestrictedItems.Count > 0)
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
            if (this.AuditProcessingComplete != null)
            {
                this.AuditProcessingComplete(
                    $"Audit record written for Order {order.OrderID}");
            }
        }
    }
}
```

7. In the DeliveryService project, open the Shipper.cs file in the Code and Text Editor window.

8. Add a public delegate called ShippingCompleteDelegate to the Shipper class. This delegate should specify a method that takes a string parameter called message and that returns a void. The code in bold in the following