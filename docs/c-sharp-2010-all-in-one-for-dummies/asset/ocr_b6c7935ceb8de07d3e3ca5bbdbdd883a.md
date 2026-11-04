# State versus behavior testing

State-based testing tests the values of an object (for example, whether the IsDirty flag is set). Behavior testing is used to test actions and interactions of objects. To test that a particular method was called or an event was raised becomes much more trivial with the more advanced frameworks like RhinoMocks.

# Listing 4-19: Fake SalesRegion Repository

```
public class SalesRegionRepositoryFake : IRepository<SalesRegion>
{
    public IList<SalesRegion> GetAll()
    {
        var list = new ObservableCollection<SalesRegion>
        {
            new SalesRegion (ID = 1, Name = "East"),
            new SalesRegion (ID = 2, Name = "Central"),
            new SalesRegion (ID = 3, Name = "West")
        };
        return list;
    }

    public bool Update(SalesRegion region)
    {
        throw new NotImplementedException();
    }
}
```

To create a customer, a list of Sales Regions must be available, so the Customer Repository Fake (as shown in Listing 4-20) uses Constructor Injection to insert the allowable values into the repository. It could have created its own list, but that would have thrown off the binding in XAML since the objects would be different.

# Listing 4-20: Fake Customer Repository

```
public class CustomerRepositoryFake : IRepository<Customer>
{
    readonly IList<SalesRegion> _salesRegions;
    public CustomerRepositoryFake(IList<SalesRegion> salesRegions)
    {
        _salesRegions = salesRegions;
    }
}
```