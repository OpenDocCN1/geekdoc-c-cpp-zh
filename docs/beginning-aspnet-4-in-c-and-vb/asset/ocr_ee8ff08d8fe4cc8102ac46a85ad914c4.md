# Add a User to a Group

To add a user to a group, you can use a GroupPrincipal and add a UserPrincipal to the Members property of the group. To get an existing user and group, you can use the static method FindByIdentity():

```
using (var context = new PrincipalContext(ContextType.Domain))
using (var group = GroupPrincipal.FindByIdentity(
    context, IdentityType.Name, "WroxAuthors"))
using (var user = UserPrincipal.FindByIdentity(
    context, IdentityType.Name, "Stephanie Nagel"))
{
    group.Members.Add(user);
    group.Save();
}
```

code snippet AccountManagementSamples/Program.cs

# Finding Users

Static methods of the UserPrincipal object allow finding users based on some predefined criteria. The sample here shows finding users who didn't change their passwords within the last 30 days by using the method FindPasswordSetTime(). This method returns a PrincipalSearchResult<UserPrincipal> collection that is iterated to display the user name, the last logon time, and the time when the password was reset:

```
using (var context = new PrincipalContext(ContextType.Domain, "explorer"))
using (var users = UserPrincipal.FindByPasswordSetTime(context,
    DateTime.Today-TimeSpan.FromDays(30), MatchType.LessThan))
{
    foreach (var user in users)
    {
        Console.WriteLine("{0}, last logon: {1}, " +
            "last password change: {2}", user.Name, user.LastLogon,
            user.LastPasswordSet);
    }
}
```

code snippet AccountManagementSamples/Program.cs

Other methods offered by the UserPrincipal class to find users are FindByBadPasswordAttempt(), FindByExpirationTime(), FindByLockoutTime(), and FindByLogonTime().

You can get more flexibility in finding users by using the PrincipalSearcher class. This class is an abstraction of the DirectorySearcher class and uses this class behind the scenes. With the PrincipalSearcher class, you can assign any Principal object to the QueryFilter property.

In the example here, a UserPrincipal object with the properties Surname and Enabled is set to the QueryFilter. This way, all user objects starting with the surname Nag and that are enabled are returned with the PrincipalSearchResult collection. The PrincipalSearcher class creates an LDAP query string to do the search.

```
var context = new PrincipalContext(ContextType.Domain);

var userFilter = new UserPrincipal(context);
userFilter.Surname = "Nag*";
userFilter.Enabled = true;

using (var searcher = new PrincipalSearcher())
{
    searcher.QueryFilter = userFilter;
    var searchResult = searcher.FindAll();
    foreach (var user in searchResult)
```