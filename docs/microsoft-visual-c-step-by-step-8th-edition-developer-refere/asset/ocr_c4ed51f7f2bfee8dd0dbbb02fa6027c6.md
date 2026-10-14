```
public class CustomersController : ApiController
{
    private AdventureWorksEntities db = new AdventureWorksEntities("YourPassword");

    // GET: api/Customers
    public IQueryable<Customer> GetCustomers()
    {
        return db.Customers;
    }
    ...
}
```