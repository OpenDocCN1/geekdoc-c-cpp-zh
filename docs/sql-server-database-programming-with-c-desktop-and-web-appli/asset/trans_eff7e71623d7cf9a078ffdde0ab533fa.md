

## ADO.NET 简介

| 属性名称 | 值类型 | 功能 |
| --- | --- | --- |
| FieldCount | 整数 | 获取当前行的列数。 |
| HasRows | 布尔值 | 获取一个值，指示 SqlDataReader 是否包含一个或多行。 |
| IsClosed | 布尔值 | 获取一个布尔值，指示 SqlDataReader 实例是否已关闭。 |
| Item(Int32) | 原生 | 根据列序数，获取指定列的原始格式值。 |
| Item(String) | 原生 | 根据列名，获取指定列的原始格式值。 |
| RecordsAffected | 整数 | 获取由执行 Transact-SQL 语句所更改、插入或删除的行数。 |
| VisibleFieldCount | 整数 | 获取 SqlDataReader 中未隐藏的字段数。 |

**图 3.24** SqlDataReader 类的属性。

| 方法 | 功能 |
| --- | --- |
| Close | 关闭指定的 SqlDataReader 对象。 |
| Dispose | 释放 DbDataReader 使用的资源。 |
| GetByte | 以字节形式获取指定列的值。 |
| GetName | 获取指定列的。 |
| GetString | 以字符串形式获取指定列的值。 |
| GetValue | 以原始格式获取指定列的值。 |
| IsDBNull | 获取一个布尔值，指示列是否包含空或缺失值。 |
| NextResult | 在读取批量 Transact-SQL 语句的结果时，将数据读取器移动到下一个结果。 |
| Read | 将 SqlDataReader 移动到下一记录。 |
| ToString | 返回表示当前对象的字符串。 |

**图 3.25** SqlDataReader 类的常用方法。

DataReader 类有超过50个方法。图 3.25 列出了 SqlDataReader 类最常用的方法。所有其他 Data 类都具有类似的方法。

当你运行 `ExecuteReader()` 方法从数据库检索行并将其分配给 DataReader 时，每个 DataReader 只能检索并持有一行。因此，如果你想从数据表中读取所有行，则应该使用循环来顺序地从数据库检索每行。

DataReader 对象提供了从数据库读取数据最高效的方法，每当你需要从头到尾从数据库读取数据以填充表单上的列表或填充数组或集合时，都应该使用它。它也可以用于填充 DataSet 或 DataTable。

图 3.6 显示了使用 SqlDataReader 对象从 Faculty 数据表连续检索所有记录（行）的示例代码，假设已经创建了名为 `sqlConnection` 的 Connection 对象。

下面解释了此代码的功能。

从部分开始，使用 SQL SELECT 语句字符串创建一个新的 `SqlCommand` 和 `SqlDataReader` 对象。

命令在部分 B 中初始化。在部分中，调用 `ExecuteReader()` 方法从 Faculty 数据表中检索数据并将结果分配给 `SqlDataReader` 对象。通过检查 `HasRows` 属性（参见图 3.24），可以判断是否收集了数据行。如果检索到有效行，则使用 `while()` 循环和 `for()` 循环通过 `Read()` 方法逐顺序读取所有行（参见图 3.25）。

```csharp
string cmdString = "SELECT name, office, title, cole FROM Faculty";
SqlCommand sqlCommand = new SqlCommand();
SqlDataReader sqlDataReader;
sqlCommand.Connection = sqlConnection;
sqlCommand.CommandType = CommandType.Text;
sqlCommand.CommandText = cmdString;
sqlDataReader = sqlCommand.ExecuteReader();
if (sqlDataReader.HasRows)
{
    while (sqlDataReader.Read())
    {
        for (int intindex = 0; intindex < sqlDataReader.FieldCount - 1; intindex++)
            FacultyLabel(intindex).Text = sqlDataReader.GetString(intindex);
    }
}
else
    MessageBox.Show("No matched found!");
sqlDataReader.Close();
SqlCommand.Dispose();
```

**图 3.26** 使用 SqlDataReader对象的对象的代码。

| 异常名称 | 功能 |
| --- | --- |
| IndexOutOfRangeException | 如果索引不存在于范围或集合内，则发生此异常。 |
| InvalidCastException | 如果你尝试将对象转换为不兼容的类型。 |
| InvalidOperationException | 如果方法对于对象的当前状态无效。 |
| NotSupportedException | 如果请求的操作不支持。 |

### 3.27 SqlDataReader 的常用方法

DataReader 类有超过50个方法。图 3.25 列出了 SqlDataReader 类最常用的方法。所有其他 Data 类都具有类似的方法。

## 78 使用 C# 进行 SQL Server 数据库编程

## ADO.NET 简介

