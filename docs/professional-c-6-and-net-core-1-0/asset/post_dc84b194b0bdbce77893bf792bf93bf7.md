
the server?

This chapter explores the features available in .NET to help you manage security, demonstrating how .NET protects you from malicious code, how to administer security policies, and how to access the security subsystem programmatically.

## Verifying User Information

Two fundamental pillars of security are authentication and authorization. *Authentication* is the process of identifying the user, and *authorization* occurs afterward to verify that the identified user is allowed to access a specific resource. This section shows how to get information about users with identities and principals.

## Working with Windows Identities

You can identify the user running the application by using an *identity*. The `WindowsIdentity` class represents a Windows user. If you don’t identify the user with a Windows account, you can use other classes that implement the interface `IIdentity`. With this interface you have access to the name of the user, information about whether the user is authenticated, and the authentication type.

A *principal* is an object that contains the identity of the user and the roles to which the user belongs. The interface `IPrincipal` defines the property `Identity`, which returns an `IIdentity` object, and the method `IsInRole` with which you can verify that the user is a member of a specific role. A *role* is a collection of users who have the same security permissions, and it is the unit of administration for users. Roles can be Windows groups or just a collection of strings that you define.

The principal classes available with .NET are `WindowsPrincipal`, `GenericPrincipal`, and `RolePrincipal`. Since .NET 4.5, these principal types derive from the base class `ClaimsPrincipal`. You can also create a custom principal class that implements the interface `IPrincipal` or derives from `ClaimsPrincipal`.

The sample code makes use of the following dependencies and namespaces:

## Dependencies

- `NETStandard.Library`
- `System.Security.Principal.Windows`

## Namespaces

- `System.Collections.Generic`
- `System.Security.Claims`
- `System.Security.Principal`
- `static System.Console`

The following example creates a Console Application (Package) that provides access to the principal in an application that, in turn, enables you to access the underlying Windows account. You need to import the System.Security.Principal and System.Security.Claims namespaces. The Main method invokes the method ShowIdentityInformation to write information about the WindowsIdentity to the console, ShowPrincipal to write additional information that is available with principals, and ShowClaims to write information about claims (code file WindowsPrincipal/Program.cs):

```
static void Main()
{
    WindowsIdentity identity = ShowIdentityInformation();
    WindowsPrincipal principal = ShowPrincipal(identity);
    ShowClaims(principal.Claims);
}
```

The method ShowIdentityInformation creates a WindowsIdentity object by invoking the static GetCurrent method of the WindowsIdentity and accesses its properties to show the identity type, name of the identity, authentication type, and other values (code file WindowsPrincipal/Program.cs):

```
public static WindowsIdentity ShowIdentityInformation()
{
    WindowsIdentity identity = WindowsIdentity.GetCurrent();
    if (identity == null)
    {
        WriteLine("not a Windows Identity");
        return null;
    }

    WriteLine($"IdentityType: {identity}");
    WriteLine($"Name: {identity.Name}");
    WriteLine($"Authenticated: {identity.IsAuthenticated}");
    WriteLine($"Authentication Type:
{identity.AuthenticationType}");
    WriteLine($"Anonymous? {identity.IsAnonymous}");
    WriteLine($"Access Token:
{identity.AccessToken.DangerousGetHandle()}");
    WriteLine();
    return identity;
}
```

All identity classes, such as WindowsIdentity, implement the IIdentity interface, which contains three properties—AuthenticationType, IsAuthenticated, and Name—for all derived identity classes to implement. The other properties you’ve seen with the WindowsIdentity are specific to this kind of identity.

When you run the application, you see information like what’s shown in the following snippet. The authentication type shows CloudAP because I’m logged into the system using a Microsoft Live account. Active Directory shows up in the authentication type if you’re using Active Directory:

```
IdentityType: System.Security.Principal.WindowsIdentity
Name: THEROCKS\Christian
```

Authenticated: True
Authentication Type: CloudAP
Anonymous? False
Access Token: 1072

## Windows Principals

A principal contains an identity and offers additional information, such as roles the user belongs to. Principals implement the interface `IPrincipal`, which offers the method `IsInRole` in addition to an `Identity` property. With Windows, all the Windows groups the user is member of are mapped to roles. The method `IsInRole` is overloaded to accept a security identifier, a role string, or an enumeration value of the `WindowsBuiltInRole` enumeration. The sample code verifies whether the user belongs to the built-in roles User and Administrator (code file `WindowsPrincipal/Program.cs`):

```
public static WindowsPrincipal ShowPrincipal(WindowsIdentity
identity)
{
    WriteLine("Show principal information");
    WindowsPrincipal principal = new WindowsPrincipal(identity);
    if (principal == null)
    {
        WriteLine("not a Windows Principal");
        return null;
    }
    WriteLine($"Users?
{principal.IsInRole(WindowsBuiltInRole.User)}");
    WriteLine(
        $"Administrators?
{principal.IsInRole(WindowsBuiltInRole.Administrator)}");
    WriteLine();
    return principal;
}
```

When I run the application, my account belongs to the role Users but not Administrator, and I get the following result:

```
Show principal information
Users? True
Administrator? False
```

It is enormously beneficial to be able to easily access details about the current users and their roles. With this information, you can make decisions about what actions should be permitted or denied. The ability to make use of roles and Windows user groups provides the added benefit that administration can be handled using standard user administration tools, and you can usually avoid altering the code when user roles change.

Since .NET 4.5, all the principal classes derive from the base class `ClaimsPrincipal`. This way, it’s possible to access claims from users with the `Claims` property of a principal object. The following section looks at claims.

## Using Claims

```
Subject: System.Security.Principal.WindowsIdentity
Issuer: AD AUTHORITY
Type:
http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid
Value type: http://www.w3.org/2001/XMLSchema#string
Value: S-1-5-114
Property:
http://schemas.microsoft.com/ws/2008/06/identity/claims/
windows subauthority NTAuthority
...
```

You can add claims to a Windows identity from a claim provider. You can also add a claim from a simple client program, such as the age claim here:

```
identity.AddClaim(new Claim("Age", "25"));
```

Using claims from a program, it’s just a matter of trust this claim. Is this claim true—the age 25? Claims can also be lies. Adding this claim from the client application, you can see that the issuer of this claim is the LOCAL AUTHORITY. Information from the AD AUTHORITY (the Active Directory) is more trustworthy, but here you need to trust the Active Directory system administrators.

The WindowsIdentity deriving from the base class ClaimsIdentity offers several methods checking for claims, or retrieving specific claims. To test whether a claim is available, you can use the HasClaim method:

```
bool hasName = identity.HasClaim(c => c.Type == 
ClaimTypes.Name);
```

To retrieve specific claims, the method FindAll needs a predicate to define a match:

```
var groupClaims = identity.FindAll(c => c.Type == 
ClaimTypes.GroupSid);
```

> NOTE A claim type can be a simple string like the "Age" type used earlier. The ClaimType defines a list of known types such as Country, Email, Name, MobilePhone, UserData, Surname, PostalCode, and several more.

> NOTE Authentication of users with ASP.NET web applications is discussed in Chapter 41, “ASP.NET MVC.”

## Encrypting Data

Confidential data should be secured so that it cannot be read by unprivileged users. This is valid for both data that is sent across the network and stored data. You can encrypt such data with symmetric or
