message parameter to the Text property of the messageBarTextBlock control, followed by a newline character, as shown here in bold:

Click here to view code image

This code causes the message to appear in the message area at the bottom of the form.

+   17. Find the constructor for the MainPage class and add the code shown here in bold:

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

These statements subscribe to the events exposed by the Auditor and Shipper objects. When the events are raised, the displayMessage method runs. Notice that the same method handles both events.

+   18. On the Debug menu, select Start Debugging to build and run the application.

+   19. When the Wide World Importer appears, select some items (at least one age-restricted item), and then select Checkout.

+   20. Verify that the “Audit record written” message appears in the area at the bottom of the form, followed by the “Dispatch note generated” message.