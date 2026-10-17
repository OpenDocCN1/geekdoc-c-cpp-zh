
- **表示层**由管理应用程序外观的 ASP.NET 页面组成。此层可以包含绑定数据控件和`ObjectDataSource`对象，这些控件和对象将数据控件绑定到数据。

- **中间层**包含管理应用程序数据访问的*数据访问类*。此层还可以包含业务对象，这些对象表示客户、产品或员工等业务实体，并实现信用和折扣策略等业务规则。

- **数据库层**由包含应用程序数据的数据库组成。理想情况下，执行数据库访问的 SQL 语句应保存在数据库内的存储过程中，但 SQL 语句通常存储在数据访问类中。

## 说明

- *对象数据源*由`ObjectDataSource`控件实现，它允许你在数据库应用程序中使用*三层架构*进行数据绑定。

- 对象数据源与 SQL 数据源类似。但是，对象数据源不是直接访问数据库，而是通过处理数据库访问细节的数据访问类获取数据。

另外，你可能习惯于用*三层体系结构*来指代图 17-1 中描述的*三层架构*。不过，因为有些人使用*三层体系结构*来指代将三个层分别放在三台不同物理设备上的架构，所以我在本章中使用了*三层架构*这一术语。虽然你可以将三个层分别放置在三台设备上，但并非必须如此。

## 如何使用 `ObjectDataSource` 控件

图 17-2 介绍了使用`ObjectDataSource`控件的基础知识。此图顶部的图像显示了绑定到下拉列表的`ObjectDataSource`控件在 Web Forms 设计器中的外观。然后，第一个代码示例显示了下拉列表及其所绑定对象数据源的`aspx`代码。与任何其他数据源一样，你可以通过从工具箱中拖动对象数据源，或从可绑定控件中选择“选择数据源”命令，将对象数据源添加到网页中。

在第一个代码示例中，你可以看到下拉列表绑定到对象数据源的方式与绑定到 SQL 数据源的方式完全相同。唯一的区别是`DataSourceID`属性提供的是对象数据源的 ID，而不是 SQL 数据源的 ID。你还可以看到，`ObjectDataSource`控件的代码除了必需的 ID 和`runat`属性之外，只有两个属性。`TypeName`属性提供数据访问类的名称，`SelectMethod`属性提供用于检索数据的方法名称。在本例中，数据访问类是`ProductDB`，选择方法是`GetAllCategories`。

此图中的第二个代码示例展示了`ProductDB`类的`GetAllCategories`方法。该方法使用直接的 ADO.NET 代码从`Categories`表检索类别行，并返回一个可用于读取这些类别行的数据读取器。但请注意，此方法的返回类型是`IEnumerable`。因为`SqlDataReader`类实现了`IEnumerable`接口，所以数据读取器是该方法的有效返回对象。（你将在图 17-8 中详细了解 select 方法可接受的返回类型。）

## 绑定到 `ObjectDataSource` 控件的下拉列表

![](img/c024ccf88e28c30c07dd410d4342288f_588_0.png)

## 下拉列表和 `ObjectDataSource` 控件的代码

```
<asp:DropDownList ID="ddlCategories" runat="server" AutoPostBack="True"
    DataSourceID="ObjectDataSource1"
    DataTextField="ShortName"
    DataValueField="CategoryID">
</asp:DropDownList>
<asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
    TypeName="ProductDB"
    SelectMethod="GetAllCategories">
</asp:ObjectDataSource>
```

## `ProductDB` 类的 `GetAllCategories` 方法

```
[DataObjectMethod(DataObjectMethodType.Select)]
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

## `ObjectDataSource` 控件的基本属性

| 属性 | 描述 |
|---|---|
| `ID` | 控件的 ID。 |
| `Runat` | 必须指定为`"server"`。 |
| `TypeName` | 数据访问类的名称。 |
| `SelectMethod` | 检索数据的方法的名称。 |
| `UpdateMethod` | 更新数据的方法的名称。 |
| `DeleteMethod` | 删除数据的方法的名称。 |
| `InsertMethod` | 插入数据的方法的名称。 |
| `DataObjectTypeName` | 提供属性以用于传递参数值的类的名称。 |
| `ConflictDetection` | 指定如何检测并发冲突。`CompareAllValues` 使用乐观并发检查。`OverwriteValues`（默认值）不执行并发检查。 |

## 说明

- `ObjectDataSource`控件指定数据访问类的名称以及用于选择、更新、删除和插入数据的方法。

## 如何配置 `ObjectDataSource` 控件

图 17-3 显示了如何使用 Configure Data Source 对话框来配置对象数据源控件。正如你所见，第一个对话框让你选择将与此对象数据源关联的业务对象。你在此处的选择将用于`ObjectDataSource`控件的`TypeName`属性中。 （请注意，Microsoft 在此向导中将数据访问类称为业务对象。在其他上下文中，Microsoft 却将数据访问类称为数据对象或数据组件。）

第一个对话框中的下拉列表列出了`App_Code`文件夹中所有可用的类。如果你选中“Show Only Data Components”复选框，则只会列出将自身标识为数据组件的类。在图 17-10 中，你将学习如何以这种方式标记类。

当你选择一个数据访问类并单击 Next 时，会显示第二个 Configure Data Source 对话框。在这里，你可以选择要用于检索对象数据源数据的方法。你选择的方法在`ObjectDataSource`控件的`SelectMethod`属性中指定。 （在此步骤中，向导使用 .NET 的一个特性 reflection 来确定所有可用方法，你稍后会了解更多关于 reflection 的内容。）

如果你选择一个需要参数的 select 方法，Define Parameters 步骤会让你指定每个必需参数的来源。然后，Visual Studio 会生成定义`ObjectDataSource`控件所需参数的元素。这与使用 SQL 数据源时的工作方式相同。

正如你在此图中看到的，第二个 Configure Data Source 对话框还提供了选项卡，让你指定 update、insert 和 delete 操作的方法。本章后面你将看到一个使用这些方法的应用。但现在，我只关注如何使用`ObjectDataSource`控件来检索数据。

## 如何使用绑定控件

虽然你可以将下拉列表或`GridView`控件等控件绑定到对象数据源，但你不能像使用 SQL 数据源时那样使用设计器来选择单个字段。那是因为字段是在数据访问类中定义的，而不是直接在数据源中定义的。例如，当你绑定下拉列表时，你必须手动输入要显示的字段名称以及控件值的字段名称。同样，当你绑定`GridView`控件时，你必须手动输入要绑定的每个字段的名称，如果控件提供排序功能，你还必须为每个排序表达式输入字段名称。此外，你还必须为控件的`DataKeyNames`属性输入适当的字段名称或名称。例外情况是如果 select 方法返回强类型集合。你将在本章后面看到类似的示例。现在，只需意识到由于返回强类型集合的 select 方法可以使对象数据源更易于使用，因此在有意义时应尽可能使用它们。

## 配置数据源的对话框

![](img/c024ccf88e28c30c07dd410d4342288f_590_0.png)

## Description

- 你可以通过从其 smart tag 菜单中选择 Configure Data Source 来使用 Configure Data Source 对话框配置`ObjectDataSource`控件。
- Choose a Business Object 步骤让你选择要使用的数据访问类。
- Define Data Methods 步骤包含选项卡，让你选择要用于 select、update、insert 和 delete 操作的方法。
- 如果你选择一个需要参数的方法，将会出现 Define Parameters 步骤。此步骤将让你选择该方法所需每个参数的来源。例如，你可以指定下拉列表应作为参数的来源。
- 如果你从绑定控件创建新的数据源，Data Source Configuration Wizard 会要求你选择数据源类型。要创建对象数据源，请选择 Object 选项。然后，当你单击 Next 按钮时，将显示上面显示的第一个对话框。

Figure 17-3    如何配置 `ObjectDataSource` 控件

## 一个 Product List 应用

为了说明使用`ObjectDataSource`控件的基础知识，图 17-4 展示了一个 Product List 应用。此应用在外观上与第 13 章中介绍的 Product List 应用完全相同。但是，它不是使用`SqlDataSource`控件来检索数据，而是使用`ObjectDataSource`控件。

该图还列出了此应用使用的数据访问类`ProductDB`提供的方法。第一个方法`GetAllCategories`返回一个`IEnumerable`对象（实际上是一个 data reader），其中包含`Categories`表中所有类别的数据。此数据仅包括每个类别的类别 ID 和长名称。

第二个方法`GetProductsByCategory`返回一个`IEnumerable`对象（同样是一个 data reader），其中包含`Products`表中所有具有由参数提供的类别 ID 的产品。此参数将绑定到下拉列表的`SelectedValue`属性。因此，用户选择的类别的 ID 将传递给`GetProductsByCategory`方法。

此应用说明了使用对象数据源如何让你将表示代码与数据访问代码分离。正如你将看到的，所有表示代码都在`aspx`文件中。而所有数据访问代码都在名为`ProductDB`的数据访问类中。

## `aspx` 文件

图 17-5 显示了 Product List 应用的`Default.aspx`页面的主要部分。如果你将此列表与图 13-16 中显示的列表进行比较，你会发现唯一的区别是`SqlDataSource`元素已被`ObjectDataSource`元素替换。换句话说，无论应用使用 SQL 数据源还是对象数据源，下拉列表和`DataList`控件的代码都是相同的。

在第一个`ObjectDataSource`控件中，`TypeName`属性指定`ProductDB`，`SelectMethod`属性指定`GetAllCategories`。因此，当下拉列表绑定时，将调用`ProductDB`数据访问类中的`GetAllCategories`方法来检索类别数据。

在第二个`ObjectDataSource`控件中，`SelectParameters`元素内的`ControlParameter`元素用于声明`CategoryID`参数。此参数绑定到下拉列表的`SelectedValue`属性。

由于此应用的数据绑定完全在`aspx`文件中定义，因此此页没有 code-behind 文件。因此，此应用的唯一 C# 代码位于`ProductDB`类中，该类在下一幅图中介绍。

## `Default.aspx` 文件的主要部分

```
<div id="main">
    <p>
        Choose a category:&nbsp;
        <asp:DropDownList ID="ddlCategory" runat="server"
            DataSourceID="ObjectDataSource1" DataTextField="LongName"
            DataValueField="CategoryID" AutoPostBack="True">
        </asp:DropDownList>
        <asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
            SelectMethod="GetAllCategories" TypeName="ProductDB">
        </asp:ObjectDataSource>
    </p>
    <asp:DataList ID="dlProducts" runat="server" DataKeyField="ProductID"
        DataSourceID="ObjectDataSource2" CellPadding="3" GridLines="Vertical">
        <HeaderTemplate>
            <table>
                <tr>
                    <td class="col1">ID</td>
                    <td class="col2">Product</td>
                    <td class="col3">Unit Price</td>
                    <td class="col4">On Hand</td>
                </tr>
            </table>
        </HeaderTemplate>
        <ItemTemplate>
            <table>
                <tr>
                    <td class="col1">
                        <asp:Label ID="lblID" runat="server"
                            Text='<%# Eval("ProductID") %>' /></td>
                    <td class="col2">
                        <asp:Label ID="lblName" runat="server"
                            Text='<%# Eval("Name") %>' /></td>
                    <td class="col3">
                        <asp:Label ID="lblUnitPrice" runat="server"
                            Text='<%# Eval("UnitPrice", "{0:C}") %>' /></td>
                    <td class="col4">
                        <asp:Label ID="lblOnHand" runat="server"
                            Text='<%# Eval("OnHand") %>' /></td>
                </tr>
            </table>
        </ItemTemplate>
        <AlternatingItemStyle BackColor="#CCCCCC" />
        <HeaderStyle BackColor="Black" Font-Bold="True" ForeColor="White" />
    </asp:DataList>
    <asp:ObjectDataSource ID="ObjectDataSource2" runat="server"
        SelectMethod="GetProductsByCategory" TypeName="ProductDB">
        <SelectParameters>
            <asp:ControlParameter ControlID="ddlCategory" Name="CategoryID"
                PropertyName="SelectedValue" Type="String" />
        </SelectParameters>
    </asp:ObjectDataSource>
</div>
```

## `ProductDB` 类
