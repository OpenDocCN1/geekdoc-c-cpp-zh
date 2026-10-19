

**图 12-33：使用姓氏筛选员工记录的代码**

```
37    private void btnFilterByLastName_Click(object sender, EventArgs e)
38    {
39        employeeBindingSource.Filter = "LastName = '" + txtLastName.Text + "'";
40        // Or, use the wildcard character "*" to specify incomplete strings
41        employeeBindingSource.Filter = "LastName LIKE '" + txtLastName.Text + "*'";
42    }
```

步骤2-10：运行窗体。在文本框中输入“Hope”并单击按钮。如导航栏所示（共2条中的第1条），窗体上只有姓氏为Hope的两条记录可用。

接下来，输入“M”以显示所有姓氏以“M”开头的员工。验证结果。

## 使用从组合框中选择的姓氏筛选记录

与其在文本框中输入姓氏，不如从所有有效的不重复姓氏列表中选择一个姓氏，这样会更简单。你可以通过将 Data Source 设置为 employeeBindingSource、将 Display Member 设置为 LastName，在组合框中显示所有姓氏。但是，如果有多个记录具有相同的姓氏，这将多次显示同一姓氏。因此，我们将创建一个名为 LastNames 的新数据表，其中仅包含不重复的姓氏，没有重复的名称。

### 添加新数据表及对应的表适配器

若要在数据集中添加新数据表，需要执行与添加数据源时相同的许多步骤。创建数据表的同时也会为该表创建表适配器。

步骤2-11：在解决方案资源管理器中双击文件 HRDataSet.xsd 以打开数据集窗口。你将看到 Employee 数据表及其表适配器。

步骤2-12：在窗口中的任意位置单击右键，然后选择“添加”、“TableAdapter”（而不是“Data Table”）。系统将要求你选择连接。由于你使用的是同一连接，请单击“下一步”。系统将要求你选择命令类型。

步骤2-13：保留默认选项“使用 SQL 语句”。单击“下一步”。系统将要求你输入 SQL 语句。

步骤2-14：单击“查询生成器”而不是手动输入查询。在“添加表”窗口中选择 Employee 表，单击“添加”。关闭“添加表”窗口。

步骤2-15：勾选 LastName 字段，单击“确定”。你将看到以下用于选择姓氏的 SQL：

```
SELECT    LastName
FROM      Employee
```

步骤2-16：通过在 LastName 前插入关键字 DISTINCT 来修改 SQL，如下所示：

```
SELECT    DISTINCT LastName
FROM      Employee
```

步骤2-17：单击“高级选项”。取消勾选“生成 Insert、Update 和 Delete 语句”复选框，因为 LastNames 数据表仅用于显示数据。单击“确定”。

步骤2-18：确保已勾选“填充数据表”。单击“下一步”。单击“完成”。你将看到名为 DataTable1 的新数据表。

**图 12-37：筛选员工记录的代码**

```
44  private void cboLastNames_SelectionChangeCommitted(object sender, EventArgs e)
45  {
46      employeeBindingSource.Filter = "LastName = '" + cboLastNames.SelectedValue + "'";
47  }
```

请注意，应使用组合框的 SelectedValue（而不是 Text 属性），该值由 ValueMember 属性指定的字段值提供。在引发此事件时，Text 属性尚未更新，原因是此事件在 SelectedIndexChanged 事件之前引发；因此，你不能在此事件处理程序中使用 Text 属性。

步骤2-24：为 cboLastNames 创建 SelectionChangeCommitted 事件处理程序，并添加图 12-37 中的代码。运行窗体并测试代码。

### 取消筛选

若要取消使用 BindingSource.Filter 属性指定的筛选，请将 Filter 设置为空字符串。

步骤2-25：添加一个名为 btnCancelFilter 的按钮，并将图 12-38 中的代码添加到其 Click 事件处理程序。运行窗体并测试代码。

**图 12-38：取消筛选的代码**

```
48
49  private void btnCancelFilter_Click(object sender, EventArgs e)
50  {
51      employeeBindingSource.Filter = "";
52  }
```

是时候练习了！完成练习 12-2。

## 从一个表中选择列表以筛选另一个表

假设你要从组合框中选择部门编号，并筛选员工记录，以便只查看该部门的员工。HR 数据库包含另一个名为 department 的表，如图 12-39 所示。

**图 12-39：部门表**

| 部门编号 | 部门名称 | 部门电话 |
|---|---|---|
| 1 | 会计 | 920-424-1414 |
| 2 | 财务 | 920-424-3377 |
| 3 | 市场营销 | 920-424-2442 |
| 4 | 采购 | 920-424-0405 |
| 5 | 人力资源 | 920-424-1166 |
| 6 | 信息技术 | 920-424-3020 |

可通过修改 SQL 从 Employee 表获取用于在组合框中显示的不重复部门编号列表，也可以从 department 表获取。由于 Employee 表远大于 department 表，从 department 表获取此类列表效率更高。从 department 表获取部门编号还使你可以选择在组合框中显示部门名称，同时使用部门编号来筛选记录。

若要获取部门编号（以及需要的部门名称），你需要先使用与创建 LastNames 数据表相同的步骤，为 Department 表创建数据表和表适配器。

是时候练习了！完成练习 12-3。

### 复习题

12.9 来自名为 Employee 的表的数据以详细信息视图显示在窗体上的 TextBox 中。窗体上的控件是通过将数据表拖放到窗体上创建的。

执行以下语句会对用户在窗体上看到的记录集产生什么影响？

```
employeeBindingSource.Filter = "CountryId = 22";
```

执行上述语句会对内存中 Employee 数据表存储的记录产生什么影响？

## 12.8 使用表适配器选择记录

在上一节中，你使用绑定源的 Filter 属性选择记录，该属性控制数据表与窗体之间传输的内容。另一种选择记录的方法是使用表适配器更改其用于将数据从数据库传输到数据集的 SQL 语言。这与使用绑定源有根本区别。

### 绑定源与表适配器选择记录的对比

当使用绑定源筛选记录时，通常会将表（或多个表）中的整个数据从数据库加载到内存中的数据表中。绑定源用于帮助用户选择要处理的不同数据组。数据加载到数据表后，对数据库所做的任何更改都不会反映在用户看到的数据中。因此，用户可能看不到最新数据。此外，大型表会占用大量内存。将整个表加载到内存中，然后使用绑定源筛选记录的一个好处是，数据库只需在开始时访问一次，从而减少网络流量。

当使用表适配器时，每次用户需要一组数据，都会从数据库加载到数据表中并显示在窗体上。因此，每次加载一组数据时，都会包含最新的更改。由于数据表中仅保存选定的记录，内存占用较低。这也意味着每次用户请求一组记录时都会访问数据库。

接下来，我们来看如何使用表适配器选择记录。

步骤3-5：注释掉 Load 事件处理程序中使用标准 Fill 方法的语句，如图 12-42 所示。将图 12-42 中的代码添加到按钮的 Click 事件处理程序。

**图 12-42：EmployeeSearch_ParmQry 窗体的 Load 事件处理程序**

```
28  private void EmployeeSearch_ParmQry_Load(object sender, EventArgs e)
29  {
30      // TODO: This line of code loads data into the 'hRDataSet.Employee' table.
31      //this.employeeTableAdapter.Fill(this.hRDataSet.Employee);
32  }
33  private void btnSelectRecords_Click(object sender, EventArgs e)
34  {
35      employeeTableAdapter.FillByLastName(hRDataSet.Employee, txtLastName.Text);
36  }
```

步骤3-6：运行窗体并测试代码。

步骤3-7：为了给用户提供显示全部记录的选项，添加一个按钮 btnAllRecords，其标题为“Display All”。添加使用标准查询的代码，如图 12-43 所示。运行窗体并测试代码。

**图 12-43：显示全部记录的标准 Fill 方法**

```
37
38  private void btnAllRecords_Click(object sender, EventArgs e)
39  {
40      this.employeeTableAdapter.Fill(this.hRDataSet.Employee);
41  }
```

是时候练习了！完成练习 12-4。

### 复习题

12.10 来自名为 Employee 的表的数据以详细信息视图显示在窗体上的 TextBox 中。窗体上的控件是通过将数据表拖放到窗体上创建的。使用以下 SQL 创建了一个名为 FillByLastName 的参数查询：

```
SELECT EmpId, LastName, FirstName, DateOfBirth, Phone, DeptNo, CountryId, Salary, FullTime
FROM dbo.Employee
WHERE DeptNo = @DeptNo
```

执行以下语句会对 Employee 数据表产生什么影响？`employeeTableAdapter.FillByLastName(hRDataSet.Employee, 11)`

