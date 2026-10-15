samples in this book, keep in mind that the XAML you’re looking at is really nothing more than a declarative, designer-friendly view of a set of object instantiation and configuration statements.

Take a look at the following bit of XAML. It creates an instance of an object of type Customer and then sets several properties, including properties which are themselves instances of other objects like Address.

```
<cust:Customer
    FirstName="John"
    LastName="Doe"
    PhoneNumber="888-555-1212">
    <cust:Customer.Address>
        <cust:Address
            Line1="12 Somewhere St"
            Line2=""
            City="Somewhere"
            State="CA"
            Zip="90210"/>
    </cust:Customer.Address>
</cust:Customer>
```

In the preceding XAML, we’re using an XML namespace prefix. In XAML, we can associate an XML namespace prefix with a .NET namespace. In the preceding sample, we might have associated the cust XML namespace prefix with the MySamples.Customer namespace using the following XAML:

```
xmlns:cust="clr-namespace:MySamples.Customer"
```

Keeping in mind that XAML has no tight coupling to any UI system and is just a generic way of instantiating via XML, we can assume that the preceding XAML is functionally equivalent to the following C# block:

```
Customer c = new Customer()
{
    FirstName = "John",
    LastName = "Doe",
    PhoneNumber = "888-555-1212",
    Address = new Address()
    {
        Line1="12 Somewhere St",
        Line2="",
        City="Somewhere",
        State="CA",
        Zip="90210"
    }
};
```