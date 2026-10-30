# LISTING 3-8 An improvement is made to all clients of SecurityService.

```
[HttpPost]
public void ChangePassword(Guid userID, string newPassword)
{
    this.securityService.ChangeUsersPassword(userID, newPassword);
}
//...
public class SecurityService
{
    public void ChangeUsersPassword(Guid userID, string newPassword)
    {
        var userRepository = new UserRepository();
        var user = userRepository.GetByID(userID);
        user.ChangePassword(newPassword);
    }
}
```

This is definitely an improvement for the AccountController, but the ChangeUsersPassword method is still directly instantiating the UserRepository.

# Alternatives to object construction

What would improve the AccountController and SecurityService—or any other example of inappropriate object construction? How can they be made demonstrably correct so that none of the aforementioned problems apply? There are a few options, all complementary, that you can choose from.

# Coding to an interface

The first and most important change that you should make is to hide the implementation of SecurityService behind an interface. This allows the AccountController to depend only on the interface, and not on the implementation, of SecurityService. The first refactor is to extract an interface out of SecurityService, as shown in Listing 3-9.

# LISTING 3-9 Extracting an interface from SecurityService.

```
public interface ISecurityService
{
    void ChangeUsersPassword(Guid userID, string newPassword);
}
//...
public class SecurityService : ISecurityService
{
    public ChangeUsersPassword(Guid userID, string newPassword)
    {
        //...
    }
}
```