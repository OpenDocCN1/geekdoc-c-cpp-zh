
你可以在 `<properties>` 标签内拥有多个组，但组只能有一层。这意味着你不能将一个 `<group>` 元素嵌套在另一个 `<group>` 或 `<add>` 元素中。

## 使用非标准数据类型

除了之前列出的 String、DateTime 和 Int32 数据类型外，你还可以使用自己的类型（例如定义在 App_Code 文件夹中的类型）。

与内置的 .NET 类型一样，你需要使用其完全限定的名称来引用你的类型，该名称包含了命名空间和类名。假设你有一个名为 `Preference` 的类型，它包含与用户偏好相关的各种属性（在本示例中实现为自动属性）。要将其包含在配置文件中，你需要首先将其封装在一个命名空间中：

```VB.NET
Namespace PlanetWrox
  Public Class Preference
    Public Property FavoriteColor As String
    ' 其他属性放在这里
  End Class
End Namespace
```

```C#
namespace PlanetWrox
{
  public class Preference
  {
    public string FavoriteColor { get; set; }
    // 其他属性放在这里
  }
}
```

然后，按照如下方式在 `<add />` 元素中引用该类型：

```xml
<add name="Preferences" type="PlanetWrox.Preference" />
```

在设置配置文件时，你可能需要引用类型的情况是使用泛型。第 5 章讨论了如何使用字符串列表（List of strings）引用角色名称。这里快速回顾你在该章节看到的代码：

```VB.NET
Dim roles As New List (Of String)
...
roles.Add("Members")
```

```C#
List<string> roles = new List<string>();
roles.Add("Members");
```

要为你的配置文件提供一个泛型列表类型的属性，你需要使用一些特殊语法。Web.config 中的以下设置将创建一个名为 `FavoriteGenres` 的属性，它在 VB.NET 中以 `List (Of Integer)` 存储用户喜欢的类型，在 C# 中存储为 `List<int>`：

```xml
<add name="FavoriteGenres" type="System.Collections.Generic.List`1[System.Int32]" />
```

type 属性的第一部分看起来很正常。`List` 类位于 `System.Collections.Generic` 命名空间中，因此在这里也需要指定它是合理的。然而，在类名（List）之后你看到了一个 `1`。这并不是一个类型，而是 .NET 使用反引号（`）来引用泛型类型，为了基于泛型类型定义它，你需要使用反引号（`）并后跟一个 `1`。反引号通常位于键盘上 `1` 键的左侧。`1` 之后跟着一对方括号，其中包含你想为列表使用的实际类型。`FavoriteGenres` 配置文件属性中指定的类型会将这些映射到 VB.NET 和 C# 的对应项：

```VB.NET
Dim FavoriteGenres As New List(Of Integer)
```

```C#
List<int> FavoriteGenres = new List<int>();
```

你将在练习中学习如何使用此属性和其他配置文件属性。首先，你将在下一次“尝试一下”中学习如何在 web.config 中配置配置文件。随后的练习将展示如何处理这些属性，以及如何使用 `List` 类的各种方法。

## 尝试一下

在本次尝试中，你将看到如何创建一个能够存储用户名、姓、出生日期、短传以及用户喜欢的类型 ID 列表的配置文件。该列表稍后用于显示与用户兴趣匹配的结果。

1. 从网站根目录打开 `web.config` 文件，并找到上一章通过 NuGet 添加的 `<profile>` 元素。如果你还没有这个元素，请参考第 16 章中的“介绍登录控件”部分来学习如何配置你的网站。
2. 作为 `<profile>` 的直接子元素添加新的 `<properties>` 元素。确保不要不小心将该元素添加到 `<providers>` 元素内部。
3. 完成 `<profile>` 元素，使其看起来如下所示：

```xml
<profile defaultProvider="DefaultProvider">
  <properties>
    <add name="FirstName" />
    <add name="LastName" />
    <add name="DateOfBirth" type="System.DateTime" />
    <add name="Bio" />
    <add name="FavoriteGenres" type="System.Collections.Generic.List`1[System.Int32]" />
  </properties>
  <providers>
    ...
  </providers>
</profile>
```

保存 Web.config。一旦保存了文件，后台进程就会开始生成一个用于配置文件的类文件。在类文件创建并成功编译后，你可以通过 Page 类的 `Profile` 属性以编程访问它。

要测试配置文件，打开你在之前的设计视图中创建的 `MyProfile.aspx` 文件。双击页面以为 `Load` 事件设置事件处理程序，并添加包含你自己的名和姓的代码：

![](img/9e033e3b9560597824f8b22941d6d8bb_672_0.png)

图 17-1

## VB.NET

```VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles My.Load
    Profile.FirstName = "YourFirstName"
    Profile.LastName = "YourLastName"
End Sub
```

## C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    Profile.FirstName = "YourFirstName";
    Profile.LastName = "YourLastName";
}
```

当你输入 `Profile.` 时，IntelliSense 会显示可用属性。如果它们没有出现，按 Ctrl+B 生成解决方案。几秒钟后，它们应该就会出现。

