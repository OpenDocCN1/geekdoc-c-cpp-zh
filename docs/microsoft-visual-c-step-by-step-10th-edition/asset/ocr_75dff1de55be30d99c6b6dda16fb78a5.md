```
public ViewModel()
{
    this.customers = new List<Customer>
    {
        new Customer
        {
            CustomerID = 1,
            Title = "Mr",
            FirstName="John",
            LastName="Sharp",
            EmailAddress="john@contoso.com",
            Phone="111-1111"
        },
        new Customer
        {
            CustomerID = 2,
            Title = "Mrs",
            FirstName="Diana",
            LastName="Sharp",
            EmailAddress="diana@contoso.com",
            Phone="111-1112"
        },
        new Customer
        {
            CustomerID = 3,
            Title = "Ms",
            FirstName="Francesca",
            LastName="Sharp",
            EmailAddress="frankie@contoso.com",
            Phone="111-1113"
        }
    };
};
```

The ViewModel class uses a List<Customer> object as its model, and the constructor populates it with some sample data. Strictly speaking, this data should be held in a separate Model class, but for the purposes of this exercise we will make do with this sample data.

+   5. Add the private variable currentCustomer shown in bold in the following code to the ViewModel class, and initialize this variable to zero in the constructor:

Click here to view code image