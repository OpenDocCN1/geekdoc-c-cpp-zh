

```
routes.MapRoute( _
    "Default", _
    "{controller}/{action}/{id}", _
    New With {.controller = "Home", .action = "Index", .id = ""} _
)
```

第一个参数是路由表中用作键的路由名称。第二个参数是 URL 模板。该模板表示可能有三个段：第一个映射到控制器名称，第二个映射到操作名称，第三个映射到 id。最后一个参数是一个匿名类型，定义了各段的默认值。

添加以下代码（在对 MapRoute 的现有调用之上）以添加一个映射，允许我们在浏览产品时将类别名称作为 URL 的一部分包含在内：

```
routes.MapRoute("BrowseProducts", _
    "Products/Browse/{Category}", _
    New With {.controller = "Products", .action = "Browse", .Category = ""})
```

来自 Global.asax 的代码片段

现在您应该能够运行应用程序并导航到 /Products/Browse/Beverages 或 /Products/Browse/Condiments 以查看这些类别中的产品。

## 脚手架和 CRUD 操作

我们已使用 Visual Studio 中的工具来协助我们创建控制器和视图，但我们尚未充分探索这些工具。它们具有额外的功能，可协助创建用于略微修改的 CRUD（创建、读取、更新和删除）操作的 action 方法和视图。

在开始创建新的 MVC 元素之前，我们需要重新审视 NorthwindRepository 类。需要两个新方法：一个按 ID 检索单个产品，第二个使我们能够保存对 LINQ to SQL 实体的任何更改：

```
Public Function GetProduct(ByVal id As Integer) As Product
    Dim query = From prod In _context.Products
                Where prod.ProductID = id
                Select prod
    Return query.SingleOrDefault()
End Function

Public Sub Save()
    _context.SubmitChanges()
End Sub
```

来自 \Models\NorthwindRepository.vb 的代码片段

完成这些更改后，我们现在能够正确探索 Visual Studio 中的脚手架工具。这些工具的工作方式与 Web Forms 中的数据服务器控件非常相似。通过指示要呈现的数据类型和所需的视图类型（列表、编辑、创建等），Visual Studio 可以使用反射来确定正在呈现的对象的属性并生成适当的标记和代码。

要亲眼看看这一点，请创建一个名为 AdminController 的新控制器，但这次选中“为 Create、Update 和 Details 场景添加 action 方法”选项，如图 23-12 所示。生成的代码包含 Index、Details、Create 和 Edit action 方法的基础实现。

我们将首先修改 Index action 方法。请求时，我们将返回一个视图，显示包含所有产品数据的网格。修改

![](img/d99870e80390742f93963da7be0b2e61_802_0.png)

图 23-12

```
<td>
    <%= Html.Encode(item.ProductName) %>
</td>
<td>
    <%= Html.Encode(item.CategoryID) %>
</td>
<td>
    <%= Html.Encode(String.Format("{0:F}", item.UnitPrice)) %>
</td>
<td>
    <%= Html.Encode(item.UnitsInStock) %>
</td>
<td>
    <%= Html.Encode(item.Discontinued) %>
</td>
</tr>
<% Next%>
</table>
```

来自 Views\Admin\Index.aspx 的代码片段

注意基于 ASP.NET MVC 约定的假设。Create 链接假定您将拥有 Create action 方法，Edit 链接假定您拥有一个以 ProductID 作为参数的 Edit action 方法，等等。如果没有约定，这些链接将无法代码生成。

运行应用程序并导航到 /Admin 应呈现与图 23-14 所示类似的页面。

![](img/d99870e80390742f93963da7be0b2e61_804_0.png)

# 图 23-14

接下来是 Details action 方法，修改代码以从存储库获取请求的 product 并将其传递给 Details 视图：

```
'
' GET: /Admin/Details/5

Function Details(ByVal id As Integer) As ActionResult
```

我们将 Edit 操作分为两部分。第一部分涉及生成允许编辑产品数据的表单；第二部分涉及在用户提交表单时接收更新的数据。

Edit action 方法将与 Details action 方法具有相同的实现。修改它以便检索请求的 product 并返回 Details 视图：

```
' GET: /Admin/Edit/5

Function Edit(ByVal id As Integer) As ActionResult
    Dim product = _repository.GetProduct(id)
    Return View(product)
End Function
```

来自 \Controllers\AdminController.vb 的代码片段

生成一个强类型视图，选择 Edit 作为视图内容下拉列表，如图 23-16 所示。

```
<h2>Edit Product</h2>

<script src="../../Scripts/jquery-1.3.2.min.js" type="text/javascript"></script>
<script src="../../Scripts/jquery.validate.min.js" type="text/javascript"></script>
<script src="../../Scripts/MicrosoftMvcJQueryValidation.js" type="text/javascript"></script>

<%= Html.ValidationSummary("Edit was unsuccessful. Please correct the errors ... ") %>
<% Html.EnableClientValidation() %>

<% Using Html.BeginForm() %>

    <fieldset>
        <legend>Fields</legend>
        <p>
            <label for="ProductName">ProductName:</label>
            <%= Html.TextBox("ProductName", Model.ProductName) %>
            <%= Html.ValidationMessage("ProductName", "*") %>
        </p>
        <p>
            <label for="SupplierID">SupplierID:</label>
            <%= Html.TextBox("SupplierID", Model.SupplierID) %>
            <%= Html.ValidationMessage("SupplierID", "*") %>
        </p>
        <!-- Some fields removed for brevity -->
        <p>
            <%= Html.LabelFor(Function(p) p.Discontinued) %>
            <%= Html.EditorFor(Function(p) p.Discontinued) %>
            <%= Html.ValidationMessage("Discontinued", "*") %>
        </p>
        <p>
            <input type="submit" value="Save" />
        </p>
    </fieldset>

<% End Using %>

<div>
    <%=Html.ActionLink("Back to List", "Index") %>
</div>
```

来自 \Views\Admin\Edit.aspx 的代码片段

生成的视图中需要进一步讨论的几件事。请注意，代码片段中的几个元素涉及验证。ASP.NET MVC 1.0 支持服务器端验证，而 ASP.NET MVC 2 增加了对客户端验证的原生支持。指向脚本文件的链接包括实现客户端验证框架所需的 JavaScript。其中一个文件是 jQuery 基础库，第二个是 jQuery 验证插件。Microsoft 将 jQuery 作为 ASP.NET 4 的一部分包含在内，并将其基础库作为许多开箱即用的项目模板（包括我们当前使用的模板）的一部分。很安全地认为，我们将在未来经常看到 jQuery 作为 Visual Studio 项目和项目模板的一部分使用。ValidationSummary 和 ValidationMessage HTML 助手的作用与 Web Forms 框架中的验证服务器控件非常相似。您将在下一节中更深入地了解如何实现规则以填充这些控件。

![](img/d99870e80390742f93963da7be0b2e61_807_0.png)

下一个值得注意的是 TextBox 助手的用法。可以使用几种 HTML 助手来呈现文本框、复选框、按钮、下拉列表等固有元素。自动脚手架的当前实现在生成的代码中使用了这种类型的助手。

ASP.NET MVC 2 添加了新的强类型助手方法，使编译时检查和 IntelliSense 更好。Discontinued 属性的标记和代码已修改为使用新的 LabelFor 和 EditorFor 助手。这两种方法都期望 lambda 表达式作为参数返回属性的值。反射用于确定属性的名称，以便可以在标签中显示，以及属性的类型，以便可以呈现适当的 HTML 元素来显示和编辑。在我们的示例中，Discontinued 属性是 Boolean，因此在表单中呈现了复选框。可以预见，脚手架机制将很快被修改为生成这些强类型助手。

最后值得注意的是 BeginForm 助手。此方法负责呈现 HTML 表单标签，该标签将确定在用户提交表单时如何将更新的数据发送到客户端。调用不带任何参数的 BeginForm 将导致表单数据通过 HTTP POST 发送到当前 URL。为处理 POST，我们有一个第二个 Edit action 方法：

```vb
' POST: /Admin/Edit/5

<AcceptVerbs(HttpVerbs.Post)> _
Function Edit(ByVal id As Integer, ByVal collection As FormCollection) As ActionResult
    Dim product = _repository.GetProduct(id)
    Try
        UpdateModel(product)
        _repository.Save()
        Return RedirectToAction("Index")
    Catch
        Return View(product)
    End Try
End Function
```

*来自 \\Controllers\\AdminController.vb 的代码片段*

