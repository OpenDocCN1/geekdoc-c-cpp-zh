```
public class AddressViewModel
{
    public string Name { get; set; }
}
```

then I can create my mapper class like below

```
public static class ViewModelMapper
{
    public static UserViewModel ToViewModel(this UserDTO user)
    {
        return user == null ?
            null :
            new UserViewModel()
            {
                Address = user.Address.ToViewModel()
                // Job = user.Job.ToViewModel(),
                // Contact = user.Contact.ToViewModel() .. and so on
            };
    }

    public static AddressViewModel ToViewModel(this AddressDTO userAddr)
    {
        return userAddr == null ?
            null :
            new AddressViewModel()
            {
                Name = userAddr.Name
            };
    }
}
```

Then finally i can invoke my mapper like below

```
UserDTO userDTOObj = new UserDTO() {
    Address = new AddressDTO() {
        Name = "Address of the user"
    }
};

UserViewModel user = userDTOObj.ToViewModel(); // My DTO mapped to Viewmodel
```

The beauty here is all the mapping method have a common name (ToViewModel) and we can reuse it several ways

# Section 48.16: Using Extension methods to build new collection types (e.g. DictList)

You can create extension methods to improve usability for nested collections like a Dictionary with a List<T> value.

Consider the following extension methods:

```
public static class DictListExtensions
{
    public static void Add<TKey, TValue, TCollection>(this Dictionary<TKey, TCollection> dict, TKey key, TValue value)
        where TCollection : ICollection<TValue>, new()
    {
        TCollection list;
```