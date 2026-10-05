
1. Return to Visual Studio 2022 and display the Delegates solution.

2. In the AuditService project, open the Auditor.cs file in the Code and Text Editor window.

3. Add a public delegate called AuditingCompleteDelegate to the Auditor class. This delegate should specify a method that takes a string parameter and returns a void. The code in bold in the following example shows the definition of this delegate:

Click here to view code image

```
public class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    ...
}
```

4. Add a public event called AuditProcessingComplete to the Auditor class, after the AuditingCompleteDelegate delegate. This event should be based on the AuditingCompleteDelegate delegate as shown in bold in the following code:

Click here to view code image

```
public class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    public event AuditingCompleteDelegate AuditProcessingComplete;
    ...
}
```

5. Locate the AuditOrder method. This is the method that is run using the delegate in the CheckoutController object. It invokes another private method doAuditing to actually perform the audit operation. The method looks like this:

Click here to view code image

```
public void AuditOrder(Order order)
{
    this.doAuditing(order);
}
```

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
public delegate void ShippingCompleteDelegate(string message);
...
}
```

10. Add a public event called ShippingProcessingComplete to the Shipper class, based on the ShippingCompleteDelegate delegate as shown in bold in the following code:

Click here to view code image

```
public class Shipper
{
    public delegate void ShippingCompleteDelegate(string message);
    public event ShippingCompleteDelegate ShippingProcessingComplete;
    ...
}
```

11. Find the doShipping method, which is the method that performs the shipping logic. In the method, after the catch block, add a finally block that raises the ShipProcessingComplete event, as shown here in bold:

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
        if (this.ShipProcessingComplete is not null)
        {
            this.ShipProcessingComplete("Dispatch note generated for Order "+order.OrderID);
        }
    }
}
```

12. In the Delegates project, display the layout for the MainPage.xaml file in the Design View. Then, in the XAML pane, scroll down to the first set of RowDefinition items. The XAML code looks like this:

Click here to view image

```
<Grid Background="StaticResource
  ApplicationPageBackgroundThemeBrush">
  <Grid Margin="12,0,12,12" Loaded="MainPageLoaded">
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="2*"/>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
    <RowDefinition Height="*"/>
  </Grid.RowDefinitions>
...
```

13. Change the Height property of the final RowDefinition item to 2* as shown in bold in the following code:

Click here to view image

```
<Grid.RowDefinitions>
...
  <RowDefinition Height="10*"/>
  <RowDefinition Height="2*"/>
</Grid.RowDefinitions>
```

This change in the layout makes a bit of space available at the bottom of the form. You'll use this space to display the messages received from the Auditor and Shipper components when they raise their events. Chapter 25, “Implementing the user interface for a Universal Windows Platform app,” provides more detail on laying out user interfaces using a Grid control.

14. Scroll to the bottom of the XAML pane and add the following ScrollViewer and TextBlock elements shown in bold before the penultimate </Grid> tag:

Click here to view image

```
...
  <ScrollView Grid.Row="4"
  VerticalScrollBarVisibility="Visible">
    <TextBlock x:Name="messageBar" FontSize="18" />
  </ScrollView>
</Grid>
</Page>
```

This markup adds a TextBlock controlled messageBar to the area at the bottom of the screen. You'll use this control to display messages from the Auditor and Shipper objects. Again, you'll learn more about grid layouts in Chapter 25.

15. Display the MainPage.xaml.cs file in the Code and Text Editor window. Then find the CheckoutButtonClicked method and remove the code that displays the summary of the order. The try block should look like this after you've deleted the code:

Click here to view code image

```
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
try {
    // Perform the checkout processing
    this.checkoutController.StartCheckoutProcessing(this.order);
    // Deleted code was here
    // Clear out the order details so the user can start again
    this.order = new Order
    {
        Date = DateTime.Now,
        Items = new List<OrderItem>(),
        OrderID = Guid.NewGuid(),
        TotalValue = 0
    }
    this.orderDetails.DataContext = null;
    this.orderDetails.Text = $
```

16. Add a private method called displayMessage to the MainPage class. This method should take a string parameter called message and should return a void. In the body of this method, add a statement that appends the value in the

message parameter to the Text property of the messageBarTextBlock control, followed by a newline character, as shown here in bold:

Click here to view code image

This code causes the message to appear in the message area at the bottom of the form.

17. Find the constructor for the MainPage class and add the code shown here in bold:

Click here to view code image

```
public MainPage()
{
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
    this.auditor.AuditOrder +=;
    this.checkoutController.CheckoutProcessing +=;
    this.auditor.AuditProcessingComplete += this.displayMessage;
    this.shipper.ShipProcessingComplete += this.displayMessage;
}
```

These statements subscribe to the events exposed by the Auditor and Shipper. When the events are raised, the displayMessage method runs. Notice that the same method handles both events.

18. On the Debug menu, select Startging to build and run the application.

19. When the Wide Importer appears, select some items (at least one age-restricted item), then select Checkout.

20. Verify that the “Audit record written” message appears in the area at the bottom of the form, followed by the “dispatch note generated” message.

# Wide Importers

| Hammer | Name: Power Saw | Order Details |
|---|---|---|
| 24oz heavy-duty claw hammer | Description: Rotary action, high powered | |
| £18.35 | Price: £88.00 | |
| No | Age Restricted: Yes | |
| | Total: £0.00 | |
| | | Checkout |

Audit record written for Order 24975f99-cddf-4521-850d-2547ccde3dda
Dispatch note generated for Order 24975f99-cddf-4521-850d-2547ccde3dda

21. Place further orders and note the new messages that appear each time you select Checkout. You might need to scroll down to see them when the message area fills up.

22. When you've finished, return to Visual Studio 2022 and stop debugging.

# Summary

In this chapter, you learned how to use delegates to reference methods and invoke those methods. You also saw how to define lambda expressions that can run by using a delegate. Finally, you learned how to define and use events to trigger execution of a method.

- If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 21.
