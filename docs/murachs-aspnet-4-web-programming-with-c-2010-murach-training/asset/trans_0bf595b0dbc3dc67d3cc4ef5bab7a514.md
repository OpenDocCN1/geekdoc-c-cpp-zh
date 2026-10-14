

![](img/c024ccf88e28c30c07dd410d4342288f_432_0.png)

## 定义 Select 语句的对话框

## Description

- 要配置 Select 语句，您可以选择是否使用自定义 SQL 语句，或从数据库中的表或视图中指定列。
- 如果您选择从表或视图中选择列，则可以選擇要检索的表或视图以及列。您可以点击 ORDER BY 按钮来指定记录的排序方式。并且您可以点击 WHERE 按钮来指定选择条件，如图 13-6 所示。
- 如果您选择使用自定义 SQL 语句，下一个对话框允许您输入如图 13-8 所示的 SQL 语句，或点击 Query Builder 按钮来构建如图 13-9 所示的查询。

Figure 13-5 How to configure the Select statement

## How to create a Where clause

如果您点击图 13-5 中第一个对话框中显示的 WHERE 按钮，则会显示图 13-6 中的 Add WHERE Clause 对话框。它允许您为 Select 语句创建 Where 子句和参数。

Where 子句由一个或多个条件组成，这些条件限制 Select 语句检索的行。要创建这些条件，Add WHERE Clause 对话框允许您将数据库表中列中的值与多种类型的数据进行比较，包括字面值、页面上另一个控件的值、通过页面 URL 传递的查询字符串的值，或 cookie。

例如，绑定到产品列表应用程序中的 DataList 控件的数据源的 Select 语句使用一个 Where 子句，该子句将 Products 表中的 CategoryID 列与从下拉列表中选择的类别进行比较。要创建此 Where 子句，请在 Column 下拉列表中选择 CategoryID，在 Operator 下拉列表中选择等于运算符，在 Source 下拉列表中选择 Control。接下来，在 Control ID 下拉列表中选择 ddlCategory。此时，控件的 SelectedValue 属性会被自动选中。然后，当您点击 Add 按钮时，此条件会显示在对话框的 WHERE 子句部分。

## The Add WHERE Clause dialog box

![](img/c024ccf88e28c30c07dd410d4342288f_434_0.png)

## The WHERE clause section after a condition has been added

![](img/c024ccf88e28c30c07dd410d4342288f_434_1.png)

## Description

- Add WHERE Clause 对话框允许您为 Select 语句指定 Where 子句。
- Where 子句由一个或多个条件组成，您可以使用此对话框中的控件构建这些条件。要创建条件，您需要选择要比较的列、用于比较的运算符以及用于比较的数据来源。然后，您必须点击 Add 将条件添加到 Where 子句条件列表中。
- 比较的数据来源可以是字面值、表单上另一个控件的值、cookie、HTML 表单字段、配置文件属性、页面 URL 中的查询字符串，或存储在会话状态中的值。

## Remember

- 在选择用于比较的列、运算符和来源后，请务必点击 Add 按钮将条件添加到生成的 Where 子句中。否则，条件将不会被添加到 Where 子句中。

Figure 13-6 How to create a Where clause

## How select parameters work

当您按照前一图所述创建 Where 子句时，向导会创建一个或多个 select 参数，这些参数提供 Where 子句使用的值。图 13-7 显示了这些 select 参数的工作方式。如您所见，每个包含 select 参数的 SqlDataSource 控件都由一个包含名为 SelectParameters 的子元素的 SqlDataSource 元素定义。然后，此元素包含 Select 语句使用的每个参数的子元素。

select 参数本身由第一表中列出的元素之一定义。这些元素中的每一个都指定一个参数，其值从不同类型来源获取。例如，如果参数的值从表单控件获取，则此控件参数由 ControlParameter 元素定义。类似地，QueryStringParameter 元素定义一个参数，其值来自用于页面的 URL 中的查询字符串。

此图中的第二张表列出了 ControlParameter 元素用于定义从表单控件获取值的参数的属性。如您所见，这些属性提供了参数的名称、用于参数的 SQL 数据类型、提供值的表单控件的 ID，以及用于获取值的属性名称。

此图顶部的代码示例显示了产品列表应用程序中使用的第二个 SqlDataSource 控件生成的 aspx 代码。在这里，Select 语句使用一个名为 CategoryID 的参数。此参数由 ControlParameter 元素定义，其 Name 属性设置为 CategoryID。此参数的 SQL 数据类型为 String，并且参数的值从 ID 为 ddlCategory 的表单控件的 SelectedValue 属性获取。

请注意，此示例中的代码是由 Web Forms Designer 在您使用 Data Source Configuration Wizard 配置数据源时生成的。因此，您不必自己编写此代码。

## The aspx code for a SqlDataSource control that includes a select parameter

```
```aspx
<asp:SqlDataSource ID="SqlDataSource2" runat="server"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"
    SelectCommand="SELECT [ProductID], [Name], [UnitPrice], [OnHand]
        FROM [Products]
        WHERE ([CategoryID] = @CategoryID)
        ORDER BY [ProductID]">
    <SelectParameters>
        <asp:ControlParameter Name="CategoryID" Type="String"
            ControlID="ddlCategory" PropertyName="SelectedValue" />
    </SelectParameters>
</asp:SqlDataSource>
```
```

## Elements used to define select parameters

| Element | Description |
|---|---|
| SelectParameters | 包含数据源的 Select 语句使用的每个参数的子元素。 |
| Parameter | 定义具有常量值的参数。 |
| ControlParameter | 定义从页面上的控件获取其值的参数。 |
| QueryStringParameter | 定义从用于请求页面的 URL 中的查询字符串获取其值的参数。 |
| FormParameter | 定义从 HTML 表单字段获取其值的参数。 |
| SessionParameter | 定义从会话状态中的项获取其值的参数。 |
| ProfileParameter | 定义从配置文件属性获取其值的参数。 |
| CookieParameter | 定义从 cookie 获取其值的参数。 |

## Attributes of the ControlParameter element

| Attribute | Description |
|---|---|
| Name | 参数名称。 |
| Type | 参数的 SQL 数据类型。 |
| ControlID | 提供参数值的 Web 表单控件的 ID。 |
| PropertyName | 提供参数值的 Web 表单控件的属性名称。 |

## Description

- SelectParameters 元素定义数据源的 Select 语句使用的 *select parameters*。定义这些参数的 aspx 代码在使用 Add WHERE Clause 对话框创建参数时会自动生成。
- *control parameter* 是从 Web 表单上的另一个控件获取其值的参数，例如下拉列表中选择的值。控件参数由 ControlParameter 元素定义。
- 一旦您了解如何使用控件参数，您就不应该有任何困难自行学习如何使用其他类型的参数。

Figure 13-7 How select parameters work

## How to use custom statements and stored procedures

本章前面您学习了如何通过从表中选择列来配置 SQL 数据源的 Select 语句。如果您需要编写比使用此技术可以创建的更复杂的 Select 语句，您可以定义自己的自定义语句。为此，您可以直接输入语句，或使用 Query Builder。您也可以使用数据库中已定义的存储过程。

## How to enter custom statements

如果您从图 13-5 所示的对话框中选择第一个选项，然后点击 Next 按钮，则会显示图 13-8 所示的对话框。如您所见，此对话框包含选项卡，允许您为数据源输入 Select、Update、Insert 和 Delete 语句。在这种情况下，Select 语句与本章前面由向导生成的语句相同。因此，您可能会认为您不需要输入自定义 Select 语句。请记住，通过从表中选择列来创建 Select 语句时，您无法控制生成的 Update、Insert 和 Delete 语句。因此，如果您想使用除自动生成的语句之外的语句，可以通过输入自定义语句来实现。

## How to select stored procedures

如果您想要用于选择、插入、更新和删除数据的存储过程已在数据库中定义，您可以轻松地在 SQL 数据源中使用它们。为此，您从图 13-8 所示对话框的相应选项卡中选择 Stored Procedure 选项。然后，您从出现的下拉列表中选择要用于该操作的存储过程。

