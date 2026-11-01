
他们仍然会看到以原始请求的主题呈现的页面。输出缓存可能出现问题的另一个情况是当你使用与安全相关的控件时，例如 LoginView（将在下一章讨论）。这些控件可以根据当前登录的用户显示内容。如果该页面被缓存，其他用户将看到属于第一个请求该页面的用户的内容。

解决此问题的一个办法是不在页面级别使用输出缓存，而是将适用于所有用户的内容移至单独的用户控件中，然后将其嵌入页面中，就像你看到的对联系表单的处理方式一样。例如，新闻文章列表或完整的评论列表对所有用户都相同。如果你将这些列表的代码移至启用了输出缓存的用户控件中，则包含页面仍会为每个用户单独创建，但用户控件的内容只在第一次生成，然后对所有后续请求重复使用。

另一种解决方案是指示数据源控件为你缓存数据，如下一节所示。

如果你不受输出缓存的缺点影响（例如不使用主题或与安全相关的控件时），输出缓存是提高站点性能的绝佳机制。

## 使用数据源控件进行缓存

使用数据源控件缓存的最大好处是它们只缓存动态的、基于数据库的数据，而不是整个页面。这使你能够保持页面的其他部分动态，例如横幅模块或个性化问候语欢迎用户。缓存在大多数数据源控件上是设计支持的，除了 SiteMapDataSource、LinqDataSource 和 EntityDataSource 控件。

使用数据源控件进行缓存非常容易：你只需设置 EnableCaching 属性，然后指定 CacheDuration。以下代码片段显示了一个缓存其数据 10 分钟的 SqlDataSource 控件：

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server" CacheDuration="600" EnableCaching="True"></asp:SqlDataSource>
```

关于数据源控件缓存的酷之处在于它们足够智能，能够检测你是否对底层数据进行了更新。因此，当你设置 SqlDataSource 控件缓存 SelectCommand 的数据 20 分钟，但随后使用 InsertCommand、UpdateCommand 或 DeleteCommand 对数据进行更改时，缓存会自动失效。这仅在你对完全相同的 SqlDataSource 执行插入、更新或删除命令时才有效。如果你有一个页面用于显示并缓存评论列表（例如 All.aspx），然后另一个页面用于插入新评论（例如 Management 文件夹中的 AddEditReview.aspx），则此方法不起作用。在网站的管理部分插入新评论后，它不会在 All.aspx 中显示，直到缓存过期为止。

数据源控件的无代码缓存在使用许多情况下很有用。然而，并非在每种情况下都可以使用数据源控件。如果想缓存从完全不同来源获取的数据结果怎么办？如果想缓存在针对 Entity Framework 的手工编码页面中接收的数据，或频繁需要访问的文本或 XML 文件的内容怎么办？对于这些情况，ASP.NET 为你提供了对缓存的编程访问。

## 编程缓存

使用编程缓存，你可以通过 VB.NET 或 C# 代码将项目存储在缓存中。显然，你也可以稍后再次访问它们。要存储项目，你可以使用 Add 或 Insert 方法，或直接索引 Cache 集合。Add 方法功能强大（且复杂），可让你指定大量选项，以确定项目缓存多长时间、与其他缓存项目相比应具有的优先级以及触发项目从缓存中移除的因素。

另一方面，Insert 方法要容易得多。它有几个简短的重载，可让你指定缓存的项目并将其与特定键关联。另一个重载还可让你定义依赖项，当原始源更改时可用于使缓存的项目失效。这对于缓存不经常更改的文件非常有用。你可以从磁盘读取文件，并将其存储在缓存中，同时依赖原始文件。然后你继续从缓存而不是磁盘读取文件。当磁盘上的文件更改时，缓存的项目会自动失效，你可以再次读取原始源文件并将其存储在缓存中。以下示例显示如何修改 ContactForm.ascx 用户控件，以便在项目更改之前将其存储并从缓存中获取：

```vbnet
If Page.IsValid Then
    Dim mailBody As String = TryCast(Cache("ContactFormMailBody"), String)
    If String.IsNullOrEmpty(mailBody) Then
        Dim fileName As String = Server.MapPath("~/App_Data/ContactForm.txt")
        mailBody = System.IO.File.ReadAllText(fileName)
        Cache.Insert("ContactFormMailBody", mailBody, New CacheDependency(fileName))
    End If
    mailBody = mailBody.Replace("##Name##", Name.Text)
    ...
End If
```

```csharp
if (Page.IsValid)
{
    string mailBody = Cache["ContactFormMailBody"] as string;
    if (string.IsNullOrEmpty(mailBody))
    {
        string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
        mailBody = System.IO.File.ReadAllText(fileName);
        Cache.Insert("ContactFormMailBody", mailBody, new CacheDependency(fileName));
    }
    mailBody = mailBody.Replace("##Name##", Name.Text);
    ...
}
```

注意如何创建一个新的 CacheDependency（为此你需要使用 Imports/using 语句将 System.Web.Caching 命名空间引入作用域）并将其传递给 Insert 方法。此 CacheDependency 预期其依赖的文件的名称。一旦你更改磁盘上的文件（例如使用 VS 或 Notepad），ASP.NET 就会从缓存中移除该项目，以便下次执行此代码时再次从原始源文件读取。

你使用接受缓存项目键的 Remove 方法从缓存中移除项目。你在插入项目时使用 Add 或 Insert 定义此键。

要访问缓存中的项目，你有几种可用的选项。首先，你可以直接访问 Cache 集合：

### VB.NET

```
myReview = TryCast(Cache(myKey), Review)
```

### C#

```
Review myReview = Cache[myKey] as Review;
```

这里，Cache 集合使用存储在 myKey 变量中的键进行索引。

此外，你可以使用期望键的 Get 方法：

### VB.NET

```
myReview = TryCast(Cache.Get(myKey), Review)
```

### C#

```
Review myReview = Cache.Get(myKey) as Review;
```

因为 Get 是一个方法，C# 示例现在也在缓存键周围使用括号，使两个示例看起来更相似。

最后，你可以使用 Item 属性访问缓存中的项目，该属性也接受缓存项目的键。

所有三种访问缓存中项目的方式在找不到项目时始终返回对象或 Nothing/null。这意味着如果你知道从缓存中获取回的类型，则应在使用其属性之前使用 VB.NET 中的 TryCast 或 C# 中的 as 关键字将其转换为适当的类型。前两个示例向你展示了如何首先将缓存中的项目转换为强类型的 Review 对象。

为了让你了解如何以编程方式使用缓存，下一个练习将向你展示如何将评论插入缓存，以便每次需要时不必从数据库中获取它。

## 试一试 使用缓存 API

在此试一试练习中，你将看到如何缓存使用 LINQ to Entities 查询从 EF 获取的 Review 实例，以便以后通过其键（包含评论者 ID）检索它，

- 1. 首先在 Web 应用程序的 Reviews 文件夹中添加一个名为 ViewDetails.aspx 的新页面。确保它基于你的自定义模板。无需设置显式标题，因为它将以编程方式设置。相反，从 Page 指令中删除 Title="" 属性。ASP.NET 中有一个有趣且古老的错误，会导致当此属性在标记视图中设置为空字符串时，对页面的 Title 的编程修改无法生效。
- 2. 在标记视图中，向 cpMainContent 内容占位符添加三个 Label 控件，并按如下方式命名控件：
  - TitleLabel
