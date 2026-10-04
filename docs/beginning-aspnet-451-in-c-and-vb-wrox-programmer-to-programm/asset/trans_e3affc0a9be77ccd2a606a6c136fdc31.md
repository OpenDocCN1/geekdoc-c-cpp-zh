

# 在 Ajax 网站中使用 Web 服务

（服务遇到错误或不可用）。最后一个参数称为 `useContext`，它允许你向回调方法传递额外数据。如果你需要额外的上下文数据来正确处理成功回调，这非常有用。在本示例中，第一个参数是必选的，其他三个是可选的。然而，在现实场景中，你至少需要实现 `onSuccess` 回调，以便处理从服务返回的数据。

在这个示例中，成功回调 `HelloWorldCallback` 中的代码非常简单；它所做的只是弹出（alert）从服务返回的值。然而，它并不非如此简单。你可以从服务返回的值不仅限于简单的字符串，正如接下来的章节所示。

# 与 WCF 交换对象

虽然简单的字符串作为服务的响应可能足够了，但你通常需要更多信息。例如，当用户点击刷新按钮时，你可能想从服务加载最后两条评论。与其提交整个页面，你可以调用服务，从数据库中检索评论，然后以某种方式将它们显示在页面上。以下是一个获取评论的服务示例：

```
VB.NET
<ServiceContract(Namespace="")
[AspNetCoreCompatibilityRequirements(RequirementMode=AspNetCoreCompatibilityRequirementsMode.Allowed)]
Public Class ReviewsService

    <OperationContract>
    Public Function GetLatestReviews() As List(Of Review)
        Dim temp As List(Of Review) From
        {
            New Review() With {.Id = 1,
            .Title = "21st Century Breakdown by Green Day"},
            New Review() With {.Id = 2,
            .Title = "Sonic Youth: Daydream Nation live in Roundhouse, London"}
        }
        Return temp
    End Function
End Class

Public Class Review
    Public Property Id As Integer
    Public Property Title As String
End Class
```

```csharp
[ServiceContract(Namespace = "")
[AspNetCoreCompatibilityRequirements(RequirementMode=AspNetCoreCompatibilityRequirementsMode.Allowed)]
public class ReviewsService
{
    [OperationContract]
    public List<Review> GetLatestReviews()
    {
        List<Review> temp = new List<Review>()
        {
          new Review() {Id = 1,
            Title = "21st Century Breakdown by Green Day"},
          new Review() {Id = 2,
            Title = "Sonic Youth: Daydream Nation live in Roundhouse, London"}
        };
        return temp;
    }
}

public class Review {
  public int Id { get; set; }
  public string Title { get; set; }
}
```

为了向你展示如何在客户端处理复杂数据，此代码示例返回了两个硬编码的 `Review` 实例。在后的章节中，你将看到如何处理数据库中的评论，从而使此示例真正具有动态性。目前，它的作用是在客户端显示评论。

该代码设置了一个 `Review` 实例的通用集合。目前，`Review` 是一个具有两个属性的简单类：`id` 和 `Title`。该集合使用集合初始化器填充，添加 `Review` 实例，每个实例都是使用对象初始化器创建的。有关集合和对象初始化器的更多信息，请参阅第5章。

当你从客户端代码调用 `GetLatestReviews` 方法时，你会得到一个可以遍历的实例集合。下面的代码显示了实现此功能的 `getReviewsCallback` 方法：

```javascript
function getLatestReviewsCallback(result) {
  var listItems = '';
  for (var i = 0; i < result.length; i++) {
    listItems += '<li>' + result[i].Title + '</li>';
  }
  document.getElementById('Reviews').innerHTML = listItems;
}
```

这段代码声明了一个用于存储评论标题的字符串。它遍历 `result` 变量中的评论。虽然 JavaScript 无法预见，但通过使用字符串进行循环，你可以轻松访问集合中的所有项。在 `for` 循环内部，使用 `result[i].Title` 获取评论标题，然后将其封装在 `<li>` 标签中并附加到字符串变量中。最后，该字符串作为名为 `Reviews` 的元素的 `innerHTML` 添加（该元素在 HTML 中可能像这样：`<ul id="Reviews"></ul>`），这样评论标题就会以项目列表的形式出现。

当你输入这些内容时，你会注意到 `result` 对象没有 IntelliSense（智能感知）。由于 VS 并不不知道 `result` 变量的实际类型，因此无法帮助你找到如 `Id` 和 `Title` 之类的属性。

注意，这段代码有点笨拙。使用 `document.getElementById` 和 `innerHTML` 并不是编写此类代码的最佳方式。因此，下一章在讨论 jQuery 时将向你介绍更好的替代方案。不过，目前这足够了，展示了处理从 WCF 服务返回的复杂对象的核心概念。

重要的是，你在 JavaScript 中处理的 `Reviews` 对象与你在服务中使用的并不完全相同。VB.NET 或 C# 代码针对的是服务器端的 .NET Framework，而你的 JavaScript 运行在客户端。为了将对象传递到客户端，WCF 将评论集合序列化为 JavaScript 对象表示法 (JSON) —— 对象的字符串表示形式，可以直接在你的 JavaScript 代码中使用。你将在稍后的练习中看到 JSON 的示例。

Planet Wrox 项目中的 Web 服务将仅用于让浏览器中的客户端页面与服务器通信并交换数据。因此，在这个站点中，服务器和客户端都在同一个 Web 项目中——一个运行在客户端（调用 Web 服务器的 JavaScript）。

# 创建 Web 服务

使用 VS 创建 WCF 服务非常简单。就像所有其他类型一样，VS 都带了服务的模板。只需将服务添加到站点中。然后修改服务代码以符合你的需求。

# 创建 Web 服务

在本练习中，你创建一个简单的 "Hello World" Web 服务。该服务接受你的名称作为输入参数并返回一个个性化的问候。由于该服务的简单性，你可以专注于关注底层概念。

- 1. 在站点根目录下创建一个名为 `services` 的文件夹，将所有服务分组在一个文件夹中。这不是必须的，但有助于组织你的站点。
- 2. 接下来，右单击此文件夹并选择“新建项”。点击“WCF 服务（启用 Ajax）”。由于模板列表可能很长，你可以在对话框右上角的搜索框中搜索 WCF 来快速找到正确的项。
- 3. 点击“添加”将服务添加到站点。
- 4. 打开 `App_Code` 文件夹中的 `NameService` 后代码文件，将 `Do` 方法重命名为 `HelloWorld`，并修改代码使其接受字符串并返回个性化问候。在 VB 中你需要将代码从 `Sub` 改为 `Function` 并使其返回 `String`，在 C# 中则从 `void` 改为字符串方法，因为服务方法返回字符串。

# 第10章 ASP.NET AJAX

确保你点击对应你编程语言的项，并如图 10-6 所示调用 `NameService`。

```
VB.NET
Public Class NameService

    <OperationContract()>
    Public Function HelloWorld(name As String) As String
        Return String.Format("Hello {0}", name)
    End Function
End Class
```

```csharp
public class NameService
{
    [OperationContract]
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

