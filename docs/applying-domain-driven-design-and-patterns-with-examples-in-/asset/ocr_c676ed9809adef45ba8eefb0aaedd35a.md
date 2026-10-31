```
```csharp
Assert.IsNotNull(o);
}
```
```

Any other tests to write? Sure, what we have been discussing all along is how to deal with the `customer` parameter. So in my opinion an interesting test would be to check that a newly created `order` has a `customer`. I currently don't have verification of that. Let's add a test for doing so.

```
```csharp
[Test]
public void CanCreateOrderWithCustomer()
{
    Order o = new Order(new Customer());

    Assert.IsNotNull(o.Customer);
}
```
```

This test tells me that I need to add a `Customer` field or property on the `Order`. (I think it will be needed not only for my test, but also for some of the requirements.)

In order to cut down the complexity, I decide on a read-only property like this in the `Order` class:

```
```csharp
//Order
public readonly Customer Customer;
```
```

If there is no way to change the `Customer` of the `Order`, we can expect it to be ever-present (and never-changing), and that will simplify the other rules. If you don't need the flexibility...

Now everything compiles and life is good, and we do get a red bar. That's easily fixed by modifying the constructor so it uses the `customer` parameter. The constructor now looks like this, and we get a green bar:

```
```csharp
//Order
public Order (Customer customer)
{
    Customer = customer;
}
```
```

# Some Domain Logic

In Figure 5-2, I mentioned that I should also add `OrderDate` to the `Order`. What could the semantics around that one be? The `order` should probably get an initial `OrderDate` when first created and then a final `OrderDate` when the `order` gets the status of Ordered (or something like that). Let's express that in a test:

```
```csharp
[Test]
public void OrderDateIsCurrentAfterCreation()
{
    DateTime theTimeBefore = DateTime.Now.AddMilliseconds(-1);
```
```