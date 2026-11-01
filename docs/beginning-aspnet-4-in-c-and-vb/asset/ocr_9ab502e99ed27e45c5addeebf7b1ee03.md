enumeration value of Domain, Machine, or ApplicationDirectory, depending on whether the directory service, the local accounts of the machine, or an application directory should be used. If the current user does not have access to add accounts to Active Directory, you can also set a user and password with the PrincipalContext that is used to access the server.

Next, you can create an instance of UserPrincipal passing the principal context, and setting all required properties. Here, the GivenName and EmailAddress properties are set. Finally, you must invoke the Save() method of the UserPrincipal to write the new user to the store:

```
```csharp
using (var context = new PrincipalContext(ContextType.Domain, "cninnovation"))
using (var user = new UserPrincipal(context, "Tom", "P@ssw0rd", true)
{
    GivenName = "Tom",
    EmailAddress = "test@test.com"
})
{
    user.Save();
}
```
```

code snippet AccountManagementSamples/Program.cs

# Reset a Password

To reset a password from an existing user, you can use the SetPassword() method from a UserPrincipal object:

```
```csharp
using (var context = new PrincipalContext(ContextType.Domain, "cninnovation"))
using (var user = UserPrincipal.FindByIdentity(context, IdentityType.Name, "Tom"))
{
    user.SetPassword("P@ssw0rd");
    user.Save();
}
```
```

code snippet AccountManagementSamples/Program.cs

The user running this code needs to have the privilege to reset a password. To change the password from an old one to a new one, you can use the method ChangePassword().

# Create a Group

A new group can be created in a similar way to creating a new user. Here, just the class GroupPrincipal is used instead of the class UserPrincipal. As in creating a new user, the properties are set, and the Save() method is invoked:

```
```csharp
using (var ctx = new PrincipalContext(ContextType.Domain, "cninnovation"))
using (var group = new GroupPrincipal(ctx)
{
    Description = "Sample group",
    DisplayName = "Wrox Authors",
    Name = "WroxAuthors"
})
{
    group.Save();
}
```
```

code snippet AccountManagementSamples/Program.cs