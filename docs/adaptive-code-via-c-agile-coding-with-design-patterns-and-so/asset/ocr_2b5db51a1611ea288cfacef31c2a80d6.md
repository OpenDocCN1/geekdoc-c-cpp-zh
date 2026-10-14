```
{
    public UserRepository()
    {
        users = new List<User>
        {
            new User(Guid.NewGuid()),
            new User(Guid.NewGuid()),
            new User(Guid.NewGuid()),
            new User(Guid.NewGuid())
        };
    }

    public IUser GetByID(Guid userID)
    {
        IUser userFound = users.SingleOrDefault(user => user.ID == userID);
        if(userFound == null)
        {
            userFound = new NullUser();
        }
        return userFound;
    }

    private ICollection<User> users;
}
```

First, this code attempts to retrieve the User from the in-memory collection, which is no change from the previous implementation. Now, though, you check whether the User instance returned is actually a null reference. If it is, you return a special subclass of the IUser type: the NullUser. This subclass overrides the IncrementSessionTicket method to do precisely nothing, as shown in Listing 3-14. In fact, a proper NullUser implementation overrides all methods to do as close to nothing as possible.

# LISTING 3-14 The NullUser method implementations all do nothing.

Click here to view code image

```
public class NullUser : IUser
{
    public void IncrementSessionTicket()
    {
        // do nothing
    }
}
```