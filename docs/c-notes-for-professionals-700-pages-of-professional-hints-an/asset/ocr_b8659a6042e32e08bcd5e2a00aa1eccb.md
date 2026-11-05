# # Section 66.23: Joining multiple sequences

Consider entities Customer, Purchase and PurchaseItem as follows:

```
```csharp
public class Customer
{
    public string Id { get; set; } // A unique Id that identifies customer
    public string Name {get; set; }
}

public class Purchase
{
    public string Id { get; set; }
    public string CustomerId {get; set; }
    public string Description { get; set; }
}

public class PurchaseItem
{
    public string Id { get; set; }
    public string PurchaseId {get; set; }
    public string Detail { get; set; }
}
```
```

Consider following sample data for above entities:

```
```csharp
var customers = new List<Customer>()
{
    new Customer() {
        Id = Guid.NewGuid().ToString(),
        Name = "Customer1"
    },

    new Customer() {
        Id = Guid.NewGuid().ToString(),
        Name = "Customer2"
    }
};

var purchases = new List<Purchase>()
{
    new Purchase() {
        Id = Guid.NewGuid().ToString(),
        CustomerId = customers[0].Id,
        Description = "Customer1-Purchase1"
    },

    new Purchase() {
        Id = Guid.NewGuid().ToString(),
        CustomerId = customers[0].Id,
        Description = "Customer1-Purchase2"
    },

    new Purchase() {
        Id = Guid.NewGuid().ToString(),
        CustomerId = customers[1].Id,
        Description = "Customer2-Purchase1"
    },

    new Purchase() {
        Id = Guid.NewGuid().ToString(),
```
```