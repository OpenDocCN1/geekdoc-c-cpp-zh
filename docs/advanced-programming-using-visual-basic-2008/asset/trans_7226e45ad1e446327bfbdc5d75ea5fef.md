

**图 4.15**

DataSet 设计器中的 jobs 和 employee 表。jobs 表是一对多关系中的“一”方。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_190_0.png)

右键单击关系连线，然后选择“编辑关系”。在“关系”对话框（图 4.16）中，可以查看和修改该关系。关系的默认名称相当晦涩：在此示例中为“FK__employee__job_id__1BFD2C07”。在编写任何引用该关系的代码之前，请将其更改为更有意义的名称，例如“EmployeeToJobsRelation”。

**图 4.16**

将关系的名称更改为比默认名称更有意义的名称，例如 EmployeeToJobsRelation。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_190_1.png)

## 引用记录和字段

当使用 DataSet 中的数据时，通常需要引用选定记录中的单个字段。实际数据值保存在 DataRow 对象中。DataSet 中的每个 Table 对象都有一个由 DataRow 对象组成的 DataRows 集合（图 4.17）。

**图 4.17**

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_191_0.png)

Table 对象具有一个 DataRows 集合，该集合由表中每条记录对应的一个 DataRow 对象组成。

数据值保存在 DataRow.Item 属性中。可以通过索引位置（第一个字段的索引为 0）、用引号括起的字段名或使用感叹号（称为“bang”）来引用单个字段。例如，可以使用以下三条语句中的任意一条来检索这个 employee DataRow 对象的 fname 字段：

```
FirstNameString = EmployeeDataRow.Item(1).ToString
FirstNameString = EmployeeDataRow.Item("fname").ToString
FirstNameString = EmployeeDataRow!fname.ToString
```

除非你想查找记录中每个字段的索引位置，否则你会发现使用字段名更方便。你可以在 DataSet 设计器和“数据源”窗口中查看字段名。

## 检索相关的父行

以下示例允许用户从绑定的组合框中选择一个员工姓名，然后显示 employee 表中的雇用日期和 jobs 表中的职位描述（图 4.18）。数据字段显示在未绑定的文本框中；也就是说，文本框没有数据绑定。每个字段都被赋值给文本框的 Text 属性。

> 注意：这个应用程序使用绑定控件也可以轻松编写。本练习的重点是学习使用未绑定控件并引用单个数据库字段，因为许多专业应用程序都采用这种方法。

**图 4.18**

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_191_1.png)

程序根据选定的员工姓名检索正确的 employee DataRow 和匹配的 jobs 父 DataRow，以显示职位描述。

当您允许用户从绑定的组合框中选择值时，可以在 SelectionChangeCommitted 事件处理程序中编写代码来检索数据。该过程基本上有三个步骤：

1. 在 employee 表中查找与组合框选择匹配的行。
2. 使用 GetParentRow 方法从 jobs 表中检索匹配的行。
3. 检索特定的数据项并将其赋值给文本框的 Text 属性。

> **提示**
> 在 Class 语句之前添加 Imports System.Data；然后就可以在代码中省略所有数据对象声明上的“Data.”命名空间。

### 查找 Employee（子）行

为 employee 表声明一个 DataRow 对象，并为 jobs 表声明另一个 DataRow 对象。

```
Dim EmployeeDataRow As DataRow
Dim JobDataRow As DataRow
```

使用 employee 组合框中的 SelectedValue 查找完整的员工记录。DataSet 中的每个表都包含一个按键字段查找记录的方法。由于 employee 表中的主键是 emp_id，因此会自动为表对象生成 FindByemp_id 方法。
查找的格式为

```
DataRow = DataSetName.TableName.FindByMethod(PrimaryKeyValue)
```

如果将组合框的 ValueMember 属性设置为 emp_id，则可以使用以下代码通过其键字段检索正确的员工记录。

```
' Save the Employee ID for the selected employee.
EmployeeIDString = EmployeeComboBox.SelectedValue.ToString
' Find the data row for this employee.
EmployeeDataRow = PubsDataSet.employee.FindByemp_id(EmployeeIDString)
```

### 获取父行

既然您已经知道 employee（子）表中与组合框条目匹配的行，则必须从 jobs 表中获取父行。

```
' Find the matching row from the parent (jobs) table.
JobDataRow = EmployeeDataRow.GetParentRow("EmployeeToJobsRelation")
```

请注意，GetParentRow 方法参数中的“EmployeeToJobsRelation”是我们在图 4.16 中讨论设置的关系名称。

### 检索特定字段

最后一步是从数据行中获取字段。

```
' Display a field from the matching row.
JobTitleTextBox.Text = JobDataRow!job_desc.ToString
```

### 完整的查找父行程序

```
'Program: Ch04FindParentUnbound
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: Allow the user to select the employee name from a combo box
' and display the corresponding hire date from the same table
' and the job description from the jobs table.
' Demonstrates finding a parent row for a selected child row,
' referring to individual fields in a DataRow object, and
' assigning database fields to unbound controls.

Imports System.Data

Public Class EmployeeForm

Private Sub EmployeeForm_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles MyBase.Load
' Fill the DataSet.
JobsTableAdapter.Fill(PubsDataSet.jobs)
EmployeeTableAdapter.Fill(PubsDataSet.employee)
End Sub

Private Sub EmployeeComboBox_SelectionChangeCommitted(ByVal sender As Object, _
ByVal e As System.EventArgs) _
Handles EmployeeComboBox.SelectionChangeCommitted
' Find and display the selected record.
Dim EmployeeIDString As String
Dim EmployeeDataRow As DataRow
Dim JobDataRow As DataRow

' Find the data row for the selected name.
EmployeeIDString = EmployeeComboBox.SelectedValue.ToString
EmployeeDataRow = PubsDataSet.employee.FindByemp_id( _
EmployeeIDString)

' Display a field from the selected row.
HireDateTextBox.Text = EmployeeDataRow.hire_date.ToString
' Use this alternate statement to format the date.
HireDateTextBox.Text = Convert.ToDateTime( _
EmployeeDataRow.hire_date).ToString("d")

' Find the matching row from the parent (jobs) table.
JobDataRow = EmployeeDataRow.GetParentRow( _
"EmployeeToJobsRelation")

' Display a field from the matching row.
JobTitleTextBox.Text = JobDataRow.job_desc.ToString
End Sub
End Class
```

## 检索相关的子行

检索相关子行与检索相关父行类似。主要区别在于 GetChildRows 方法返回一个行数组，而不是单一行。在此前一个程序的变体中，用户从组合框中选择一个职位。程序检索该职位对应的正确数据行，并在列表框中显示匹配的员工数组（图 4.19）。请注意，此程序中的 DataSet 和关系与前面示例完全相同。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_194_0.png)

**图 4.19**

当用户选择职位（父行）时，程序检索并显示匹配的员工（子行）记录数组。

### 完整的查找子行程序

```
'Program: Ch04FindChildrenUnbound
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: Allow the user to select the job description from a
'combo box and display the corresponding employees
'(child rows) from the employee table.
'Demonstrates finding child rows for a selected parent row,
'referring to individual fields in a DataRow object, and
'assigning database fields to unbound controls.
'
Imports System.Data

Public Class EmployeeForm

Private Sub EmployeeForm_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles MyBase.Load
'This line of code loads data into the 'PubsDataSet.jobs' table.
Me.JobsTableAdapter.Fill(Me.PubsDataSet.jobs)
'This line of code loads data into the 'PubsDataSet.employee' table.
Me.EmployeeTableAdapter.Fill(Me.PubsDataSet.employee)
End Sub

Private Sub JobComboBox_SelectionChangeCommitted(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles JobComboBox.SelectionChangeCommitted
'Find and display employees for the selected job.

Dim JobIDShort As Short
Dim JobDataRow As DataRow
Dim EmployeeDataRow As DataRow
Dim EmployeeDataRows As DataRow()

Try
'Get the job_id of the selected job.
JobIDShort = Convert.ToInt16(JobComboBox.SelectedValue)
'Find the row from the job table for the selected job_id.
JobDataRow = PubsDataSet.jobs.FindByjob_id(JobIDShort)
```

