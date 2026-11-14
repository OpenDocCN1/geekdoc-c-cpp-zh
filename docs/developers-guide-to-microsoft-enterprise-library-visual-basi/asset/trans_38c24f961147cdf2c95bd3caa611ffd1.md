

示例代码首先显示存储在应用程序级变量中的当前主体令牌的值（在运行此示例之前，您必须先执行第一个示例来对自己进行身份验证并获取令牌）。然后它使用此令牌从安全缓存中检索主体，并调用名为 **AuthorizeUserWithRules** 的单独例程来执行授权。

**AuthorizeUserWithRules** 例程将实现 **IPrincipal** 接口的泛型主体作为参数，以及要使用的授权提供程序的引用。在此示例中，这是从 Enterprise Library 容器中解析并在示例应用程序启动时存储在名为 `ruleAuth` 的变量中的 Security 块授权规则提供程序。我们在本章前面的“深入示例”部分中展示了如何获取两种授权提供程序的实例。

```
' Check if the user has run the operation that caches the identity and principal.
If principalToken IsNot Nothing Then
    ' First try authorizing tasks using the cached Generic Principal.
    Console.WriteLine("The IPrincipal security token is '{0}'". _
        principalToken.Value)
    ' Retrieve the user principal from the security cache using the token.
    Dim principal As IPrincipal = secCache.GetPrincipal(principalToken)
    If principal IsNot Nothing Then
        ' Check if this user is authorized for tasks using the Rule Provider.
        AuthorizeUserWithRules(principal, ruleAuth)
    Else
        ' Identity removed from cache due to time expiration, or explicitly in code.
        Console.WriteLine("Principal not found in cache for the specified token.")
    End If
Else
    Console.WriteLine("You must obtain a token by caching the current identity " _
        & "before you can use it to check authorization rules.")
End If
```

以下代码显示了我们在前一个示例中使用的 **AuthorizeUserWithRules** 例程。它只是调用授权提供程序的 **Authorize** 方法——一次针对 **UpdateSalesData** 任务，一次针对 **ReadSalesData** 任务——并显示结果。

```
Sub AuthorizeUserWithRules(ByVal principal As IPrincipal, _
    ByVal authProvider As IAuthorizationProvider)
    ' Determine whether user is authorized for rule defined as "UpdateSalesData".
    Dim canUpdateSalesData As Boolean _
        = authProvider.Authorize("UpdateSalesData")
    Console.WriteLine("User can execute 'UpdateSalesData' task: {0}", _
        canUpdateSalesData)

    ' Determine whether user is authorized for rule defined as "ReadSalesData".
    Dim canReadSalesData As Boolean _
        = authProvider.Authorize("ReadSalesData")
    Console.WriteLine("User can execute 'ReadSalesData' task: {0}", _
        canReadSalesData)
End Sub
```

运行此示例时，您将看到类似于以下内容的输出。本章第一个示例中的代码（用于对用户进行授权并缓存身份和主体）将其生成的主体定义为仅属于 FieldSalesStaff 角色的成员，因此用户仅获授权执行 ReadSalesData 任务。

```
The IPrincipal security token is '77a9c8Af-9691-4ae4-ab5-0e96d4c4610e'.
User can execute 'UpdateSalesData' task: False
User can execute 'ReadSalesData' task: True
```

## 使用 AzMan 提供程序规则

第二个授权示例“使用 AzMan 规则为进程授权用户”使用 Windows 授权管理器 (AzMan) 提供程序。在示例中，我们为前一个示例中看到的相同两个任务定义了规则：UpdateSalesData 和 ReadSalesData。但是，AzMan 依赖于能够使用安全标识符 (SID) 访问 Windows 帐户详细信息，因此我们随示例提供的名为 Example.xml 的文件中的角色可能无法在您的计算机上对您进行身份验证。只有在使用本地计算机帐户或当前域登录帐户可以访问 Active Directory® 存储以获取信息时，它才能工作。您应该在 AzMan（Microsoft Management Console (MMC) 的一个 snap-in）中打开 Example.xml 文件，并编辑其中包含的规则以指定您自己的本地或域帐户，以便试验 AzMan 授权。

示例代码与您在前一个示例中使用 Security 块授权规则提供程序时看到的代码类似。它使用存储在应用程序级变量中的令牌从安全缓存中获取当前用户主体，并调用与前一个示例相同的 AuthorizeUserWithRules 方法来检查该主体是否获授权执行 UpdateSalesData 和 ReadSalesData 任务。然后，此示例为当前用户生成一个 WindowsPrincipal，并检查其是否获授权执行 UpdateSalesData 和 ReadSalesData 任务。

此示例代码的主要区别在于，它将程序启动时创建的 AzMan 授权提供程序的引用传递给 AuthorizeUserWithRules 例程，如下所示。

```
' First try authorizing tasks using the cached Generic Principal.
Dim genPrincipal As IPrincipal = secCache.GetPrincipal(principalToken)
If genPrincipal IsNot Nothing Then
    ' Check if this user is authorized for tasks using the AzMan provider.
    AuthorizeUserWithRules(genPrincipal, azmanAuth)
End If
...
```

```
' Now try checking for authorization for tasks using the cached WindowsIdentity
Dim identity As IIdentity = secCache.GetIdentity(identityToken)
If identity IsNot Nothing Then
    ' Generate a WindowsPrincipal from the IIdentity.
    Dim winPrincipal As IPrincipal = New WindowsPrincipal(TryCast(identity, _
    WindowsIdentity))
    ' Check if this user is authorized for tasks using the AzMan provider.
    ' Note: this will only work if you are using a local machine account or your
    ' current domain account can access directory store to obtain information.
    AuthorizeUserWithRules(winPrincipal, azmanAuth)
End If
...
```

运行此示例后，在配置 AzMan 规则以适应您自己的计算机和帐户后，您应该能够看到类似于此处所示的结果。

```
The IPrincipal security token is '77a9Cbaf-9691-4e4b-ab5b-0e964dc461e0'.
User can execute 'UpdateSalesData' task: False
User can execute 'ReadSalesData' task: True
The IIdentity security token is 'b6eb4af7-b958-4cc2-b2b9-112cd58c566d'.
User can execute 'UpdateSalesData' task: False
User can execute 'ReadSalesData' task: True
```

## 创建自定义授权提供程序

尽管 Security 应用程序块仅包含两个授权提供程序和两个缓存提供程序，但如果没有一个完全适合您自己的场景，您可以轻松扩展它以添加新提供程序。该块包含一个名为 AuthorizationProvider 的基类，您可以从中继承并扩展以执行自定义授权。您只需实现 Authorize 方法，然后将新提供程序与 Enterprise Library 集成即可。您还可以实现自定义缓存管理器和缓存后端存储，并将这些与 Caching 应用程序块集成，以提供凭据的自定义缓存机制，并为 Cryptography 应用程序块实现自定义加密提供程序，然后可使用它来加密缓存的凭据。有关创建自定义提供程序、缓存管理器和后端存储的更多信息，请参阅在线文档以及随 Enterprise Library 安装并在线提供的帮助文件，网址为 http://go.microsoft.com/fwlink/?LinkId=188874。

## 摘要

本章描述了如何使用 Security 应用程序块来简化常见任务，例如缓存经过身份验证的用户凭据以及检查用户是否获授权执行特定任务。虽然不使用 Security 块来实现这些任务所需的代码并不过分繁琐，但该块确实省去了您在多个位置编写和测试相同代码的工作。它还允许您根据要求使用各种不同的缓存和授权提供程序，并通过配置更改提供程序。管理员和操作员在将应用程序部署到不同环境时会发现此功能很有用。

本章描述了使用 Security 块的场景，并解释了授权用户和缓存凭据的概念。然后，它介绍了如何在示例应用程序中使用该块的功能的详细示例。有关特定任务（例如配置和部署）的更多详细信息，请参阅在线文档以及随 Enterprise Library 安装的帮助文件。

