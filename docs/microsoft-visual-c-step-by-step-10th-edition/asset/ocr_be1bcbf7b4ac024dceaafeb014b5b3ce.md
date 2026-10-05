command bar at the base of the page and indicates which record is currently displayed. The Run element of a TextBlock control enables you to display multiple text items as part of the same control.

Click here to view code image

```
<Page.BottomAppBar>
<CommandBar>
  <AppBarElementContainer VerticalAlignment="Center">
    <TextBlock Padding="0, 0, 20, 0">
      <Run Text="{Binding Path=CurrentCustomerIndex}" />
      <Run Text=" />
      <Run Text="{Binding Path=CustomerListCount}" />
    </TextBlock>
  </AppBarElementContainer>
</CommandBar>
</Page.BottomAppBar>
```

You can now update the ViewModel class to call the web service to fetch customer data.

# To fetch data from the Adventure works service

+   1. In Solution Explorer, right-click the Customers project and select Manage NuGet Packages.
2. In the NuGet Package Manager window, on the Browse tab, type System.Text.Json.
3. Select the System.Text.Json package (make sure it's version 6.0.0 or later) and select Install. Then, in the Preview Changes dialog, select OK.
4. Open the ViewModel.cs file in the Code and Text editor window.
5. Add the following using directives to the list at the top of the file:

The System.Text.Json package contains utilities for serializing and deserializing JSON text and converting objects into your application.
Open the ViewModel.cs file in the Code and Text editor window.

Click here to view code image

```
using System.Net.Http;
using System.Text.Json;
```

+   6. In the ViewModel class, add the following private fields directly above the constructor. In the statement that initializes the ServerUrl variable, replace