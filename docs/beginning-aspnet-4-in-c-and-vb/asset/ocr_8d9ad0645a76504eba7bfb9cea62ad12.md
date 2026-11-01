```
namespace Wrox.ProcCSharp.Security
{
class Program
{
static void Main()
{
AppDomain.CurrentDomain.SetPrincipalPolicy(
PrincipalPolicy.WindowsPrincipal);
try
{
ShowMessage();
}
catch (SecurityException exception)
{
Console.WriteLine("Security exception caught ({0})", exception.Message);
Console.WriteLine("The current principal must be in the local"
+ "Users group");
}
}

[PrincipalPermission(SecurityAction.Demand, Role = "BUILTIN\\Users")]
static void ShowMessage()
{
Console.WriteLine("The current principal is logged in locally ");
Console.WriteLine("(member of the local Users group)");
}
}
}
```

code snippet RoleBasedSecurity/Program.cs

The ShowMessage() method will throw an exception unless you execute the application in the context of a user in the Windows local Users group. For a web application, the account under which the ASP.NET code is running must be in the group, although in a “real-world” example you would certainly avoid adding this account to the administrators group!

If you run the preceding code using an account in the local Users group, the output will look like this:

```
The current principal is logged in locally
(member of the local Users group)
```

# Client Application Services

Visual Studio makes it easy to use authentication services that previously have been built for ASP.NET web applications. With this service, it is possible to use the same authentication mechanism with both Windows and web applications. This is a provider model that is primarily based on the classes Membership and Roles in the namespace System.Web.Security. With the Membership class you can validate, create, delete, and find users; change the password; and do other things related to users. With the Roles class you can add and delete roles, get the roles for a user, and change roles for a user. Where the roles and users are stored depends on the provider. The ActiveDirectoryMembershipProvider accesses users and roles in the Active Directory; the SqlMembershipProvider uses a SQL Server database. With .NET 4 these providers exist for client application services ClientFormsAuthenticationMembershipProvider and ClientWindowsAuthenticationMembershipProvider.

Next, you use client application services with Forms authentication. To do this, first you need to start an application server, and then you can use this service from Windows Forms or Windows Presentation Foundation (WPF).