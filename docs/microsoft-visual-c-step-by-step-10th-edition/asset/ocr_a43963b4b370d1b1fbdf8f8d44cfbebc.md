```
Customer customer = new Customer
{
  ... 
};
this.DataContext = customer;
```

This statement specifies the object to which controls on the MainPage form should bind. In each of the controls, the XAML markup Text="Binding Path" will be resolved against this object. For example, the id TextBox and cH TextBox controls both specify Text="Binding CustomerID", so they will display the value found in the CustomerID property of the Customer object that the form is bound to.

> Note

In this example, you've set the DataContext property of the form, so the same binding automatically applies to all the controls on the form. You can also set the DataContext property for individual controls if you need to bind specific controls to different objects.

+   12. On the Debug menu, select Start Debugging to build and run the app.

Verify that the form occupies the full screen and displays the details for the customer John Sharp, as shown in the following image: