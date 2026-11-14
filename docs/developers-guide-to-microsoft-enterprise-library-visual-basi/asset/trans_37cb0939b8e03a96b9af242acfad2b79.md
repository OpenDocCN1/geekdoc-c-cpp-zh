

你还可以使用安全缓存的 **保存配置文件** 方法来存储用户的配置文件（例如用户的 ASP.NET 配置文件），并获取一个令牌，以便在需要时再次访问它。

## 显示用户身份详细信息

前面的代码使用一个名为 **显示用户身份详细信息** 的独立例程来完成此操作。它显示所有实现 **IIdentity** 接口的类型共有的两个属性的值，然后检查该身份是否实际是 **WindowsIdentity** 类的实例。如果是，代码将显示特定于此类型的其他属性的值。

```
Sub ShowUserIdentityDetails(ByVal identity As Object)
    Dim iid As IIdentity = TryCast(identity, IIdentity)
    Console.WriteLine("Current user {0} is authenticated.", iid.Name)
    Console.WriteLine("Authentication type: {0}", iid.AuthenticationType)

    If TypeOf identity Is WindowsIdentity Then
        Dim windidentity As WindowsIdentity = TryCast(identity, WindowsIdentity)
        Console.WriteLine("Impersonation level: {0}", _
            windidentity.ImpersonationLevel)
        Console.WriteLine("Is the Guest account: {0}", windidentity.IsGuest)
        Console.WriteLine("Is the system account: {0}", windidentity.IsSystem)
        Console.WriteLine("SID value: '{0}'", windidentity.User.Value)
        Console.WriteLine("Member of {0} groups.", _
            windidentity.Groups.Count)
    End If
End Sub
```

## 显示通用主体详细信息

你之前看到的代码使用一个名为 **显示通用主体详细信息** 的独立例程来显示通用主体的详细信息。它显示身份名称，然后调用 **IsInRole** 方法来检查该主体是否定义为名为 **SalesManagers** 和 **FieldSalesStaff** 的两个角色。

```
Sub ShowGenericPrincipalDetails(ByVal principal As IPrincipal)
    Console.WriteLine("Current user is {0}.", principal.Identity.Name)
    Console.WriteLine("IsInRole 'SalesManagers': {0}", _
        principal.IsInRole("SalesManagers"))
    Console.WriteLine("IsInRole 'FieldSalesStaff': {0}", _
        principal.IsInRole("FieldSalesStaff"))
End Sub
```

运行示例时，您将看到类似下面的输出。当然，身份详细信息会因您登录的帐户而异。但是，请注意，输出显示该主体仅是我们测试的两个角色中的一个成员。您还可以看到当我们缓存身份和主体时，安全缓存生成的令牌的值。

```
Current user identity obtained from Windows:
- Current user SOME-DOMAIN\username is authenticated.
- Authentication type: Kerberos.
- Impersonation level: None.
- Is the Guest account: False.
- Is the System account: False.
- SID value: 'S-1-5-21-xxxxxxxxxx-117669710-xxxxxxxx-1108'.
- Member of 12 account groups.
Current user identity has been cached.
The IIdentity security token is '02ac9a5-6dac-4b40-a82d-a16f3d9ddc37'.

Created a new Generic Principal for this user:
- Current user is SOME-DOMAIN\username.
- IsInRole 'SalesManagers': False.
- IsInRole 'FieldSalesStaff': True.
Current user principal has been cached.
The IPrincipal security token is 'ffcbc717-63ad-4a8b-82e2-26af54741ac1'.
```

## 使用令牌对用户进行身份验证

缓存身份并获取令牌后，您可以使用此令牌在整个应用程序中对用户进行身份验证。在代码的任何位置，您都可以使用该令牌来获取存储在缓存中的身份或主体。

示例“从缓存中检索用户的身份”展示了如何使用令牌检索缓存的身份。代码显示令牌的值，然后调用 GetIdentity 方法从缓存中检索匹配的身份。如果在缓存中找不到该身份，此方法将返回 Nothing。

```
' Check if the user has run the option that caches the identity and principal.
If IdentityToken IsNot Nothing Then

    ' Check if the user has been authenticated and the identity has been cached.
    Console.WriteLine("The IIdentity security token is {0}.", identityToken.Value)
    Dim identity As Object = seccache.GetIdentity(IdentityToken)
    If identity IsNot Nothing Then

        ' Identity was found in cache.
        Console.WriteLine("User identity has been retrieved from the cache.")
        ShowUserIdentityDetails(identity)

    Else

        ' Identity removed from cache due to time expiration, or explicitly in code.
        Console.WriteLine("Identity was not found in cache for the specified token.")
    End If
Else
    Console.WriteLine("You must obtain a token by caching the current " _
        & "identity before you can retrieve it.")
End If
```

您还可以使用安全缓存的 **获取配置文件** 方法，通过提供使用 **保存配置文件** 方法从安全缓存获得的合适令牌来检索用户的配置文件（例如用户的 ASP.NET 配置文件）。

该示例生成类似下面的输出，但实际值当然会因您的帐户身份而异。

```
The IIdentity security token is '02ac985-6dac-4b40-a82d-a16f3d9ddc37'.
User Identity has been retrieved from the cache:
- Current user SOME-DOMAIN\username is authenticated.
- Authentication type: Kerberos.
- Impersonation level: None.
- Is the Guest account: False.
- Is the System account: False.
- SID value: 'S-1-5-21-xxxxxxx-117609710-xxxxxxxx-1108'.
- Member of 12 account groups.
```

检索身份、主体或配置文件后，您可以将其值与当前用户的值进行比较，或使用它来为其他进程或系统对用户进行身份验证。

## 终止用户会话并使令牌过期

当用户退出应用程序，或当您希望使缓存的身份失效时，可以使用安全缓存的方法。如您所料，**使身份过期** 方法使与缓存身份对应的令牌过期，**使主体过期** 方法使与缓存主体对应的令牌过期，**使配置文件过期** 方法使与缓存用户配置文件对应的令牌过期。示例“使经过身份验证的用户过期”演示了如何使用这些方法使缓存的身份和缓存的主体过期，如下所示。

```
' Check if the user has run the option that caches the identity and principal.
If identityToken IsNot Nothing Then
    Console.WriteLine("The Identity security token is '{0}'.", _
        identityToken.Value)
End If

' Expire the identity token in the cache.
secCache.ExpireIdentity(identityToken)
Console.WriteLine("The identity for this token has been expired " _
    & "and removed from the cache.")
Console.WriteLine("The Principal security token is '{0}'.", _
    principalToken.Value)

' Expire the principal token in the cache.
secCache.ExpirePrincipal(principalToken)
Console.WriteLine("The principal for this token has been expired " _
    & "and removed from the cache.")
Else
    Console.WriteLine("You do not have a token that you can use to " _
        & "expire an identity.")
End If
```

运行此示例时，您将看到令牌在过期前的值，以及指示它们已从缓存中删除的消息。

```
The IIdentity security token is 'e303fd67-331a-45b8-94d4-088746e2cacd'.
The identity for this token has been expired and removed from the cache.

The IPrincipal security token is 'd6563752-78ed-489a-86fa-efd76c979a76'.
The principal for this token has been expired and removed from the cache.
```

## 检查用户是否有权执行任务

使用安全块来管理身份的主要原因之一是，它可以轻松检查用户是否有权执行指定的任务或操作。安全块包含两个授权提供程序，不过如果您愿意，可以创建自己的提供程序并将其与安全块集成。

要检查用户是否有权，请调用授权提供程序的 **授权** 方法，将用户主体和任务或操作的名称传递给它。**授权** 方法返回 True 或 False。块中包含的两个提供程序是授权规则提供程序和 AzMan 授权提供程序（有关这些提供程序的详细信息，请参见本章开头附近的“什么是授权规则提供程序？”）。本章介绍的示例包括一个使用授权规则提供程序的示例和一个使用 AzMan 授权提供程序的示例。

## 使用安全块配置的规则

如果您只需要将授权规则存储在应用程序的配置中，并由安全块完全管理，可以使用授权规则提供程序。如您在本章前面所见，您为应用程序配置了一系列授权规则。每个规则都定义一个表达式，用于指定哪些用户可以访问特定任务或执行特定操作。

示例“使用存储的规则为进程授权用户”演示了这种授权方法。在应用程序配置中，我们定义了两个规则：

- 名为 **更新销售数据** 的规则使用表达式“R:Administrators OR R:SalesManagers”。这允许 **管理员** 角色或 **SalesManagers** 角色的成员执行此任务。

- 名为 **读取销售数据** 的规则使用表达式“R:Users OR R:FieldSalesStaff OR R:SalesManagers”。这允许 **用户**、**FieldSalesStaff** 或 **SalesManagers** 角色的成员执行此任务。

