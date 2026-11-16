This query groups people by their age, sorts the groups by age in ascending order, and then prints the groups and their members.

# 3. Joining Data

```
C#
List<Order> orders = new List<Order>
{
    new Order { OrderId = 1, CustomerId = 101 },
    new Order { OrderId = 2, CustomerId = 102 },
    new Order { OrderId = 3, CustomerId = 101 }
};

List<Customer> customers = new List<Customer>
{
    new Customer { CustomerId = 101, Name = "Alice" },
    new Customer { CustomerId = 102, Name = "Bob" }
};

var customerOrders = from order in orders
                     join customer in customers on order.CustomerId equals customer.CustomerId
                     select new { CustomerName = customer.Name, OrderId = order.OrderId };

foreach (var item in customerOrders)
{
    Console.WriteLine(item.CustomerName + " - Order ID: " + item.OrderId);
}
```