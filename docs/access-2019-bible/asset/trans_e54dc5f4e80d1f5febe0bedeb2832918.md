

CheckBox 控件的建立方式与任何其他 Ribbon 控件类似：

```
<tab id="ch30_t_Outdoor" label="Outdoor">
    <group id="ch30_g_Sports" label="Sports">
        <checkBox id="chkBaseball" label="Baseball" ...
        <checkBox id="chkBasketball" label="Basketball" ...
        <separator id="outdoor_Sep1"/>
        <checkBox id="chkTennis" label="Tennis" ...
        <checkBox id="chkWaterPolo" label="Water Polo" ...
    </group>
    <group id="ch30_g_Camping" label="Camping Supplies">
        <checkBox id="chkTent" label="Tent" ...
        <checkBox id="chkGranola" label="Granola" ...
        <checkBox id="chkLantern" label="Lantern" ...
        <separator id="camping_Sep1"/>
        <button id="btnCamping" imageMso="StartTimer"
            size="large" label="A Big Button" />
    </group>
</tab>
```

> **注意**
> 
> 我们移除了部分 XML 并用省略号字符替换，以提高此示例 XML 的清晰度。

此 XML 代码生成的选项卡显示在图 30.22 中（并包含在 Chapter30.accdb 数据库中的 ControlExamples.xml 示例 Ribbon 中）。

## 图 30.22

当用户需要在多个选项中进行选择时，CheckBox 控件是不错的选择。

![](img/1e45673ab6eca9d20e67635ff5b9b318_1027_0.png)

图 30.22 中显示的 Ribbon CheckBox 控件的工作方式正如你所期望的那样。复选框可以单独选择或以任意组合选择。CheckBox 控件不是互斥的，每个控件可以有自己的 onAction 属性，或者多个控件可以共享一个回调过程。

## DropDown 控件

DropDown 控件比我们已介绍的标签、按钮和复选框示例更复杂。它包含一个供用户选择的项目列表。因此，DropDown 有许多定义其外观的属性，以及填充其列表的回调：

```
```xml
<dropDown
    id="ddLogin"
    label="Login" supertip="Select your employee name...
    screentip="Login Name"
    getItemCount="ddLogin_GetItemCount"
    getItemLabel="ddLogin_getItemLabel"
    onAction="ddLogin_onAction" />
```
```

id、label、screentip 和 supertip 属性定义 DropDown 控件的外观。getItemCount 和 getItemLabel 填充 DropDown 的列表。onAction 指定处理控件操作的回调。图 30.23 显示了本节中创建的 DropDown。

## 图 30.23

DropDown 控件列出用户的姓名。

![](img/1e45673ab6eca9d20e67635ff5b9b318_1028_0.png)

典型 DropDown 的 VBA 回调显示在以下代码中。DropDown 需要两个主要回调。第一个设置要在列表中显示的项目数，第二个实际填充列表：

```
```vba
Public Sub ddLogin_GetItemCount( _
    control As IRibbonControl, ByRef count)

    count = Nz(DCount("*", "tblSalesPerson"), 0)

End Sub

Public Sub ddLogin_getItemLabel( _
    control As IRibbonControl, index As Integer, ByRef label)

    Dim sName As String

    sName = Nz(DLookup("SalespersonName", _
```

```
"tblSalesPerson", "SalesPersonID = " & index + 1), _
vbNullString)

label = sName

End Sub
```

第一个回调（ddLogin_getItemCount）获取要放置在 DropDown 列表上的项目数。请注意 ByRef count 参数。此参数告诉 DropDown 其列表需要容纳多少个项目。

第二个过程（ddLogin_getItemLabel）实际检索列表的项目。在此例中，该过程使用 DLookup 从 tblSalesPersons 中提取 SalesPerson 名称字段。ddLogin_getItemLabel 会被 DropDown 多次调用；调用的确切次数由 ddLogin_getItemCount 确定的 count 值决定。

准确计算要添加到 DropDown 的值数量很重要。DropDown 除了 count 参数外，没有其他方式知道应期望多少个项目。设置 count 过低意味着并非所有项目都会被添加，而设置 count 过高则意味着列表中包含空白。举例来说，如果你将 count 设置为十个项目但只有五个可用，则 DropDown 的列表包含五个项目，同时还有五个空白。

ddLogin_getItemLabel 例程在提供此信息时有点取巧。请注意传递给此例程的 index 参数，它告诉过程在调用时正在填充下拉列表的哪个位置。DLookup 对此值加 1 并提取其 ID 与该值匹配的销售人员的姓名。这意味着 SalesPersonID 值必须从 1 开始顺序排列，否则此过程将失败。

提取具有非顺序 ID 值或 ID 值非数字的数据需要多做一些工作。在以下代码中，ddLogin_getItemLabel 已重写为使用记录集而不是 DLookup 函数。ddLogin_onAction 过程以相同方式使用记录集：

```
Private Const msSQLSALESPERSON As String = _
    "SELECT SalesPersonName FROM tblSalesPerson ORDER BY
    SalesPersonName;"

Public Sub ddLogin_getItemLabel( _
    control As IRibbonControl, index As Integer, ByRef label)

    Dim adRs As ADODB.Recordset

    Set adRs = CurrentProject.Connection.Execute(msSQLSALESPERSON)
    adRs.Move index

    label = adRs.Fields(0).Value

End Sub
```

```
Public Sub ddLogin_onAction(
    control As IRibbonControl, id As String, index As Integer)

    Dim rs As DAO.Recordset

    Set rs = CurrentDb.OpenRecordset(msSQLSALESPERSON, dbopendynaset)
    rs.Move index

    MsgBox "You are logged in as " & rs.Fields(0).Value & ".", vbOKOnly, "Logged In"

End Sub
```

两个过程都使用相同的模块级常量 msSQLSALESPERSON。这确保记录按相同顺序排序。Move 方法移动到 index 指定的记录，如果记录在不同过程之间的顺序不同，则会返回错误的名字。销售人员的姓名使用 rs.Fields(0).Value 语句检索。通过在模块级常量中控制 SQL 语句，你可以确保第一个字段（.Fields(0)）包含正确的信息。

> 注意
> Ribbon 包含三个外观相似的控件。本节讨论的 DropDown 控件在视觉上与 Menu 控件（参见图 30.3）和 ComboBox 控件有很多共同点。（“开始”选项卡上的“文本格式”组中的字体组合框就是一个例子。）DropDown 和 ComboBox 控件使用 getItemCount 和 getItemLabel 回调来填充其列表，而 Menu 控件则在 XML 中直接包含 Button 元素。你应该了解这些控件之间的差异，以便为你的应用程序选择最佳控件。
> 
> DropDown 控件强制用户从列表中选择一个项目并在控件中显示所选项目。虽然 DropDown 控件看起来像 ComboBox 控件，但用户不能直接编辑该值。
> 
> ComboBox 控件的工作方式与 DropDown 类似，只是用户可以直接在控件中编辑值，并且不限于列表中的项目。DropDown 控件和 CombBox 控件类似于你在窗体上可能使用的列表框和组合框。
> 
> 三个控件中最简单的是 Menu 控件，它是一组执行操作的按钮。所选值的数值不会在控件中显示，并且按钮不能动态创建。

## SplitButton 控件

SplitButton 控件在用户可能从多个不同选项中选择，但其中一个选项使用频率高于其他选项的情况下非常有用。一个例子可能是多个报表，其中一个报表经常打印，而其他报表打印较少。设计表格时“开始”选项卡上的“视图”SplitButton 就是一个很好的例子（参见图 30.2）。View SplitButton 的按钮部分会根据上下文而变化。如果用户已处于数据表视图，则按钮会更改为设计视图，反之亦然。

