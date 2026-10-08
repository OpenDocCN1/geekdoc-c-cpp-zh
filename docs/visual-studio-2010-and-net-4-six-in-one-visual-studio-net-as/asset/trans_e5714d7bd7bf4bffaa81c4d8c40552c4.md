

```csharp
{
  editedBook.Validate(ModelState);
  if (ModelState.IsValid)
  {
    // ...
    return View(editedBook);
  }
}
```

## 客户端验证

在许多情况下，最简单的验证规则可以在客户端进行检查，而无需与服务器进行往返交互。在 MVC 2 中，使用基于 JavaScript 的客户端验证非常简单。当你创建 ASP.NET MVC 2 Web 应用程序时，所需的 JavaScript 文件会被复制到 Scripts 文件夹中。你可以轻松地为你的视图（views）添加客户端验证支持。例如，你可以修改 Create.aspx 文件的主要内容，如下代码提取所示：

```asp
<asp:Content ID="ContentHolderID" Content="MainContent" runat="server">
  <script src="Scripts/MicrosoftAjax.js" type="javascript"></script>
  <script src="Scripts/MicrosoftMvcValidation.js" type="javascript"></script>
  <%: Html.EnableClientValidation(); %>
  <h2><%: Html("Create") %></h2>
  <%: Html.BeginForm() %>
    <%: Html.ValidationSummary(false, "There are some invalid input data:") %>
    <fieldset>
      <legend>New Book Attributes</legend>
      <div class="editor-label">
        <%: Html.LabelFor(model => model.Author) %>
      </div>
      <div>
        <!-- 其他字段在列表中已省略 -->
      </div>
    </fieldset>
  <% } %>
  <div>
    <%: Html.ActionLink("Back to List", "Index") %>
  </div>
</asp:Content>
```

你必须只需要添加那两个 `<script>` 标签，并使用 `<%: Html.EnableClientValidation()%>` 标签。当你下一次运行应用程序时，由 Book 元数据（metadata）定义的模型规则将在客户端进行验证。

然而，在使用客户端验证时，你应该注意以下两点重要的事情：

- 你在服务器端显式实现的自定义验证代码（例如，检查未来出版日期的规则）不会被检查——因此，其失败结果不会在客户端标出。当使用客户端验证规则时，模型数据会被发送到服务器，并在那里进行服务器端验证。

即使你在客户端实现了验证，也绝不能只信任客户端验证。健壮的业务逻辑应该在服务器（服务层）同样检查所有的业务规则。

## UI 定制

添加视图（Add View）命令（可在代码编辑器的右键菜单中，或从解决方案管理器中可用）可以帮助你在几秒钟内生成一个视图。这可能很快且易于操作，但不一定是你想要放入应用程序正式版本中的内容。ASP.NET MVC 2 框架提供了许多方法，根据你的样式以及你公司或客户的标准设计来定义 UI。

在 Views/Shared 文件夹中，你可以看到 Site.Master 页面和 Content 文件夹持有 Site.cs 文件。你可以使用与任何其他 ASP.NET 应用程序相同的技术，通过更改/添加主文件和 CSS 文件来更改应用程序的通用输出。由于这些文件的结构，练的 Web 设计师可以为你的 MVC 2 应用程序创建出且迷人的网站。

然而，你还有其他方法可以自定义应用程序中的视图。

## 使用模板助手（Templated Helpers）

MVC 2 有一项名为“模板助手”（template helpers）的新功能，这可能是对开发人员效率最重要的功能。在本章较之前的视图源代码列表中，你可能会看到几个未经过解释的渲染标签，例如：

```asp
<@ using (Html.BeginForm()) %>
<%= Html.LabelFor(model => model.Author) %>

<%= Html.TextBoxFor(model => model.Title) %>
<%= Html.ValidationMessage(model => model.Title) %>

<%= Html.ActionLink("Back to List", "Index") %>
```

