
例如，前一个示例中对 `executeUpdate` 的调用返回价格下调了 $5.00 的行数。

`executeUpdate` 方法可以执行诸如 `INSERT`、`UPDATE` 和 `DELETE` 之类的操作，也可以执行诸如 `CREATE TABLE` 和 `DROP TABLE` 之类的数据定义语句。但是，需要改用 `executeQuery` 方法来执行 `SELECT` 查询。此外还有一个通用的 `execute` 语句，可用于执行任意 SQL 语句。它通常仅用于用户交互提供的查询。

执行查询时，你关心的是结果。`executeQuery` 方法返回一个 `ResultSet` 类型的对象，你可以用它逐行遍历结果。

```
ResultSet rs = stat.executeQuery("SELECT * FROM Books");
```

分析结果集的基本循环如下所示：

```
while (rs.next())
{
    *look at a row of the result set*
}
```

> **注意：** `ResultSet` 接口的迭代协议与 `java.util.Iterator` 接口的迭代协议有细微差别。在这里，迭代器被初始化为指向第一行之前的位置。必须调用一次 `next` 方法将迭代器移动到第一行。此外，没有 `hasNext` 方法；应持续调用 `next`，直到它返回 false。

结果集中行的顺序完全是任意的。除非使用 `ORDER BY` 子句专门对结果排序，否则不应赋予行顺序任何意义。

检查单独一行时，你会想了解各字段的内容。大量访问器方法可为你提供这些信息。

```
String isbn = rs.getString(1);
double price = rs.getDouble("Price");
```

有适用于各种类型的访问器，例如 `getString` 和 `getDouble`。每个访问器都有两种形式：一种接受数值参数，另一种接受字符串参数。提供数值参数时，你引用的是具有该编号的列。例如，`rs.getString(1)` 返回当前行中第一列的值。

> **注意：** 与数组索引不同，数据库列号从 1 开始。

提供字符串参数时，你引用的是结果集中具有该名称的列。例如，`rs.getDouble("Price")` 返回标签为 Price 的列的值。使用数值参数效率稍高，但字符串参数使代码更易于阅读和维护。

当方法类型与列类型不匹配时，每个 get 方法都会进行合理的类型转换。例如，调用 `rs.getString("Price")` 会将 Price 列的浮点值转换为字符串。

| java.sql.Connection 1.1 | |
|---|---|
| `Statement createStatement()` | 创建一个 Statement 对象，可用于执行不带参数的 SQL 查询和更新。 |
| `void close()` | 立即关闭当前连接及其创建的 JDBC 资源。 |

| java.sql.Statement 1.1 | |
|---|---|
| `ResultSet executeQuery(String sqlQuery)` | 执行字符串中给定的 SQL 语句，并返回一个 ResultSet 对象以查看查询结果。 |
| `int executeUpdate(String sqlStatement)`<br>`long executeLargeUpdate(String sqlStatement)` 8 | 执行字符串指定的 SQL INSERT、UPDATE 或 DELETE 语句。还执行数据定义语言（DDL）语句，例如 CREATE TABLE。返回受影响的行数；对于没有更新计数的语句，返回 0。 |
| `boolean execute(String sqlStatement)` | 执行字符串指定的 SQL 语句。可能会产生多个结果集和更新计数。如果第一个结果是结果集，则返回 true，否则返回 false。调用 getResultSet 或 getUpdateCount 获取第一个结果。有关处理多个结果的详细信息，请参见第 321 页的 5.5.4 节“多个结果”。 |

### java.sql.Statement 1.1（续）

- `ResultSet getResultSet()`  
  返回前一条查询语句的结果集；如果前一条语句没有结果集，则返回 null。每条已执行的语句只调用此方法一次。
- `int getUpdateCount()`
- `long getLargeUpdateCount()` 8  
  返回前一条更新语句影响的行数；如果前一条语句是没有更新计数的语句，则返回 -1。每条已执行的语句只调用此方法一次。
- `void close()`  
  关闭此语句对象及其关联的结果集。
- `boolean isClosed()` 6  
  如果此语句已关闭，则返回 true。
- `void closeOnCompletion()` 7  
  使此语句在其所有结果集都关闭后自动关闭。

### java.sql.ResultSet 1.1

- `boolean next()`  
  使结果集中的当前行向前移动一行。最后一行之后返回 false。注意，必须调用此方法才能前进到第一行。
- `Xxx getXxx(int columnNumber)`
- `Xxx getXxx(String columnLabel)`  
  （Xxx 是诸如 int、double、String、Date 等类型。）
- `<T> T getObject(int columnIndex, Class<T> type)` 7
- `<T> T getObject(String columnLabel, Class<T> type)` 7
- `void updateObject(int columnIndex, Object x, SQLType targetSqlType)` 8
- `void updateObject(String columnLabel, Object x, SQLType targetSqlType)` 8  
  返回或更新具有给定列索引或标签的列的值，并将其转换为指定类型。列标签是 SQL AS 子句中指定的标签；如果未使用 AS，则为列名。
- `int findColumn(String columnName)`  
  给出与列名关联的列索引。

| java.sql.ResultSet 1.1（续） | |
|---|---|
| `void close()` | 立即关闭当前结果集。 |
| `boolean isClosed()` 6 | 如果此结果集已关闭，则返回 true。 |

### 5.4.2 管理连接、语句和结果集

每个 `Connection` 对象可以创建一个或多个 `Statement` 对象。你可以将同一个 `Statement` 对象用于多个不相关的命令和查询。但是，一个 `Statement` *至多有一个*打开的结果集。如果发出多个查询并同时分析其结果，则需要多个 `Statement` 对象。

但请注意，每个连接的语句数量是有限制的。使用 `DatabaseMetaData` 接口的 `getMaxStatements` 方法查明 JDBC 驱动程序支持的并发打开语句数。

在实践中，可能不必为多个并发结果集费心。如果这些结果集相关，应能发出一个组合查询并分析单个结果。让数据库合并查询比让 Java 程序遍历多个结果集高效得多。

在发出新查询或对 `Statement` 对象执行更新之前，务必完成对任何结果集的处理。先前查询的结果集会自动关闭。

使用完 `ResultSet`、`Statement` 或 `Connection` 后，最好立即调用 `close` 方法。这些对象使用大型数据结构，会占用数据库服务器的有限资源。

`Statement` 对象的 `close` 方法会关闭任何关联的结果集。同样，`Connection` 类的 `close` 方法会关闭该连接的所有语句。

反之，可以在 `Statement` 上调用 `closeOnCompletion` 方法，这样一旦其所有结果集都已关闭，它就会自动关闭。

如果连接是短生命周期的，则不必担心关闭语句和结果集。为确保连接对象不可能保持打开状态，请使用 try-with-resources 语句：

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_327_0.png)

**图 5.5** SQL 异常类型

当从数据库读取的数据被意外截断时，会使用 SQLWarning 的 DataTruncation 子类。如果数据截断发生在更新语句中，则会抛出 DataTruncation 异常。

### java.sql.SQLException 1.1

- `SQLException getNextException()`  
  获取链接到此异常的下一个 SQL 异常；在链末尾返回 `null`。
- `Iterator<Throwable> iterator()` 6  
  获取一个迭代器，用于生成链式 SQL 异常及其原因。
- `String getSQLState()`  
  获取“SQL 状态”——一种标准化错误代码。
- `int getErrorCode()`  
  获取供应商特定的错误代码。
