```
var customerNames =
    customers.Select(cust => new { FirstName = cust.FirstName, LastName = cust.LastName });
```