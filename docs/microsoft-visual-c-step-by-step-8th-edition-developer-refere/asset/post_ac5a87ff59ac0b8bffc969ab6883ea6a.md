
In fact, there is no guarantee that the processing performed by the delegated methods has completed by the time the dialog box appears, so the message could actually be misleading. This is where an event is invaluable. The Auditor and Shipper components could both publish an event to which the application subscribes. This event could be raised by the components only when they have completed their processing. When the application receives this event, it can display the message, safe in the knowledge that it is now accurate.

In the following exercise, you will modify the Auditor and Shipper classes to raise an event that occurs when they have completed their processing. The application will subscribe to the event for each component and display an appropriate message when the event occurs.

## Add an event to the CheckoutController class

- 1. Return to Visual Studio 2015 and display the Delegates solution.
- 2. In the AuditService project, open the Auditor.cs file in the Code and Text Editor window.
- 3. Add to the Auditor class a public delegate called AuditingCompleteDelegate. This delegate should specify a method that takes a string parameter called message and that returns a void. The code in bold in the following example shows the definition of this delegate:

Click here to view code image

```
class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    ...
}
```

- 4. Add to the Auditor class a public event called AuditProcessingComplete, after the AuditingCompleteDelegate delegate. This event should be based on the AuditingCompleteDelegate delegate as shown in bold in the following code:

Click here to view code image

```
class Auditor
{
    public delegate void AuditingCompleteDelegate(string message);
    public event AuditingCompleteDelegate AuditProcessingComplete;
    ...
}
```

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

Click here to view code image

```
<Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
    <Grid Margin="12,0,12,0" Loaded="MainPageLoaded">
        <Grid.RowDefinitions>
            <RowDefinition Height="*"/>
            <RowDefinition Height="2*"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="10*"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ...
```

12. Change the Height property of the final RowDefinition item to 2* as shown in bold in the following code:

Click here to view code image

```
<Grid.RowDefinitions>
    ...
    <RowDefinition Height="10*"/>
    <RowDefinition Height="2*"/>
</Grid.RowDefinitions>
```

This change in the layout makes available a bit of space at the bottom of the form. You will use this space as an area for displaying the messages received from the Auditor and Shipper components when they raise their events. Chapter 25, “Implementing the user interface for a Universal Windows Platform app,” provides more detail on laying out user interfaces by using a Grid control.

13. Scroll to the bottom of the XAML pane. Add the following ScrollViewer and TextBlock elements shown in bold before the penultimate </Grid> tag:

Click here to view code image

```
...
    </Grid>
    <ScrollViewer Grid.Row="4" VerticalScrollBarVisibility="Visible">
        <TextBlock x:Name="messageBar" FontSize="18" />
    </ScrollViewer>
    </Grid>
</Grid>
</Page>
```

This markup adds a TextBlock control called messageBar to the area at the bottom of the screen. You will use this control to display messages from the Auditor and Shipper objects.

14. Display the MainPage.xaml.cs file in the Code and Text Editor window. Find the CheckoutButtonClicked method and remove the code that displays the summary of the order. The try block should look like this after you have

deleted the code:

Click here to view code image

```
private void CheckoutButtonClicked(object sender, RoutedEventArgs e)
{
    try
    {
        // Perform the checkout processing
        this.checkoutController.StartCheckoutProcessing(this.order
        // Clear out the order details so the user can start
again with a new order
        this.order = new Order { Date = DateTime.Now, Items = new List<OrderItem>(),
            OrderID = Guid.NewGuid(),
TotalValue = 0 };
        this.orderDetails.DataContext = null;
        this.orderValue.Text = $"{order.TotalValue:C}";
        this.listViewHeader.Visibility = Visibility.Collapsed;
        this.checkout.IsEnabled = false;
    }
    catch (Exception ex)
    {
        ...
    }
}
```

15. Add a private method called displayMessage to the MainPage class. This method should take a string parameter called message and should return a void. In the body of this method, add a statement that appends the value in the message parameter to the Text property of the messageBar TextBlock control, followed by a newline character, as shown here in bold:

Click here to view code image

```
private void displayMessage(string message)
{
    this.messageBar.Text += message + "\n";
}
```

This code causes the message to appear in the message area at the bottom of the form.

16. Find the constructor for the MainPage class and add the code shown here in bold:

Click here to view code image

```
public MainPage()
{
    ...
    this.auditor = new Auditor();
    this.shipper = new Shipper();
    this.checkoutController = new CheckoutController();
```
