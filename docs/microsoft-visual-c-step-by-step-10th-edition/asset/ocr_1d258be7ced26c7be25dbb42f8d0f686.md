6. Scroll down to the doAuditing method. The code in this method is enclosed in a try/catch block; it uses the XML APIs of the .NET class library to generate an XML representation of the order being audited and saves it to a file. (The exact details of how this works are beyond the scope of this book.)

7. After the catch block, add a finally block that raises the AuditProcessingComplete event, as shown in bold in the following:

Click here to view code image

```
private async void doAuditing(Order order)
{
    List<ageRestrictedItem> ageRestrictedItems = findAgeRestrictedItems(order);
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
            if (this.AuditProcessingComplete is not null)
            {
                this.AuditProcessingComplete("Audit record written for Order(order.OrderId)");
            }
        }
    }
}
```

8. In the DeliveryService project, open the Shipper.cs file in the Code and Text Editor window.

9. Add a public delegate called ShippingCompleteDelegate to the Shipper class. This delegate should specify a method that takes a string parameter and returns a void. The code in bold in the following shows the definition of this delegate:

Click here to view code image

```
public class Shipper
{
```