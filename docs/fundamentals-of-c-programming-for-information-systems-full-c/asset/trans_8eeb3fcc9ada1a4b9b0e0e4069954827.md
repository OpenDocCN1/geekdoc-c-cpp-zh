

例如，如果 Salary 需要在计算中使用，可以使用以下语句将其作为 Double 检索，即其在数据库表中的类型，如第 71 行所示：

```
double salary = drEmployee.GetDouble(2);
```

这种方法需要了解检索数据时字段的确切类型。

步骤 7-3：注释掉第 61 行，并添加图 12-69 中第 65 行的代码以使用序数显示 salary。运行表单以测试代码。

注释掉第 65 行，并添加使用 GetOrdinal 方法的第 67 行和第 68 行的代码。运行表单以测试代码。

注释掉第 67 行和第 68 行，并添加使用 GetDouble 方法的第 71 行和第 72 行的代码。取消注释第 74 行和第 75 行。运行表单以测试代码。

DataReader 还有其他方法和属性可帮助使用它。一些常用的方法/属性显示在表 12-1 中。

### 表 12-1：SqlDataReader 的方法和属性

| 方法/属性名称 | 描述 | 示例 |
|---|---|---|
| Close | 关闭 DataReader 对象 | drEmployee.Close() |
| Dispose | 释放使用的资源 | drEmployee.Dispose() |
| GetBoolean, GetDateTime, GetDecimal, GetDouble, GetFloat, GetInt32, GetString | 以其原始类型获取值 | drEmployee.GetString(0)<br>drEmployee.GetDouble(2) |
| GetOrdinal(String) | 获取序数 | drEmployee.GetOrdinal("EmpId") |
| GetSchemaTable | 返回包含字段属性的数据表 | drEmployee.GetSchemaTable() |
| GetValue | 以 object 获取值 | drEmployee.GetValue(0) |
| GetValues | 以对象数组形式获取行中的值 | object[] colValues = new object[10];<br>drEmployee.GetValues(colValues); |
| Read | 前进到下一行 | drEmployee.Read() |
| Properties |  |  |
| FieldCount | 获取列数 | int count = drEmployee.FieldCount; |
| HasRows | 指示 DataReader 是否包含任何行 | if (drEmployee.HasRows) |

## SqlCommand 的 ExecuteNonQuery 方法

前面的部分使用了 SqlCommand 的 ExecuteScalar 方法和 ExecuteReader 方法从表中检索数据。SqlCommand 有第三个方法 ExecuteNonQuery，用于执行不检索任何数据的查询，但可用于更新、插入和删除记录，以及执行创建表等其他数据库操作。对于更新、插入和删除，该方法返回受影响的记录数。对于大多数其他操作，返回值是 -1。

你将使用 ExecuteNonQuery 在用户将新工资输入到 TextBox txtSalary 中并单击 Employee_Reader1 表单上之前在图 12-65 中介绍的 Update Salary 按钮时更新工资。代码显示在图 12-70 中。

## 循环遍历多行

此应用程序涉及访问多个 DeptNo 和 Employee 数据行。这是通过在 while 循环中重复调用 DataReader 的 Read 方法来完成的，如图 12-72 所示。

### 图 12-72：使用 while 循环访问多行

```
while (drEmployee.Read() == true)
{
    (statements to access the row)
}
```

while 循环中的 Read 方法每次循环都会将读取器推进到下一行。当 DataReader 中没有更多行时，循环终止，这由 DataReader 返回的值 false 标识。

### 从 Department 表获取 DeptNo

与之前一样，你将使用 SqlCommand 对象和 SqlDataReader 对象检索 DeptNo。图 12-73 显示了将数据检索到 DataReader 中并将其添加到 ComboBox 的代码。

你将使用相同的 SqlCommand 对象 cmdEmployee 通过更改分配给 CommandText 属性的 SQL 来检索 Department 和 Employee 数据。

### 图 12-73：检索 DeptNo 并添加到 ComboBox

```
19  // Create a SqlCommand object
20  SqlCommand cmdEmployee = new SqlCommand();
21
22  private void Employee_Reader2_Load(object sender, EventArgs e)
23  {
24      // Create a Connection object and specify the connection string
25      cmdEmployee.Connection = new SqlConnection();
26      cmdEmployee.Connection.ConnectionString = @"Data Source = (LocalDB)\MSSQLLocalDB; AttachDbFilename = C:\VC\HR2.mdf";
28      // Add DeptNo’s from the Department table, to the ComboBox
29      cmdEmployee.CommandText = "SELECT DeptNo FROM Department"; // specify SQL
30      cmdEmployee.Connection.Open();
31      // Call the ExecuteReader method to execute the SQL.
32      SqlDataReader drEmployee = cmdEmployee.ExecuteReader();
33
34      while (drEmployee.Read() == true) // loop through the rows
35      {
36          cboDeptNo.Items.Add(drEmployee["DeptNo"]); // add DeptNo to the ComboBox
37      }
38      cmdEmployee.Connection.Close();
39  }
```

第 32 行执行 SQL，并创建包含多行、每行包含单个 DeptNo 的 DataReader drEmployee。

第 34 行的 while 循环重复处理 Read 方法以访问行。

第 36 行将每个 DeptNo 添加到 ComboBox。

步骤 7-5：打开表单 Employee_Reader2。添加图 12-73 中的缺失代码。运行表单。确保 ComboBox 显示 DeptNo。

## 在 ListView 中显示员工记录

在 ListView 中显示数据涉及以下步骤：

- 检索员工记录，并使用 while 循环访问每一行。
- 使用 GetValues 方法获取整个当前行，并将其存储在对象数组中。
- 将对象数组转换为 String 数组。
- 使用 String 数组创建 ListViewItem。
- 将 ListViewItem 添加到 ListView。

图 12-74 显示了实现这些步骤的代码。

### 图 12-74：在 ListView 中显示员工数据

```
41  private void cboDeptNo_SelectedIndexChanged(object sender, EventArgs e)
42  {
43      cmdEmployee.CommandText = "SELECT * FROM Employee WHERE DeptNo = "
44                          + cboDeptNo.SelectedItem;
45      cmdEmployee.Connection.Open();
46      SqlDataReader drEmployee = cmdEmployee.ExecuteReader();
47
48      // display data in a ListView by storing the current row in an array
49      lvwEmployee.Items.Clear();
50      while (drEmployee.Read() == true)  // loop through the rows
51      {
52          int colCount = drEmployee.FieldCount; // get number of columns
53          object[] colValuesObj = new object[colCount];  // create an object array
54
55          // Get values from the current row, and store in the array, colValuesObj
56          drEmployee.GetValues(colValuesObj);
57          // Convert objects to strings and store in the String array, colValues
58          String[] colValues = Array.ConvertAll(colValuesObj, element => element.ToString());
59
60          // Create a ListViewItem using the array, colValues
61          ListViewItem lviEmp = new ListViewItem(colValues);
62          lvwEmployee.Items.Add(lviEmp); // add the ListViewItem to ListView
63      }
64      cmdEmployee.Connection.Close();
65  }
```

让我们更详细地查看这些步骤。

### 检索员工记录，并使用 while 循环访问每一行

第 43–46 行检索所选 DeptNo 的员工记录，并像之前一样创建 DataReader。

第 50 行在 while 循环中使用 Read 方法访问行。

你也可以将整行存储到数组中，并从数组中访问各个列：

```
while (drEmployee.Read() == true) // loop through the rows
{
    int colCount = drEmployee.FieldCount; // get number of columns
    object[] colValuesObj = new object[colCount]; // create an object array

    // Get values from the current row, and store in the array, colValuesObj
    drEmployee.GetValues(colValuesObj);

    Int32 salaryOrdinal = drEmployee.GetOrdinal("Salary");
    double salary = (double) colValuesObj[salaryOrdinal];
    // (statements that use salary)
}
```

步骤 7-6：添加图 12-74 中的代码。运行表单以测试代码。

## 复习问题

- 12.23 DataReader 的功能是什么？
- 12.24 真或假：当你使用数据表和数据适配器从数据库表访问记录时，数据库表的连接会一直保持到数据表关闭为止。
- 12.25 真或假：DataReader 提供了在 SQL 语句检索的记录中向前和向后移动的有效方法。
- 12.26 SqlCommand 对象将用于执行检索员工工资的 SQL 语句，通过指定员工的 id。应使用 Command 对象的什么方法？
- 12.27 SqlCommand 对象将用于执行检索员工 id、姓名和电话号码的 SQL 语句，使用员工的 id。应使用 Command 对象的什么方法？
- 12.28 SqlCommand 对象将用于执行更新员工工资的 SQL 语句。应使用 Command 对象的什么方法？
- 12.29 SqlDataReader 的 Read 方法做什么？

