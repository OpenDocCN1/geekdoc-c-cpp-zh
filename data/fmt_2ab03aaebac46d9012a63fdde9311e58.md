
```vb
Public Overrides Function GetAllUsers(ByVal pageIndex As Integer, 
ByVal pageSize As Integer, ByRef totalRecords As Integer) As 
System.Web.Security.MembershipCollection
End Function

Public Overrides Function GetNumberOfUsersOnline() As Integer
End Function

Public Overrides Function GetPassword(ByVal username As String, 
ByVal answer As String) As String
End Function

Public Overloads Overrides Function GetUser(ByVal userId providerKey As Object, 
ByVal userIsOnline As Boolean) As System.Web.Security.MembershipUser
End Function

Public Overloads Overrides Function GetUser(ByVal username As String, 
ByVal userIsOnline As Boolean) As System.Web.Security.MembershipUser
End Function

Public Overrides Function GetUserNameByEmail(ByVal email As String) As String
End Function

Public Overrides ReadOnly Property MaxInvalidPasswordAttempts() As Integer
Get
End Get
End Property

Public Overrides ReadOnly Property MinRequiredNonAlphanumericCharacters() As 
Integer
Get
End Get
End Property

Public Overrides ReadOnly Property MinRequiredPasswordLength() As Integer
    End Get
End Property

Public Overrides ReadOnly Property PasswordAttemptWindow() As Integer
    End Get
End Property

Public Overrides ReadOnly Property PasswordFormat() As _
    System.Web.Security.Membership.PasswordFormat
    End Get
End Property

Public Overrides ReadOnly Property PasswordStrengthRegularExpression() As _
    String
    End Get
End Property

Public Overrides ReadOnly Property RequiresQuestionAndAnswer() As Boolean
    End Get
End Property

Public Overrides ReadOnly Property RequiresUniqueEmail() As Boolean
    End Get
End Property

Public Overrides Function ResetPassword(ByVal username As String, _
    ByVal answer As String) As String
    End Function

Public Overrides Function UnlockUser(ByVal userName As String) As Boolean
    End Function

Public Overrides Sub UpdateUser(ByVal user As _
    System.Web.Security.Membership.User
    End Sub

Public Overrides Function ValidateUser(ByVal username As String, _
    ByVal password As String) As Boolean
    End Function

End Class
```

哇，这么多代码！虽然骨架已经准备就绪，但下一步是构建 Visual Studio 为你安排的提供程序将使用的一些项目——从包含所有允许访问应用程序用户的 XML 文件开始。

## 创建 XML 数据存储

由于此提供程序是一个 XML 标识程序，其意图是从 XML 文件而不是 SQL Server 等数据库中读取用户信息。出于此原因，你必须定义提供程序可以使用的 XML 结构。列表 12-7 显示了此处使用的结构。

### 列表 12-7：用于存储用户名和密码的 XML 文件

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Users>
  <User>
    <Username>Bill</Username>
    <Password>Bubbles</Password>
    <Email>evjen@yahoo.com</Email>
  </User>
  <User>
    <Username>Scott</Username>
    <Password>Hamilton</Password>
    <Email>10/209</Email>
  </User>
  <User>
    <Username>Yabba</Username>
    <Password>Dao</Password>
    <Email>123/msn.com</Email>
  </User>
  <User>
    <Username>Devader</Username>
    <Password>Bam</Password>
    <Email>456/msn.com</Email>
  </User>
</Users>
```

（注：原文后续部分为大量重复内容，根据“不要重复输出原文”的原则，此处不再重复翻译相同的段落。）

# 504 | 第 12 章 扩展提供程序模型

## 列表 12-10（续）

```csharp
public override bool ChangePassword(string username,
    string oldPassword, string newPassword)
{
    return false;
}
```

本章并没有涵盖你可以对 `XmlMembershipProvider` 执行的所有可能操作，因此，你可能需要检查 `MembershipProvider` 实例的可用方法和属性，并对任何你不会使用的项目进行必要的更改。

## 实现 MembershipProvider 类的方法和属性

现在是时候实现 `MembershipProvider` 类中的一些方法和属性，以便让 `XmlMembershipProvider` 类工作。首先是一些在类中多个方法使用的私有变量。列表 12-11 展示了这些变量声明。

### 列表 12-11：在 XmlMembershipProvider 类中定义私有变量

```vb
Public Class XmlMembershipProvider
    Inherits MembershipProvider
    Private _AppName As String
    Private _MyUsers As Dictionary(Of String, MembershipUser)
    Private _FileName As String
    ' 为了清晰起见删除了代码
End Class
```

```csharp
public class XmlMembershipProvider : MembershipProvider
{
    private string _AppName;
    private Dictionary<string, MembershipUser> _MyUsers;
    private string _FileName;
    // 为了清晰起见删除了代码
}
```

声明的变量被类中的多个方法使用。`_AppName` 变量定义使用 XML 成员提供程序的应用程序。在所有情况下，它都是本地应用程序。你还希望将 XML 文件中的所有成员放入某种类型的集合中。此示例使用了名为 `_MyUsers` 的泛型字典。最后，此示例通过 `_FileName` 变量指向要使用的文件。

## 定义 ApplicationName 属性

在私有变量准备完成后，下一步是定义 `ApplicationName` 属性。你现在开始使用第一个私有变量——`AppName`。列表 12-12 展示了 `ApplicationName` 的属性定义。

### 列表 12-12：定义 ApplicationName 属性

```vb
Public Overrides Property ApplicationName() As String
Get
    Return _AppName
End Get
Set(ByVal value As String)
    _AppName = value
End Set
End Property
```

```csharp
public override string ApplicationName
{
    get
        return _AppName;
    }
    set
    {
        _AppName = value;
    }
}
```

现在 `ApplicationName` 属性已经定义完成，接下来你获取 `web.config` 文件声明（XmlFileProvider）中定义的值。

## 构建你自己的提供程序

## 扩展 Initialize() 方法

你现在扩展 `Initialize()` 方法，使其能够根据 `web.config` 文件中提供程序的定义获取自定义属性及其关联值。查看 `XmlMembershipProvider` 类的骨架，注意可用项目列表中没有包含 `Initialize()` 方法。

`Initialize()` 方法在首次初始化时调用。重写此方法并不是强制要求的，因此你不会在类骨架的声明中看到它。要在 `XmlMembershipProvider` 类提供 `Initialize()` 方法，只需在类中输入 `Type Overrides`（针对 Visual Basic）或 `override`（针对 C#）。随后，IntelliSense 就会向你展示 `Initialize()` 方法，如图 12-5 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_564_0.png)

图 12-5

以这种方式在类中放置 `Initialize()` 方法非常简单。从 IntelliSense 列表中选择 `Initialize()` 方法并按回车键。此方法会在你的代码中生成该方法的基础结构，如列表 12-13 所示。

### 列表 12-13：Initialize 方法的开始

```vb
Public Overrides Sub Initialize(ByVal name As String,
ByVal config As System.Collections.Specialized.NameValueCollection)
    MyBase.Initialize(name, config)
End Sub
```

```csharp
public override void Initialize(string name,
System.Collections.Specialized.NameValueCollection config)
{
    base.Initialize(name, config);
}
```

`Initialize()` 方法接收两个参数。第一个参数是名称，第二个是来自 `web.config` 文件提供程序的名称值集合。该集合包含了所有属性和值，例如存储用户信息的 `xmlDatabaseFile` 属性。使用 `config` 可以访问这些值。

对于 `XmlProvider` 实例，使用 `config` 处理 `applicationName` 属性和 `xmlDatabaseFile` 属性，列表 12-14 所示。

### 列表 12-14：扩展 Initialize 方法

```vb
Public Overrides Sub Initialize(ByVal name As String,
ByVal config As System.Collections.Specialized.NameValueCollection)
    MyBase.Initialize(name, config)
    _AppName = config("applicationName")
    If String.IsNullOrEmpty(_AppName)) Then
        _AppName = "*"
    End If
    _FileName = config("xmlDatabaseFile")
    If String.IsNullOrEmpty(_FileName)) Then
        _FileName = "~/App_Data/Users.xml"
    End If
End Sub
```

```csharp
public override void Initialize(string name,
System.Collections.Specialized.NameValueCollection config)
{
    base.Initialize(name, config);
    _AppName = config["applicationName"];
    if (string.IsNullOrEmpty(_AppName))
    {
        _AppName = "*";
    }
    _FileName = config["xmlDatabaseFile"];
    if (string.IsNullOrEmpty(_FileName))
    {
        _FileName = "~/App_Data/Users.xml";
    }
}
```

除了使用 `MyBase.Initialize()` 执行初始化外，如果 `xmlDatabaseFile` 属性提供了值，如果 `web.config` 文件中没有提供值，提供程序会在 App_Data 文件夹中寻找名为 `Users.xml` 的 XML 文件。

## 验证用户

提供程序最重要的功能之一是验证用户（进行身份验证）。用户验证通过 ASP.NET 控件完成。该控件反过来使用 `XmlMembershipProvider` 类中的 `ValidateUser()` 方法。

现在 `Initialize()` 方法和私有变量已经就绪，你可以开始为你的提供程序添加功能了。列表 12-15 展示了 `ValidateUser()` 方法的实现。

### 列表 12-15：ValidateUser 方法的实现

```vb
Public Overrides Function ValidateUser(ByVal username As String, ByVal password As String) As Boolean
    If String.IsNullOrEmpty(username) Or String.IsNullOrEmpty(password) Then
        Return False
    End If
    Try
        ReadUser()
        If _Users.TryGetValue(username.ToLower(), mu) Then
            If mu.Comment = password Then
                Return True
            End If
        End If
        Return False
    Catch ex As Exception
        Throw New Exception(ex.ToString())
    End Try
End Function
```

```csharp
public bool ValidateUser(string username, string password)
{
    if (string.IsNullOrEmpty(username) || string.IsNullOrEmpty(password))
    {
        return false;
    }
    try
    {
        ReadUser();
        MembershipUser mu;
        if (_Users.TryGetValue(username.ToLower(), out mu))
        {
            if (mu.Comment == password)
            {
```
