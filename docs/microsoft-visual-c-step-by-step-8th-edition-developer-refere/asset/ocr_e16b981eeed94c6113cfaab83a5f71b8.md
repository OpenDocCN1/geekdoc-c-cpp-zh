Notice how the same binding expression can be used with more than one control. For example, the expression {Binding CustomerID} is referenced by the id and cId TextBox controls, which causes both controls to display the same data.

9. In Solution Explorer, expand the MainPage.xaml file, and then double-click the MainPage.xaml.cs file to display the code for the MainPage.xaml form in the Code and Text Editor window. Add the statement shown below in bold to the MainPage constructor.

Click here to view code image

```
public MainPage()
{
    this.InitializeComponent();

    Customer customer = new Customer
    {
        CustomerID = 1,
        Title = "Mr",
        FirstName = "John",
        LastName = "Sharp",
        EmailAddress = "john@contoso.com",
        Phone = "111-1111"
    };
}
```

This code creates a new instance of the Customer class and populates it with some sample data.

10. After the code that creates the new Customer object, add the following statement shown in bold:

Click here to view code image

```
Customer customer = new Customer
{
    ...
};

this.DataContext = customer;
```

This statement specifies the object to which controls on the MainPage form should bind. In each of the controls, the XAML markup Text="{Binding Path}" will be resolved against this object. For example, the id TextBox and cId TextBox controls both specify Text="{Binding CustomerID}", so they will display the value found in the CustomerID property of the Customer object to which the form is bound.