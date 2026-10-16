
服务器呢？

本章探讨 .NET 中可用于帮助你管理安全性的功能，演示 .NET 如何保护你免受恶意代码的攻击、如何管理安全策略，以及如何以编程方式访问安全子系统。

## 验证用户信息

安全性的两大基本支柱是身份验证和授权。*身份验证*是标识用户的过程，*授权*则随后发生，用于验证被标识的用户是否被允许访问特定资源。本节将介绍如何通过标识和主体获取用户信息。

## 使用 Windows 标识

你可以使用一个*标识*来标识正在运行应用程序的用户。`WindowsIdentity` 类表示 Windows 用户。如果不用 Windows 帐户标识用户，你可以使用实现 `IIdentity` 接口的其他类。通过此接口，你可以访问用户的名称、用户是否已通过身份验证的信息以及身份验证类型。

*主体*是一个对象，包含用户标识和用户所属的角色。`IPrincipal` 接口定义了 `Identity` 属性（返回 `IIdentity` 对象）和 `IsInRole` 方法，你可以通过该方法验证用户是否是特定角色的成员。*角色*是具有相同安全权限的用户的集合，也是用户的管理单元。角色可以是 Windows 组，也可以是你定义的字符串集合。

.NET 中可用的主体类有 `WindowsPrincipal`、`GenericPrincipal` 和 `RolePrincipal`。从 .NET 4.5 开始，这些主体类型派生自基类 `ClaimsPrincipal`。你也可以创建实现 `IPrincipal` 接口或派生自 `ClaimsPrincipal` 的自定义主体类。

示例代码使用了以下依赖项和命名空间：

## 依赖项

- `NETStandard.Library`
- `System.Security.Principal.Windows`

## 命名空间

- `System.Collections.Generic`
- `System.Security.Claims`
- `System.Security.Principal`
- `static System.Console`

下面的示例创建了一个控制台应用程序（包），它可以在应用程序中提供对主体的访问，从而使你能够访问底层 Windows 帐户。你需要导入 System.Security.Principal 和 System.Security.Claims 命名空间。Main 方法调用 ShowIdentityInformation 方法向控制台写入有关 WindowsIdentity 的信息，调用 ShowPrincipal 写入主体可用的附加信息，并调用 ShowClaims 写入有关声明的信息（代码文件 WindowsPrincipal/Program.cs）：

```
static void Main()
{
    WindowsIdentity identity = ShowIdentityInformation();
    WindowsPrincipal principal = ShowPrincipal(identity);
    ShowClaims(principal.Claims);
}
```

ShowIdentityInformation 方法通过调用 WindowsIdentity 的静态 GetCurrent 方法创建 WindowsIdentity 对象，并访问其属性来显示标识类型、标识名称、身份验证类型和其他值（代码文件 WindowsPrincipal/Program.cs）：

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

所有标识类（如 WindowsIdentity）都实现 IIdentity 接口，该接口包含三个属性——AuthenticationType、IsAuthenticated 和 Name——供所有派生标识类实现。你在 WindowsIdentity 上看到的其他属性是这种标识特有的。

运行该应用程序时，你会看到如下所示的信息。身份验证类型显示为 CloudAP，因为我是使用 Microsoft Live 帐户登录系统的。如果你使用的是 Active Directory，身份验证类型中会显示 Active Directory：

```
IdentityType: System.Security.Principal.WindowsIdentity
Name: THEROCKS\Christian
```

Authenticated: True
Authentication Type: CloudAP
Anonymous? False
Access Token: 1072

## Windows 主体

主体包含一个标识，并提供其他信息，例如用户所属的角色。主体实现 `IPrincipal` 接口，该接口除了提供 `Identity` 属性外，还提供 `IsInRole` 方法。在 Windows 中，用户所属的所有 Windows 组都会被映射到角色。`IsInRole` 方法被重载，可以接受安全标识符、角色字符串或 `WindowsBuiltInRole` 枚举的枚举值。示例代码验证用户是否属于内置角色 User 和 Administrator（代码文件 `WindowsPrincipal/Program.cs`）：

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

当我运行该应用程序时，我的帐户属于 Users 角色，但不属于 Administrator，得到以下结果：

```
Show principal information
Users? True
Administrator? False
```

能够轻松访问当前用户及其角色的详细信息，会带来巨大的好处。借助这些信息，你可以决定应允许或拒绝哪些操作。能够利用角色和 Windows 用户组还有一个额外好处：可以使用标准的用户管理工具进行管理，而且当用户角色变化时，通常无需更改代码。

从 .NET 4.5 开始，所有主体类都派生自基类 `ClaimsPrincipal`。这样，就可以通过主体对象的 `Claims` 属性访问用户的声明。下一节将介绍声明。

## 使用声明

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

你可以从声明提供程序向 Windows 标识添加声明。你也可以从简单的客户端程序添加声明，例如下面的年龄声明：

```
identity.AddClaim(new Claim("Age", "25"));
```

当声明来自程序时，事情就只是是否信任该声明的问题。这个声明是真的吗——年龄 25 岁？声明也可能是谎言。从客户端应用程序添加此声明时，你会看到此声明的颁发者是 LOCAL AUTHORITY。来自 AD AUTHORITY（Active Directory）的信息更值得信任，但在这里你需要信任 Active Directory 系统管理员。

从基类 ClaimsIdentity 派生的 WindowsIdentity 提供了几种方法来检查声明或检索特定声明。若要测试某个声明是否可用，你可以使用 HasClaim 方法：

```
bool hasName = identity.HasClaim(c => c.Type == 
ClaimTypes.Name);
```

若要检索特定声明，FindAll 方法需要一个谓词来定义匹配条件：

```
var groupClaims = identity.FindAll(c => c.Type == 
ClaimTypes.GroupSid);
```

> 注意：声明类型可以是简单的字符串，比如之前使用的 "Age" 类型。ClaimType 定义了一组已知类型，如 Country、Email、Name、MobilePhone、UserData、Surname、PostalCode 等。

> 注意：使用 ASP.NET Web 应用程序对用户进行身份验证的内容将在第41章“ASP.NET MVC”中讨论。

## 加密数据

机密数据应受到保护，以防被无权限用户读取。这既适用于通过网络发送的数据，也适用于存储的数据。你可以使用对称加密或
