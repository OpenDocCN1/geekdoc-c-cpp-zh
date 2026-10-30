

当然，你将在 Try / Catch 块中包含上述代码。你将在后面的完整代码示例中看到异常处理。

## 将数据字段绑定到窗体控件

由于 DataSet 是在运行时创建的，因此你不能在设计时绑定窗体的控件。但在检索到 DataSet 后，你可以将 DataSet 中的字段绑定到窗体控件。

绑定窗体控件的最佳方式是使用 BindingSource 对象。你在代码中声明并实例化一个新的 BindingSource 对象，并设置其 DataSource 和 DataMember 属性。然后你可以将窗体控件绑定到 BindingSource 对象。

```
' Set up the binding source.
Dim ABindingSource As New BindingSource
With ABindingSource
    .DataSource = APubsDataSet
    .DataMember = "employee"
    .Sort = "emp_id"  ' Optionally sort the data.
End With
```

> 注意：如果你的 SELECT 语句包含 ORDER BY 子句，则无需使用 BindingSource 对数据进行排序。

## 绑定到 DataGridView

要将 DataGridView 绑定到你在代码中实例化的 DataSet，可以将网格的 DataSource 设置为 BindingSource。在设置好绑定源，如前例所示后，将网格的 DataSource 属性设置为新的 BindingSource 对象。

```
' Bind the grid.
EmployeeDataGridView.DataSource = ABindingSource
```

你可以使用一种方便的技术来设置网格的属性，例如选择和排序列以及修改列标题。在窗体设计器中，从数据源窗口拖动网格，这将设置所有数据绑定组件。使用智能标记和属性窗口按你想要的方式设置网格列。然后你可以从组件托盘中删除可视组件并编写代码来填充网格（或者你可以保留它们但不使用它们，而是在代码中绑定到数据层 DataSet）。

> 一点警告：如果删除 DataSet 和 BindingSource 组件，你将无法在设计器中修改 DataGridView 列。

## 将表数据绑定到列表框或组合框

对于列表框或组合框，你可以将控件的 DataSource 设置为 BindingSource 对象，并将 DisplayMember 设置为表字段之一。请注意，在以下代码中，你必须用引号指定现有字段的字段名。

```
' Bind a combo box.
With Emp_idComboBox
    .DataSource = ABindingSource
    .DisplayMember = "emp_id"
    .DataBindings.Add("text", ABindingSource, "emp_id", _
        False, DataSourceUpdateMode.Never)
End With
```

要绑定标签、文本框、组合框的 Text 属性以及日期时间选择器，你必须在代码中使用 DataBindings.Add 方法将字段从 DataSet 绑定。

## DataBindings.Add 方法—通用形式

```
Object.DataBindings.Add("property", DataSource, "FieldName")
```

重载格式：格式化数据字段：

```
Object.DataBindings.Add("property", DataSource, "FieldName", True,
    DataSourceUpdateMode.Never, Nothing, "FormatString")
```

请注意，属性和字段名必须用引号括起来，而数据源则不需要。此外，请注意属性名必须为小写；字段名不区分大小写。

如果需要格式化数据，请使用重载格式。你可以使用在 ToString 方法中使用的相同代码进行格式化，例如 "C" 表示货币，"d" 表示短日期。True 参数指定已启用格式化；DataSourceUpdateMode 参数指定每次分配新值时，无论来自数据库字段还是用户输入，都会进行格式化。Nothing 参数指定如果字段为空，则应允许其具有 Nothing 值。而 FormatString 是格式化代码。有关完整代码列表，请参阅帮助。

## DataBindings.Add 方法—示例

```
LastNameTextBox.DataBindings.Add("text", ABindingSource, "lname")
HireDateTextBox.DataBindings.Add("text", EmployeeBindingSource, "hire_date",
    True, DataSourceUpdateMode.Never, Nothing, "d")
```

以下是完整的 Form_Load 事件处理程序，它实例化数据层、检索 DataSet、设置 BindingSource 并绑定到窗体字段。

```
Private Sub EmployeeForm_Load(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles Me.Load
    ' Retrieve the data and bind the form's controls.
    Try
        ' Create an instance of the data-tier component.
        Dim EmployeeData As New PubsEmployeeData
```

```
' Retrieve the dataset from the data tier.
Dim ApuDataSet As PubsDataSet
ApuDataSet = EmployeeData.GetEmployeeDataset()

' Set up the binding source.
Dim ABindingSource As New BindingSource
With ABindingSource
    .DataSource = ApuDataSet
    .DataMember = "employee"
    .Sort = "emp_id"
End With

' Fill the combo box.
With Emp_idComboBox
    .DataSource = ABindingSource
    .DisplayMember = "emp_id"
    .DataBindings.Add("text", ABindingSource, "emp_id", _
        False, DataSourceUpdateMode.Never)
End With

' Bind the other controls.
FullNameTextBox.DataBindings.Add("text", _
    ABindingSource, "FullName")
Hire_dateDateTimePicker.DataBindings.Add("text", _
    ABindingSource, "hire_date")
Catch ex As Exception
    MessageBox.Show(ex.Message)
End Try
End Sub
```

## 从存储过程绑定数据

前面数据绑定的示例说明了使用表字段。如果使用存储过程，则必须用存储过程的名称代替表名。以下是前一个代码示例的绑定，但使用 GetEmployeeData 存储过程而不是 employee 表。

```
' Set up the binding source.
Dim ABindingSource As New BindingSource
With ABindingSource
    .DataSource = ApuDataSet
    .DataMember = "GetEmployeeData" ' Stored procedure name.
End With
```

请注意，在此示例中未设置 BindingSource 的 Sort 属性，因为 GetEmployeeData 存储过程包含一个 ORDER BY 子句来对数据进行排序。

## 创建数据层—逐步操作

以下逐步教程使用表示层和数据层重新创建 Employee 项目。

## 创建新项目

- STEP 1: 开始一个新的 Windows 应用程序项目。将项目命名为 `Ch03EmployeeTiers`。
- STEP 2: 将窗体命名为 `EmployeesForm` 并将 Text 属性更改为 `Employees`。

## 添加数据源

- STEP 1: 从数据源窗口添加 Pubs 数据库数据源。包含 employee 表中的 `emp_id`、`fname`、`lname` 和 `hire_date` 字段。
- STEP 2: 在 DataSet 设计器中，使用表达式 `fname + ' ' + lname`（不带外层双引号）向 employee 表添加一个名为 `FullName` 的新列。请注意，顺序与之前的示例相反。
- *Trouble?* 如果收到无法添加列的消息，请关闭并重新打开 DataSet 设计器并重复该步骤，这时应该可以正常工作。
- STEP 3: 在 DataSet 设计器中，右键单击 `employeeTableAdapter` 并选择 **Configure**。在 TableAdapter 配置向导中，选择 **Advanced Options**。
- STEP 4: 在高级选项对话框中，取消选中生成额外语句的复选框。三个复选框都应取消选中。单击 OK。在 TableAdapter 配置向导中单击 Finish。
- STEP 5: 在 DataSet 设计器中，修改每个字段的 Caption 属性，使其成为“用户友好”的字符串。
- STEP 6: 保存所有内容。

## 添加数据层类

你需要为数据层添加一个新类。虽然可以使用具有可视设计器的 Component 类，但在此示例中我们不需要可视设计器。

- STEP 1: 从 *Project* 菜单中选择 *Add Class*。 （替代方法：在解决方案资源管理器中右键单击项目名称并选择 *Add / Class*。）
- STEP 2: 将新类命名为 `PubsEmployeeData.vb`。

## 编写组件

STEP 1: 显示新类的代码。请注意，设计模板生成的行是

```
Public Class PubsEmployeeData

End Class
```

STEP 2: 编写类级变量。虽然这些变量在此程序中可以作为局部变量编写，但在未来的程序中你将需要类级变量来保存 DataSet 和 TableAdapter。

```
' Declare class-level variables.
Private AnEmployeeTableAdapter _
    As PubsDataSetTableAdapters.employeeTableAdapter
Private APubsDataSet As PubsDataSet
```
