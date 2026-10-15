

> 一个强名称是程序的名称、其版本号以及与其关联的加密密钥和数字签名文件的组合。

身份权限是由运行时根据从受信任的主机或操作系统的加载器接收到的信息授予的。因此，它们是你没有明确请求的权限。身份权限为运行时提供额外的信息。身份信息可以采用受信任主机的 URL 形式，也可以通过数字签名、应用程序目录或程序集的强名称提供。身份权限与前一节讨论的代码访问权限类似。它们源自代码访问权限相同的基类。

## 基于角色的权限

基于角色的权限是根据用户以及代码被调用的角色授予的权限。用户在操作系统平台内进行身份验证，并持有与安全上下文关联的安全标识符（SID）。SID 与在安全上下文中建立的一个或多个角色或组成员身份相关联。.NET 支持在安全上下文中关联的用户和角色，并通过主体（principal）的概念支持通用和自定义用户和角色。

主体是一个保存当前调用者凭据的对象。这包括用户的身份。主体分为两种类型：Windows 主体和非 Windows 主体。基于 Windows 的主体对象是存储有关调用模块的当前用户上下文的 Windows SID 信息的对象，用于正在使用的基于角色的权限。非 Windows 主体是通过自定义登录方法以编程方式创建的主体对象，并可供当前线程使用。

基于角色的权限不是针对环境中的对象设置的，如代码访问权限。它们是在当前用户及其角色的上下文中检查的。主体和 PrincipalPermission 类的概念用于建立和检查权限。如果程序员在调用时传递从自定义登录捕获的用户和角色信息，则 PrincipalPermission 类也可以用于验证此信息。

PrincipalPermission 类不会授予对对象的访问权限，但它具有确定调用者是否根据当前权限对象通过 Demand 方法获得权限的方法。如果生成安全异常，则用户没有足够的权限。作为如何使用这些方法的示例，以下代码片段捕获当前 Windows 主体信息并将其显示在屏幕上的文本框中。它是 ProVB_Security 项目的一部分，该项目的结构与第 1 章中介绍的 ProVB_VS2010 项目基本相同。主体信息的每个元素都可以在程序中用于验证，并因此根据主体信息中的值限制代码执行。此示例在 Form1.vb 的顶部插入了一行 `Imports System.Security.Principal`，以便您可以直接引用身份和主体对象，而无需完整的命名空间限定符：

```
Imports System.Security.Principal

'<PrincipalPermissionAttribute(SecurityAction.Demand, Name:="WSheldon", Role:="Users")> _
Private Sub DisplayPrincipalIdentity()
' The attribute above can be used to check security declaratively
' similar to how you would check using WPF or Silverlight.
' The code below uses imperative commands to get security information.
Dim objIdentity As WindowsIdentity = WindowsIdentity.GetCurrent()
TextBox1.Text = "User Name: " & objIdentity.Name & Environment.NewLine
TextBox1.Text &= "Is Guest: " & objIdentity.IsGuest.ToString()
& Environment.NewLine
```

```
TextBox1.Text &= "Is Authenticated: " & objIdentity.IsAuthenticated.ToString()
    & Environment.NewLine
Dim objPrincipal As New Security.Principal.WindowsPrincipal(objIdentity)
' Determine if the user is part of an authorized group.
TextBox1.Text &= "Is in Role Users? " & objPrincipal.IsInRole("Users")
    & Environment.NewLine
TextBox1.Text &= "Is in Role Administrators? "
    & objPrincipal.IsInRole("Administrators")
End Sub
```

来自 Form1.vb 的代码片段

此代码说明了当调用者想要运行你的代码时可以用于验证的几个属性。此处属性在顶部被注释掉是出于设计考虑。它代表了一种声明式安全检查，与你在 WPF 或 Silverlight 项目中使用 XAML 时使用的检查类似。首先，让我们检查此代码的运行情况，如图 32-1 所示。

它首先检索当前经过身份验证的 Windows 主体的用户名。请注意，这是一个包含机器名的完全限定用户名。然后它使用身份检查来查看当前身份是否为访客账户，并确保用户已通过身份验证。

此时，片段基于当前用户的身份创建了一个新的 WindowsPrincipal。此对象允许你查询当前用户是否在某个角色中。在这种情况下，我的账户作为 Users 安全组的成员处于用户角色，但即使它属于 Administrators 组，也不在管理员角色中。

![](img/d99870e80390742f93963da7be0b2e61_1027_0.png)

图 32-1

角色通常通过安全组定义，但我特意没有说这种方法允许你确定用户是否在给定组中。那是因为在 Windows Vista 和 Windows 7 下，即使用户属于 Administrators 组，操作系统也会阻止用户以管理员角色运行。因此，对代码是否以 Administrators 角色运行的检查返回 false——即使我的 WSheldon 账户实际上是这台机器上 Administrators 组的成员。只有当用户选择提升其权限时，此查询才会返回 true。

> 关于权限提升与用户账户控制（UAC）相关的问题，以及 WSheldon 账户实际上是系统管理员的问题，将在本章后面讨论。

然而，现在取消注释该方法前面的属性行。请注意，它正在进行 Demand 安全查询并传递用户名和角色名作为其一部分。因为这些是命名可选参数，代码理论上可以只检查角色，这在实际应用中更实用。然而，在这种情况下仅使用名称，并且不要将机器作为完整用户名的部分包含在内。因此，当单击 ButtonTest 时，此声明式检查失败，并显示图 32-2 中所示的错误。

![](img/d99870e80390742f93963da7be0b2e61_1028_0.png)

# 图 32-2

这说明了自 .NET 早期版本以来一直可用的相同对象仍在使用 XAML 中，以为声明式应用程序提供相同级别的安全性。主体和身份对象用于验证尝试执行你的代码的调用者的身份或身份的某些方面。基于此信息，你的应用程序可以锁定系统资源或调整自定义应用程序中用户可用的选项。Identity 和 Principal 对象使你的应用程序能够响应 Active Directory 中用户角色的变化。

## 管理代码访问权限集

本节介绍对权限的编程访问。此示例扩展了前面讨论的 ProVB_Security 项目。此示例说明了当方法失败时，会生成包含结果的异常对象。请注意，在实际示例中，你将为调用应用程序设置权限。在许多情况下，你不希望调用应用程序能够访问注册表，或者你希望调用应用程序能够读取内存变量但不能更改它们。请记住，你只能限制用户基于其身份已有的权限。你不能通过代码授予用户基于其身份无法访问的操作系统部分的访问权限。

示例首先设置所需的权限，然后授予代码适当的访问级别。然后访问此安全对象的代码说明了这些新权限对代码的影响：

```
Private Sub TestFileIOPermission()
    Dim oFp = New FileIOPermission(
```

