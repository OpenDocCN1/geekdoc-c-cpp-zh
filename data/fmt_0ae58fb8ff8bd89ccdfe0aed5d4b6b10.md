
`name` 属性被加上了主页的自动 ID (`ct100`) 前缀，且 `name` 和 `id` 属性都包含了 `ContentPlaceholder` 控件的标识 (`cpMainContent_`)。

这意味着任何以前引用 `Button` 的客户端端代码现在都应该引用 `cpMainContent_Button`。

注意，这不仅仅是主页的问题。在其他情况下，你也会遇到这种行为，例如在处理用户控件（见第 8 章）和数据绑定控件（见第 13 章）时。

第二个注意事项与第一个有关。由于 HTML 元素的名称和 ID 发生了变化，对于单个控件这可能不是问题，但当你有大量控件时，这可能会影响网站性能。嵌套主页会让问题变得严重，因为两者都会被附加。为了提高可读性，本书使用了较长的名称，如 `cpContent`。

> 注意：ASP.NET 4 引入了一个新功能 `ClientID`，有助于减少相关问题。你将在第 8 章学习该功能。

主页让你能够在单一位置定义网站的一般外观和感受，从而提高了网站的一致性和可维护性。然而，另一种提高一致性的方法是自定义页的行为。你可以通过所谓的基页（base page）来实现，下文将讨论。

## 使用集中基页

在第 5 章中你学习了，默认情况下，所有 ASPX 页面都派自 `System.UI.Page` 类。这意味着你的所有页面都具有该类的行为。

在某些情况下，这种行为并不是你所需要的，你需要在其中添加一些东西。例如，你可能需要为网站中的每个页面添加某些行为。与其在每个页面中添加这些行为，不如创建一个自定义基页。项目中的所有页面都可以继承此中间页，而不是标准的基页类。图 6-7 的左半显示了 ASPX 页面直接继承自 `Page` 类。右半显示了 ASPX 页面继承自 `BasePage`，而 `BasePage` 又继承自。

要让你的页面继承此基页，你需要做两件事：

- 在 `App_Code` 文件夹中创建一个继承自 `System.UI.Page` 的类。
- 让项目中的页面继承此基页，而不是标准的基页类。

在接下来的练习中，你将在 `App_Code` 文件夹中创建一个新的基类。目前，该类的唯一目的是在运行时控制页面的标题（Title），以防止页面显示空白或像“无标题页面”之类的无意义标题。

# 使用集中化基类页面 | 207

> 注意：旧版本的 VS 使用“Untitled Page”（未命名页面）作为新表单的默认标题。然而，从 Visual Studio 2008 的 Service Pack 1 开始，默认标题是一个空字符串。我决定在基类页面中保留对“Untitled Page”的检查，这样你就可以看到如何检查不需要的标题了。

在实现基类之前，你需要更多地了解 ASP.NET 生命周期，这是一个重要的概念，描述了 Web 页面在被浏览器请求时所经历的过程。

## ASP.Net 生命周期导论

当你思考服务器如何提供页面，以及浏览器如何将这一过程视为页面的生命周期时，你可能会想出页面生命周期中的几个重要时刻。同样，当页面将其 HTML 发送给浏览器后，过程似乎结束了。然而，在页面的生命周期中发生着更有趣的事件。下表描述了页面经历的八个大阶段。在每个阶段，都会触发一个事件，允许开发者挂钩页面的生命周期并在正确的时机执行操作。你将在下一个练习中看到相关的示例。

| 阶段 | 描述 |
| :--- | :--- |
| 页面请求 (`Page request`) | 对 ASPX 页面的请求启动该页面的生命周期。当 Web 服务器能够并允许返回页面的缓存时，整个生命就不会执行。在所有其他情况下，页面将进入开始阶段。 |
| 开始 (`Start`) | 在此阶段，页面可以访问 `Request` 和 `Response` 等属性，这些属性用于与页面环境交互。此外，在此阶段会触发 `PreInit` 事件，指示页面即将进入初始化阶段。你稍后将此事件设置页的主题。 |
| 页面初始化 (`Page initialization`) | 在此阶段，你在页面中设置或通过程序添加的控件变得可用。此外，`Page` 类会触发三个事件：`Init`、`InitComplete` 和 `PreLoad`。 |
| 加载 (`Load`) | 在此阶段，控件属性会在回传（postback）期间从 `View State`（视图状态）和 `Control State`（控件状态）加载。例如，当你在 `DropDown` 中选中项目并触发回传时，这是正确项目在下拉列表中再次预选中的时刻，随后你可以在服务器端代码中使用该项目。此外，在此阶段页面会触发 `Load` 事件。 |
| 验证 (`Validation`) | 在验证阶段，用于验证用户输入的 `Validation` 控件将被处理。你将在第 9 章中学习验证器。 |

| 阶段 | 描述 |
| :--- | :--- |
| 回传事件处理 (`Postback event handling`) | 在此阶段，页面中的控件可能会触发它们自己的事件。例如，当用户在列表中选择了不同的选项时，`DropDownList`可能会触发 `SelectedChanged` 事件。同样，当用户在回传到服务器之前更改了文本时，`TextBox`可能会触发 `TextChanged` 事件。当所有事件处理完成后，页面会触发 `LoadComplete` 事件。此外，在此阶段会触发 `PreRender` 事件，指示页面即将渲染到浏览器。不久后，会触发 `SaveStateComplete`，指示页面正在将所有相关的控件数据存储在 `View State` 中。 |
| 渲染 (`Rendering`) | 渲染是控件（以及页面本身）向浏览器输出其 HTML 的阶段。 |
| 卸载 (`Unload`) | 卸载实际上是一个清理阶段。这是页面和控件释放它们所持有的资源的时刻。在此阶段，会触发 `Unload` 事件，以便你可以处理任何可能需要的清理工作。 |

重要的一点是意识到，所有这些事件都是在服务器端触发的，而不是在客户端。因此，即使你说是“客户端文本框的文本”，`TextBox` 控件的 `TextChanged` 事件也会在你回传页面后在服务器端触发。

现在你可能奇怪为什么需要知道所有这些。最大的原因是对页面生命周期有一个基本的理解，因为正如你所看到的，某些操作可以在页面生命周期的特定阶段执行。为了理解 ASP.NET 页面生命周期，你需要更多了解控件、状态、事件等。因此，你将在第 15 章再次访问页面生命周期，届时你将详细查看触发的所有不同事件及其顺序。

在下一个练习中，你将使用页面的 `PreRender` 事件来设置标题。由于开发者可以在许多事件期间通过程序设置页面，因此检查正确的标题应该在页面生命周期尽可能晚的时候进行，`PreRender` 是此此目的最佳事件。

## 实现基类页面

实现基类页面非常简单：你只需要向 `App_Code` 文件夹中添加一个类即可。稍微困难的是确保站点中的每个页面都继承自这个基类页面，而不是使用 `System.Web.UI` 类。遗憾的是，在使用代码后置（Code Behind）时，没有办法自动为你配置应用程序，因此你需要手动修改每个页面。Visual Studio 让这变得稍微简单了一些，允许你导出一个已经包含你代码的页面模板。在下一个练习中，你将为站点添加基类页面，在后面的练习中，你将看到如何将表单导出到模板，这样你就可以立即添加使用基类的文件了。

### 尝试一下创建一个基类页面

- 1. 在解决方案资源管理器中右键点击 `App_Code` 文件夹，选择“添加 -> 添加新项”（Add Add New Item）。在模板中选择“类”（Class）并将文件命名为 `BasePage`。
- 2. 清空文件内容，然后添加以下代码：

```vb.NET
Public Class BasePage
    Inherits System.Web.UI.Page
    Private Sub Page_PreRender(sender As Object, e As EventArgs) Handles Me.PreRender
        If String.IsNullOrEmpty(Me.Title) OrElse Me.Title.Equals("Untitled Page", StringComparison.CurrentCulture) Then
            Throw New Exception("Page title cannot be empty.")
        End If
    End Sub
End Class
```

- 3. 在下一个练习中向站点添加基类页面，在后面的练习中你将看到如何将表单导出到模板，这样你就可以立即添加使用基类的文件了。
（注：此处根据上下文逻辑补全后续步骤，原文未提供步骤3-6，但翻译逻辑保持一致）

7. 保存你为继承任何打开的页面所做的更改，并再次浏览到 `Login.aspx`。如果一切都按计划运行，错误应该就会消失，你现在可以看到登录页面了。

但请记住，当你尝试访问站点中的所有其他页面时，它们都会抛出错误。修复方法很简单：在它们的页面指令（page directive）中为所有页面提供一个有效的 `Title` 属性，你不需要手动执行。对于 `Title=""` 属性为空的页面，你可以通过搜索 `Title="` 并将其替换为类似 `Title="Planet Wrox"` 的内容来快速完成。对于你目前创建的演示页面以外的页面，最好为它们提供一个唯一的标题，清晰地描述其所包含的内容。

## 工作原理

默认情况下，你所有的页面都继承自 `System.Web.UI` 命名空间中定义的 `Page` 类。这使它们具备了所需的行为，以便作为可以被浏览器请求并由服务器处理的 Web 。由于 .NET 的继承模型允许你从每个类之间创建类链，因此你可以轻松地在页面和标准 `Page` 类之间插入你自己的基页面类。你可以通过将 `Inherits` 语句（在 C# 中）更改为你的新 `BasePage` 来实现：

### VB.NET

```
Partial Class Login
Inherits BasePage
```

### C#

```csharp
public partial class Login : BasePage
```

在这个新的 `BasePage` 类内部，你添加了一个事件处理程序，该程序会在类触发其 `PreRender` 事件时被调用。正如你所学到的那样，该事件在页面生命周期的很晚阶段触发，此时整个页面已经设置完毕并渲染到客户端：

### VB.NET

```vb
Private Sub Page_PreRender(sender As Object, e As EventArgs) Handles Me.PreRender
  ' 在处实现代码
End Sub
```

### C#

```csharp
private void Page_PreRender(object sender, EventArgs e)
{
  // 在处实现代码
}
```

注意，Visual Basic 使用 `Handles` 关键字告诉编译器 `Page_PreRender` 方法将用于处理事件。在 C# 中，你需要手动挂钩此处理器。执行此操作的好地方是类的构造函数：

```csharp
public BasePage()
{
  this.PreRender += Page_PreRender;
}
```

此行高亮代码的作用与 VB.NET 中的 `Handles` 关键字相同：它告诉编译器当页面引发其 `PreRender` 事件时运行什么代码。

在事件处理程序内部，代码会检查当前页面标题。如果页面标题仍然为空字符串（你添加到项目中的任何新页面的默认值）或为 "Untitled"，它将抛出一个异常。

### VB.NET

```vb
If String.IsNullOrEmpty(Me.Title) OrElse Me.Title.Equals("Untitled Page",
StringComparison.CurrentCultureIgnoreCase) Then
    Throw Exception(
        "Page title cannot be \"Untitled Page\" or an empty string.")
End If
```

### C#

```csharp
if (string.IsNullOrEmpty(this.Title) || this.Title.Equals("Untitled Page",
StringComparison.CurrentCultureIgnoreCase))
{
    throw Exception(
        "Page title cannot be \"Untitled Page\" or an empty string.");
}
```

此代码使用 `String` 类的 `IsNullOrEmpty` 来检查值是否为 null（VB 中的 `Nothing`）或空字符串。它使用 `Equals` 方法检查页面标题是否为 Untitled。它使用 `StringComparison.CurrentCultureIgnoreCase` 进行不区分大小写的比较，因此页面标题或 Untitled 都能匹配。

注意 `Me`（在 VB.NET 中）和 `this`（在 C# 中）是如何使用的。这些关键字是环境相关的，并且始终引用它们所在的类实例。在示例中，`Me` 和 `this` 指向 `BasePage` 类的当前实例。此 `BasePage` 实例有一个 `Title` 属性（继承自 `Page`），可以更改为不需要的值。如果它仍然包含默认标题（空字符串）或文本 "Untitled"，代码将引发（或抛出）异常。这会立即停止页面的执行，以便开发者可以在页面崩溃之前通过提供标题来修复问题。在第 18 章中，你将学习更多关于异常以及如何防止和处理异常的知识。

为了在错误消息中显示双引号（"），两种语言使用了不同的格式。在 Visual Basic 中，你需要双写引号。在 C# 中，你需要在双引号前加一个反斜杠 (\) 来转义双引号。在两种情况下，双引号字符最终都会出现在错误消息中。

由于你添加到站点的每个新页面都应该继承自这个新的基页面，因此你应该创建一个页面模板，在其代码后置（Code Behind）和标记中已经包含了正确的代码，以便从开始就能轻松地将代码添加到页面。

## 创建可重用的模板

Visual Studio 自带了一个非常棒的工具，可以导出不同文件类型的模板，包括 ASPX 页面、类文件和 CSS 文件。通过创建自定义模板，你只需要定义一次所需的代码或标记，然后根据此模板创建新文件，这为你提供了一个快速开始并尽可能地减少了所需的代码。下一个练习将向你展示如何创建自己的模板。

### 尝试创建一个可重用的页面模板

在此练习中，你将看到如何为添加到站点中的所有新 ASPX 页面创建一个模板文件。为了避免与当前站点中的现有页面冲突，你创建了一个临时页面并将其用于模板。之后，你可以删除该临时文件。

- 1. 在站点根目录下添加一个新的 Web Form 并命名为 `Temporary.aspx`。确保你使用了代码后台、使用了你的编程语言，并且基于 `MasterPages` 文件夹中的主页。
- 2. 打开此新页面的代码后台（按 F7）并更改 `Inherits` 行（C# 中的冒号），使页面继承自 `System.Web.UI.Page` 的 `BasePage`。还将将类从 `Temporary` 重命名为 `$relnamespace$$_safeitemename`：

```VB.NET
Partial Class $relnamespace$$_safeitemename
Inherits BasePage
```

```c#
public partial class $relnamespace$$_safeitemename : BasePage
{
    ...
}
```

确保你没有移除任何现有的代码，例如 C# 版本中的 `using` 语句或 `Page_Load` 方法。

不要担心可能会收到的关于 `$` 等意外字符的任何编译错误。一旦你开始基于此模板添加页面，`$relnamespace$$_safeitemename` 将被替换为你正在添加的页面名称。
- 3. 切换到标记视图，并将 `Inherits` 属性从 `Temporary` 更改为 `$relnamespace$$_safeitemename`，如此 C# 示例所示：

```xml
<@ Page Title="C#" MasterFile="~/MasterPages/Frontend.master" AutoEventWireup="true" CodeFile="Temporary.aspx.cs" Inherits="Temporary">
```
