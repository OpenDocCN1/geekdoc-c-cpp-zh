
classes of user: Organizational-Person, Person, and Top. In this program, the names of the base classes are hard-coded. You could also read the base class dynamically with the subClassOf attribute.

GetSchemaProperties() returns IEnumerable<string> with all property names of the specific object type. All the property names are added to the list box:

```
private void SetUserProperties(string schemaNamingContext)
{
    var properties = from p in GetSchemaProperties(schemaNamingContext, "User").Concat(
                        GetSchemaProperties(schemaNamingContext, "Organizational-Person")).Concat(
                        GetSchemaProperties(schemaNamingContext, "Top"))
                    orderby p
                    select p;

    listBoxProperties.DataContext = properties;
}
```

code snippet UserSearch/MainWindow.xaml.cs

In GetSchemaProperties(), you are accessing the Active Directory service again. This time, rootDSE is not used but rather the LDAP name of the schema that you discovered earlier. The property systemMayContain holds a collection of all attributes that are allowed in the class objectType:

```
private IEnumerable<string> GetSchemaProperties(string schemaNamingContext, string objectType)
{
    IEnumerable<string> data;
    using (var de = new DirectoryEntry())
    {
        de.Username = username;
        de.Password = password;

        de.Path = String.Format("LDAP://{0}/CN={1},{2}", hostname, objectType, schemaNamingContext);

        PropertyValueCollection values = de.Properties["systemMayContain"];
        data = from s in values.Cast<string>()
               orderby s
               select s;
    }
    return data;
}
```

Step 2 in the application is completed. The ListBox control has all the property names of the user objects.

## Search for User Objects

The handler for the search button calls only the helper method FillResult():

```
private void OnSearch(object sender, RoutedEventArgs e)
{
    try
    {
        FillResult();
```

| CLASS | DESCRIPTION |
|---|---|
| UserPrincipal, ComputerPrincipal | UserPrincipal and ComputerPrincipal derive from the base class AuthenticablePrincipal and, thus, have all properties and methods the base class has. UserPrincipal is the object that maps to a user account, and ComputerPrincipal maps to a computer account. With UserPrincipal, you have many properties to get and set information about the user, for example, EmployeeId, EmailAddress, GivenName, and VoiceTelephoneNumber. |
| GroupPrincipal | Groups cannot authenticate; that's why GroupPrincipal derives directly from the Principal class. With GroupPrincipal, you can get members of the group with the Members property and the GetMembers() method. |
| PrincipalCollection | The PrincipalCollection contains a group of Principal objects; for example, the Members property from the GroupPrincipal class returns a PrincipalCollection object. |
| PrincipalSearcher | PrincipalSearcher is an abstraction of the DirectorySearcher class with special use for account management. With PrincipalSearcher, there's no need to know about the LDAP query syntax because this is created automatically. |
| PrincipalSearchResult<T> | Search methods from the PrincipalSearcher and Principal classes return a PrincipalSearchResult<T>. |

The following sections look at some scenarios in which you can use the classes from the System.DirectoryServices.AccountManagement namespace.

## Display User Information

The static property Current of the UserPrincipal class returns a UserPrincipal object with information about the currently logged-on user:

```csharp
using (var user = UserPrincipal.Current)
{
    Console.WriteLine("Context Server: {0}", user.Context.ConnectedServer);
    Console.WriteLine(user.Description);
    Console.WriteLine(user.DisplayName);
    Console.WriteLine(user.EmailAddress);
    Console.WriteLine(user.GivenName);
    Console.WriteLine("{0:d}", user.LastLogon);
}
```

code snippet AccountManagementSamples/Program.cs

Running the application displays information about the user:

Context Server: Magellan.cinnovation.local
Developer, Author, Trainer, Consultant
Christian Nagel
Christian@ChristianNagel.com
Christian
2009/09/25

## Create a User

You can use the UserPrincipal class to create a new user. First a PrincipalContext is required to define where the user should be created. With the PrincipalContext, you set the ContextType to an enumeration value of Domain, Machine, or ApplicationDirectory, depending on whether the directory service, the local accounts of the machine, or an application directory should be used. If the current user does not have access to add accounts to Active Directory, you can also set a user and password with the PrincipalContext that is used to access the server.

Next, you can create an instance of UserPrincipal passing the principal context, and setting all required properties. Here, the GivenName and EmailAddress properties are set. Finally, you must invoke the Save() method of the UserPrincipal to write the new user to the store:

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

code snippet AccountManagementSamples/Program.cs

## Reset a Password

To reset a password from an existing user, you can use the SetPassword() method from a UserPrincipal object:

```csharp
using (var context = new PrincipalContext(ContextType.Domain, "cninnovation"))
using (var user = UserPrincipal.FindByIdentity(context, IdentityType.Name, "Tom"))
{
    user.SetPassword("P@ssw0rd");
    user.Save();
}
```

code snippet AccountManagementSamples/Program.cs

The user running this code needs to have the privilege to reset a password. To change the password from an old one to a new one, you can use the method ChangePassword().

## Create a Group

A new group can be created in a similar way to creating a new user. Here, just the class GroupPrincipal is used instead of the class UserPrincipal. As in creating a new user, the properties are set, and the Save() method is invoked:

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

code snippet AccountManagementSamples/Program.cs

## Add a User to a Group

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

## Finding Users

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
