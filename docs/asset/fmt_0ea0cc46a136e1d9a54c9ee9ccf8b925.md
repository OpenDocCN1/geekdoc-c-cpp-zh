
在前面的示例中，我们按 `OrderID` 对它们进行分组。

### DELETE 语句

SQL 中的 `DELETE` 语句用于从表中删除记录。您可以使用 `WHERE` 子句与 `DELETE` 语句一起根据某些条件删除记录，如以下 SQL 查询语句所示：

```
DELETE FROM Customers WHERE City NOT IN ('Boston', 'York')
```

在前面的示例中，我们正在删除 `Customers` 表中 `City` 字段不包含值 `Boston` 或 `York` 的记录。

### UPDATE 语句

您可以使用 `UPDATE` 语句更新数据库。虽然 `Visual C#` 自动更新数据库，但值得注意的是，您也可以使用 SQL 更新数据库。这在以下 SQL 查询语句中显示：

```
UPDATE Customers SET City = 'Boston' WHERE City = 'York'
```

在前面的示例中，我们将所有当前城市为 `York` 的记录的城市更改为 `Boston`。

### 连接表

您可以使用 SQL 将数据库中的两个或多个表连接起来。例如，您可以处理关系型数据库。现在，您希望使用 `Customers` 表中的客户联系人姓名和 `Orders` 表中他们订购的商品 ID 创建一个新的 `DataSet`。关联这两个表的字段是 `CustomerID`，因此您可以按如下代码片段所示设置 SQL 查询：

```
SELECT Customers.ContactName, Orders.OrderID FROM Customers, Orders WHERE Customers.CustomerID = Orders.CustomerID
```
