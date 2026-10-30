

```
FROM Dim_AccountManagers INNER JOIN Dim_Territory ON
Dim_AccountManagers.AccountManagerID =
Dim_Territory.AccountManagerID
```

## 外连接

外连接操作告诉 Access 从一个表中选择所有记录，并仅从第二个表中选择连接字段中具有匹配值的记录。外连接有两种类型：左连接和右连接。

左连接操作（有时称为外左连接）告诉 Access 选择第一个表中的所有记录，而不考虑是否存在匹配项；同时，仅选择第二个表中连接字段具有匹配值的记录。

此 SQL 语句选择 `Dim_AccountManagers` 表中的所有记录，以及 `Dim_Territory` 表中 `AccountManagerID` 字段的值存在于 `Dim_AccountManagers` 表中的记录：

```
SELECT Region, Market,
Dim_AccountManagers.AccountManagerID, FullName
FROM Dim_AccountManagers LEFT JOIN Dim_Territory ON
Dim_AccountManagers.AccountManagerID =
Dim_Territory.AccountManagerID
```

右连接操作（有时称为外右连接）告诉 Access 选择第二个表中的所有记录，而不考虑是否存在匹配项；同时，仅选择第一个表中连接字段具有匹配值的记录。

此 SQL 语句选择 `Dim_Territory` 表中的所有记录，以及 `Dim_AccountManagers` 表中 `AccountManagerID` 字段的值存在于 `Dim_Territory` 表中的记录：

```
SELECT Region, Market,
Dim_AccountManagers.AccountManagerID, FullName
FROM Dim_AccountManagers RIGHT JOIN Dim_Territory ON
Dim_AccountManagers.AccountManagerID =
Dim_Territory.AccountManagerID
```

提示

请注意，在前面的连接语句中，表名列在每个列名之前，两者之间用点号分隔（例如，`Dim_AccountManager.AccountManagerID`）。为使用多个表的查询编写 SQL 语句时，通常最好同时引用表名和字段名，以避免混淆和错误。Access 会自动为所有查询执行此操作。如果被引用的表或字段包含空格等特殊字符，则还需要使用方括号。

## 使用高级 SQL 语句实现更复杂的操作

你很快会发现，SQL 语言非常灵活，能够让你执行远超基本 `SELECT`、`FROM` 和 `WHERE` 语句的操作。在本节中，你将了解一些可以使用 SQL 完成的高级操作。

## 使用 Like 运算符扩展搜索范围

单独使用时，Like 运算符与等号（`=`）运算符没有区别。例如，下面两个 SQL 语句返回的记录数相同：

```
SELECT AccountManagerID, [Last Name], [First Name]
FROM Dim_AccountManagers
WHERE [Last Name] = "Winston"
```

```
SELECT AccountManagerID, [Last Name], [First Name]
FROM Dim_AccountManagers
WHERE [Last Name] Like "Winston"
```

Like 运算符通常与通配符结合使用，以扩大搜索范围，使其包含所有符合某种模式的记录。Access 中有效的通配符如下：

- `*`：星号表示任意数量和类型的字符。
- `?`：问号表示任意单个字符。
- `#`：井号表示任意单个数字。
- `[]`：方括号允许向 Like 运算符传递单个字符或一组字符。凡是与方括号内字符值匹配的值，都会包含在结果中。
- `[!]`：带有感叹号的方括号允许向 Like 运算符传递单个字符或一组字符。凡是与感叹号后面的字符值匹配的值，都会从结果中排除。

表 14.1 列出了一些使用 Like 运算符从同一表列中选择不同记录的 SQL 语句示例。

## 表 14.1 使用 Like 运算符的选择方法

| 使用的通配符 | SQL 语句示例 | 结果 |
|---|---|---|
| `*` | SELECT Field1 FROM Table1 WHERE Field1 Like "A*" | 选择 Field1 以字母 A 开头的所有记录 |
| `*` | SELECT Field1 FROM Table1 WHERE Field1 Like "*A*" | 选择 Field1 包含字母 A 的所有记录 |
| `?` | SELECT Field1 FROM Table1 WHERE Field1 Like "???" | 选择 Field1 长度为三个字符的所有记录 |
| `?` | SELECT Field1 FROM Table1 WHERE Field1 Like "B??" | 选择 Field1 为以 B 开头的三个字母字符串的所有记录 |
| `#` | SELECT Field1 FROM Table1 WHERE Field1 Like "###" | 选择 Field1 为恰好三位数字的所有记录 |
| `#` | SELECT Field1 FROM Table1 WHERE Field1 Like "#A#" | 选择 Field1 的值为三个字符，且以 A 开头、包含一个数字并以 A 结尾的所有记录 |
| `#, *` | SELECT Field1 FROM Table1 WHERE Field1 Like "A#*" | 选择 Field1 以 A 和任意数字开头的所有记录 |
| `[], *` | SELECT Field1 FROM Table1 WHERE Field1 Like "*[$%!/*]/*" | 选择 Field1 包含 SQL 语句中所示任意一个特殊字符的所有记录 |
| `[!], *` | SELECT Field1 FROM Table1 WHERE Field1 Like "*[!a-z]*" | 选择 Field1 的值不是文本值，而是数字值或类似 @ 符号的特殊字符的所有记录 |
| `[!], *` | SELECT Field1 FROM Table1 WHERE Field1 Like "*[!0-9]*" | 选择 Field1 的值不是数字值，而是文本值或类似 @ 符号的特殊字符的所有记录 |

## 选择唯一值和不分组的行

`DISTINCT` 谓词可让你仅从数据集中的所选字段检索唯一值。例如，以下 SQL 语句只从 `PvTblFeed` 表中选择市场名称，结果为 14 条记录：

```
SELECT DISTINCT Market
FROM PvTblFeed
```

如果 SQL 语句选择多个字段，则只有当所有字段的值组合对于某条记录来说是唯一的，该记录才会包含在结果中。

如果要求整行具有唯一性，可以使用 `DISTINCTROW` 谓词。`DISTINCTROW` 谓词可让你仅检索整行唯一的记录。也就是说，所选字段中的所有值组合不能与返回数据集中的任何其他记录相匹配。使用 `DISTINCTROW` 谓词的方式与在 `SELECT DISTINCT` 子句中的用法相同：

```
SELECT DISTINCTROW AccountManagerID
FROM Dim_AccountManagers
```

## 使用 GROUP BY 子句进行分组和聚合

`GROUP BY` 子句使你能够按照列值对数据集中的记录进行聚合。在“设计”视图中创建聚合查询时，本质上就是在使用 `GROUP BY` 子句。以下 SQL 语句将按 `Market` 字段分组，并返回每个市场中的州数量：

```
SELECT Market, Count(State)
FROM Dim_Territory
GROUP BY Market
```

使用 `GROUP BY` 子句时，查询中包含的任何 `WHERE` 子句都会在聚合发生之前进行计算。但是，在某些情况下，你可能需要在完成分组后再应用 `WHERE` 条件。这时可以使用 `HAVING` 子句。

例如，以下 SQL 语句将对 `Market` 字段值为 Dallas 的记录进行分组，然后仅返回 `Revenue` 总和小于 100 的客户记录。同样，分组操作会在检查 `Revenue` 总和是否小于 100 之前完成：

```
SELECT Customer_Name, Sum(Revenue) AS Sales
FROM PvTblFeed
Where Market = "Dallas"
GROUP BY Customer_Name
HAVING (Sum(Revenue)<100)
```

## 1.1 集合的概念

在小学和初中，我们已经接触过一些集合，例如，自然数的集合，同一平面内到一个定点的距离等于定长的点的集合（即圆），所有正方形组成的集合等。

为了更有效地使用集合这一工具，我们需要进一步学习集合的有关概念和基本运算。

一般地，我们把指定的某些对象的全体称为集合（set），通常用大写英文字母 A，B，C，…表示。集合中的每个对象叫作这个集合的元素（element），通常用小写英文字母 a，b，c，…表示。

给定一个集合，它的元素必须是确定的。例如，中国的直辖市组成一个集合，北京、上海、天津、重庆都在这个集合中，而广州、南京等都不在这个集合中。

给定一个集合，它的元素必须是互异的。也就是说，集合中的元素是不重复出现的。例如，方程 (x-1)(x-2)=0 的解集，它有两个元素 1 和 2，而不能写成 {1, 1, 2}。

集合中的元素具有以下特点：

- 1. 确定性：集合中的元素必须是确定的。
- 2. 互异性：集合中的元素是不重复出现的。
- 3. 无序性：集合中的元素排列没有顺序。

如果 a 是集合 A 的元素，就说 a 属于集合 A，记作 a ∈ A；如果 a 不是集合 A 的元素，就说 a 不属于集合 A，记作 a ∉ A。

例如，若用 A 表示方程 (x-1)(x-2)=0 的解集，则 1 ∈ A，2 ∈ A，但 3 ∉ A。

我们通常用大写拉丁字母 A，B，C，…表示集合，用小写拉丁字母 a，b，c，…表示集合中的元素。

