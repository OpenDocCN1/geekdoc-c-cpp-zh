Checking for null values indicates that you are placing too much unnecessary burden on all of the clients of IRepository. The more clients that use this method, the greater the probability of forgetting a null reference check. Instead, you should change the source of the problem to perform the check for you, as shown in Listing 4-13.

# LISTING 4-13 The service code should implement the Null Object pattern.

```
public class UserRepository : IUserRepository
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

First, this code attempts to retrieve the User from the in-memory collection, which is no change from the previous usage shown in Listing 4-12. Now, though, you check whether the User instance returned is actually a null reference. If it is, you return a special subclass of the IUser type: the NullUser. This subclass overrides the IncrementSessionTicket method to do precisely nothing, as shown in Listing 4-14. In fact, a proper NullUser implementation overrides all methods to do as close to nothing as possible.

# LISTING 4-14 The NullUser method implementations all do nothing.

```
public class NullUser : IUser
{
    public void IncrementSessionTicket()
    {
        // do nothing
    }
}
```