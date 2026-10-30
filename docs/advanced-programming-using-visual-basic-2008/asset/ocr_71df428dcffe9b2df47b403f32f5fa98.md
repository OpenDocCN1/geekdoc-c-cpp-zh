```
```vb
Private Sub DisplayButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles DisplayButton.Click
    ' Display the Hello World message from the service.

    Dim HelloService As New HelloService.HelloWorldServiceClient

    WelcomeLabel.Text = HelloService.HelloWorld
End Sub
```
```

**STEP 2:** Add comments to the form class.

# Run the Completed Application

**STEP 1:** Run the program without debugging (Ctrl + F5). Unless you allow the WCF Service project to add debugging support, you will receive an error message there if you run with debugging (F5). The completed form is shown in Figure 6.8.

*Note:* Have patience. You may think that nothing is happening; it takes a while for this to run. If you are running additional firewall software, you may need to reply to a message to allow Visual Studio access to the local network.

![](bbox=[0.121, 0.433, 0.527, 0.728])

> The completed form that consumes the HelloWorld service.

# Feedback 6.3

Write the code to instantiate a service object from InventoryService.

# Performing Calculations in a WCF Service

This next example service performs a calculation. We will pass the ExtendedPrice method two arguments (price and quantity) and the method will calculate and return the extended price.

The first step is to add the ExtendedPrice contract to IHelloWorldService, then add the following ExtendedPrice method to the HelloWorldService class.