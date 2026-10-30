

- STEP 3: 在数据层类中编写 GetEmployeeDataset 方法。注意此方法返回一个 DataSet 对象。

```vb
Public Function GetEmployeeDataset() As PubsDataSet
    ' Fill and return the DataSet.

    Try
        ' Instantiate the TableAdapter and DataSet.
        AnEmployeeTableAdapter = New PubsDataSetTableAdapters.employeeTableAdapter
        APubsDataSet = New PubsDataSet
        ' Fill the DataSet.
        AnEmployeeTableAdapter.Fill(APubsDataSet.employee)
        ' Return the DataSet.
        Return APubsDataSet
    Catch ex As Exception
        Throw ex
    End Try
End Function
```

- STEP 4: 在类的顶部编写注释。
- STEP 5: 保存所有内容。

## Add Controls to the Form

虽然你可以通过从工具箱添加单个控件来创建用户界面，但我们将采用捷径。我们将使用数据源窗口的拖放功能，然后删除多余的组件。

- STEP 1: 在设计器中显示窗体。
- STEP 2: 在数据源窗口中，将 employee 表设置为 Details。
- STEP 3: 将 emp_id 字段更改为 ComboBox。
- STEP 4: 将表拖到窗体上。
- STEP 5: 删除组件托盘中的所有对象。我们不能使用这些组件，因为我们将从数据层获取数据。
- STEP 6: 显示窗体的代码并删除自动生成的代码。所有错误消息都应消失。
- STEP 7: 删除名字和姓氏字段的文本框和标识标签。保留员工 ID、全名和雇佣日期的控件。
- STEP 8: 重新排列控件并根据需要更改标签为员工 ID、姓名和雇佣日期。图 3.29 显示了此时的窗体。

**Figure 3.29.** Rearrange the controls for the step-by-step exercise.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_162_0.png)

## Feedback 3.4

- 1. 在多层项目中，你将绑定源和 TableAdapter 放置在哪里？
- 2. 用于从 TableAdapter 填充 DataSet 的类中的函数需要什么返回类型？
- 3. 编写代码将一个名为 CustomersDataSet 的 DataSet 的名字标签绑定。窗体使用 CustomersBindingSource。显示来自 Customer 表的 First-Name 字段。

## Your Hands-On Programming Example

创建一个多层项目，使用存储过程从 Pubs 数据库的 employee 表中获取数据。在存储过程中使用 ORDER BY 子句按姓氏顺序对数据进行排序。以字母顺序在组合框中显示完整的员工姓名（姓氏、名字和中间名首字母）。除组合框外，不显示名字和姓氏字段。在文本框中显示所选记录的其余字段，并附带有意义的标识标签。不要包含导航工具栏。包含一个 File / Exit 菜单项以终止程序。

## Planning the Project

草拟一个窗体草图（图 3.30），让用户签字确认其满足需求。

**Figure 3.30.** A planning sketch for the hands-on programming example.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_164_0.png)

### Plan the Objects, Properties, and Methods

规划两个层。确定窗体及其控件以及数据层组件的对象和属性设置。图 3.31 显示了两个层中的组件图。

### Presentation Tier

| Object | Property | Setting |
| --- | --- | --- |
| EmployeeForm | Name | EmployeeForm |
|  | Text | Employees |
| FullNameComboBox | Name | FullNameComboBox |
| Text boxes for all database fields (including Hire Date) |  |  |

| Event Handlers/Methods | Actions—Pseudocode |
| --- | --- |
| ExitToolStripMenuItem_Click | Exit the project. |
| Form_Load | Instantiate the data tier.<br>Retrieve the DataSet.<br>Bind the controls.<br>Format the date in its binding. |

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_165_0.png)

### Data Tier

| Methods | Actions—Pseudocode |
| --- | --- |
| GetEmployeeData | Instantiate the DataSet and TableAdapter.<br>Fill the DataSet.<br>Return the DataSet. |

### Write the Project

按照图 3.30 中的草图创建窗体。图 3.32 显示了完成的窗体。

- 将 Pubs.mdf 的副本添加到项目中，并在 Server Explorer 中使用该文件设置连接。然后创建存储过程以检索和排序数据并创建新的连接的 FullName 字段。
- 使用数据源窗口设置数据源和 DataSet。
- 创建数据层组件，根据伪代码编写方法。
- 根据计划设置用户界面。
- 编写窗体的代码。按照伪代码编写每个事件处理程序。
- 完成代码后，多次测试操作。将屏幕输出与数据表进行比较，以确保你正在显示正确的信息。

**Figure 3.32.** The completed form for the hands-on programming example.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_166_0.png)

## The Project Coding Solution

### The Form

```vb
'Project:      Ch03HandsOn
'Programmer:   Bradley/Millspaugh
'Date:         June 2009
'Class:        EmployeeForm
'Description:  Presentation tier to display the employee information.

Public Class EmployeeForm
    Private Sub EmployeeForm_Load(ByVal sender As System.Object, _
        ByVal e As System.EventArgs) Handles MyBase.Load
        ' Retrieve data from data tier and bind controls.
        Try
            Dim EmployeeData As New EmployeeDataTier
            Dim EmployeeDataSet As PubsDataSet

            EmployeeDataSet = EmployeeData.GetEmployeeData()

            ' Set up the BindingSource.
            Dim ABindingSource As New BindingSource
            With ABindingSource
                .DataSource = EmployeeDataSet
                .DataMember = "getEmployees"
            End With

            ' Bind the controls.
            With FullNameComboBox
                .DataSource = ABindingSource
                .DisplayMember = "fullName"
                .DataBindings.Add("text", ABindingSource, "FullName", _
                    False, DataSourceUpdateMode.Never)
            End With
            Emp_idTextBox.DataBindings.Add("text", _
                ABindingSource, "emp_id")
            Job_idTextBox.DataBindings.Add("text", _
                ABindingSource, "job_id")
            Job_lvlTextBox.DataBindings.Add("text", _
                ABindingSource, "job_lvl")
            Pub_idTextBox.DataBindings.Add("text", _
                ABindingSource, "pub_id")
            Hire_dateTextBox.DataBindings.Add("text", _
                ABindingSource, "hire_date", True, DataSourceUpdateMode.OnValidation, Nothing, "d")
        Catch ex As Exception
            MessageBox.Show(ex.Message)
        End Try
    End Sub

    Private Sub ExitToolStripMenuItem_Click(ByVal sender As System.Object, _
        ByVal e As System.EventArgs) Handles ExitToolStripMenuItem.Click
        ' End the program.
        Me.Close()
    End Sub
End Class
```

### The Data-Tier Component

```vb
'Project:      Ch03HandsOn
'Programmer:   Bradley/Millspaugh
'Date:         June 2009
'Class:        EmployeeDataTier
'Description:  The data-tier component for the Ch03HandsOn program.
'              Includes the code for the database access.

Public Class EmployeeDataTier
    ' Class-level declarations.
    Private EmployeeDataSet As PubsDataSet
    Private EmployeeTableAdapter As PubsDataSetTableAdapters.getEmployeesTableAdapter

    Public Function GetEmployeeData() As PubsDataSet
        ' Fill and return the DataSet.

        EmployeeDataSet = New PubsDataSet
        EmployeeTableAdapter = New PubsDataSetTableAdapters.getEmployeesTableAdapter

        EmployeeTableAdapter.Fill(EmployeeDataSet.getEmployees)
        Return EmployeeDataSet
    End Function
End Class
```

### The Stored Procedure

```sql
CREATE PROCEDURE getEmployees
/*
Procedure to retrieve and sort the Employee table.
*/
AS
Select *, lname+',' +fname+ ' '+mInit as FullName
from Employee
order by lname
RETURN
```

## Summary

- 1. 数据可从多种来源获取，包括数据库、文件、电子邮件和电子表格。
- 2. ADO.NET 是在 VB 应用程序程序中引用数据的对象模型。
- 3. 数据库表包含行（记录）和列（字段）。
- 4. 主键唯一标识一条记录。当主键包含在第二个表中用于链接目的时，它在第二个表中称为外键。
- 5. 键入的 DataSet 可以包含多个表，以及关系和约束。DataSet 中的数据是从其来源文件断开连接的内存中的临时副本。
- 6. DataSet 对象具有 DataTable 集合，可容纳多个 DataTable 对象。每个 DataTable 具有 DataRow 集合、DataColumn 集合和 Constraints 集合。DataSet 还可以包含 DataRelation 对象。
- 7. TableAdapter 对象连接到数据库并处理 SQL 查询。
- 8. 用于数据库处理的组件包括 BindingSource、TableAdapter 和 DataSet 组件。
- 9. XML 是用于以文本格式存储和传输数据的行业标准，使用标识数据字段的标签。XML 文件还可能具有定义字段名称、数据类型和约束的架构文件。
- 10. 数据源窗口提供将数据源添加到项目并将表拖到窗体以创建数据绑定控件的能力。
- 11. SQL Server 2008 Express Edition，随 Visual Studio 一起提供，可用于对 SQL Server 数据库进行编程，并被视为 VB 中单用户数据库的“原生”数据库格式。
- 12. 通过将表名从数据源窗口拖到窗体，可以自动在 DataGridView 控件中显示数据。设置每个列的 HeaderText 属性以修改列标题。
- 13. DataSet 设计器是用于处理 DataSet 的可视工具。你可以在 DataSet 设计器中添加字段、表和关系，以及预览数据。
- 14. 在数据源窗口中，你可以选择每个数据库字段要使用的控件以及是否以网格或详细信息视图显示表。
- 15. 在 DataSet 设计器中，你可以为 DataSet 中的每个字段设置标题，该标题用于详细信息控件的标识标签。你还可以添加具有表达式的字段，该表达式可以是连接的字符串或计算值。
- 16. 允许用户访问数据的一种常见方法是显示一个列表框供用户选择字段。你必须设置列表的 DataSource 和 DisplayMember 属性以自动填充列表。

