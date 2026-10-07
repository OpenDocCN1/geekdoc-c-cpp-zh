
你可以一次更新一个或多个列，使用 `WHERE` 子句指定任何条件，并一次更新单个表中的值。当你想要更新表中选定的行时，`WHERE` 子句非常有用。

让我们将这些信息应用于实际示例中：

![](img/989605394af9c1cdcfc5a952af3b7bd1_1182_0.png)

如果我们想更新 `person_info` 表中某些人的姓氏怎么办？使用 `UPDATE` 命令可以轻松实现。查看上面的 SQL 查询。

`UPDATE person_info,`，这指定了我们要更新 `person_info` 表中的数据值。

`SET LastName = ‘Rogers,’`，这指定了我们希望 `LastName` 列的新值是什么。

`Where PersonID in (2,3),`，这可能是最重要的部分。查询的这部分说明我们**只想要更新 PersonID 等于 2 或 3 的值**。这尤其为重要。如果我们不包含这条语句，它将把我们所有的 `LastName` 值都更新为 ‘Rogers’。

## 10.2 - 使用 DELETE

在某些情况下，我们可能想要从数据库中完全删除数据。为此，我们使用 `DELETE` 命令。使用此命令时要小心，因为一旦你从数据库中删除了记录记录，它就永远消失了！MySQL 也不会发出警告消息或提示询问你“你确定要删除此记录吗？”。这意味着如果你计划使用此命令，必须极其小心。

使用 `DELETE` 的语法如下：

```
DELETE FROM table_name [WHERE Clause]
```

如果未指定 `WHERE` 子句，则所有记录将从指定的 MySQL 表中删除。

你可以使用 `WHERE` 子句指定任何条件。你可以一次删除单个表中的记录。当你想要删除表中的选行时，`WHERE` 子句非常有用。

让我们将其应用于实际示例：

```
DELETE FROM city_info

WHERE CityID = 7
```

我们已经有了 `city_info` 表，其中包含各种城市的信息。如果我们不再需要跟踪其中一个城市的信息并想从数据库中删除该记录怎么办？我们只需要找到该城市的唯一 `CityID`，并将值插入到 `DELETE FROM` 命令的 `WHERE` 子句中。

`DELETE FROM city_info,`，我们指定了要从哪个表中删除。
`WHERE CityID = 7,`，这指定了我们要从表中删除的精确记录。

在 MySQL Workbench 中尝试更新记录时，可能会遇到“Error Code: 1175 You are using safe update mode and you tried to update a table without a WHERE clause that uses a KEY column.”（错误代码：1175 你正在使用安全更新模式，并尝试在没有使用使用 KEY 列的 WHERE 子句的情况下更新表）。

此类发生是因为你的 MySQL 会话设置了 `safe-updates` 选项。这意味着你不能在不指定 `WHERE` 子句中的键的情况下更新或删除记录。要避免这种情况，请执行以下查询：

![](img/989605394af9c1cdcfc5a952af3b7bd1_1185_0.png)

这将防止在使用你的 `UPDATE` 语句时发生此错误。

> 试一下！尝试使用 `UPDATE` 和 `DELETE` 命令。使用 `UPDATE` 让 PersonIds 1、2 和 3 具有相同的姓氏。此外，删除 `city_info` 表中某一个没有来自该城市人员的城市。

## 10.3 - 使用 TRUNCATE

`TRUNCATE` 是从表中删除记录的另一种方法。MySQL `TRUNCATE TABLE` 语句允许你删除表中的所有数据。从逻辑上讲，`TRUNCATE TABLE` 语句类似于不带 `WHERE` 子句的 `DELETE` 语句，它会删除表中的所有行。它通过使用 `DROP TABLE` 语句后 `CREATE TABLE` 语句来实现相同的功能。然而，`TRUNCATE TABLE` 语句比 `DELETE` 语句更高效，因为它删除并重建表，而不是逐行删除行。

这里是 `TRUNCATE TABLE` 语句的基本语法：

```
TRUNCATE [TABLE] table_name;
```

`table_name` - 你想要移除所有数据的表名。

`TABLE` - 这个关键字是可选的。但是，使用 `TABLE` 关键字是一个良好的习惯，可以区分 `TRUNCATE TABLE` 语句和 `TRUNCATE()` 函数。

如果有从其他表引用你所截断的表的外键 `FOREIGN KEY` 约束，则 `TRUNCATE TABLE` 语句将失败。`TRUNCATE` 操作会导致隐式提交；因此，它无法回滚。`TRUNCATE TABLE` 语句还会重置 `AUTO_INCREMENT` 字段中的当前值。`TRUNCATE TABLE` 语句不会触发任何与被截断表关联的 `DELETE` 触发器。与 `DELETE` 不同，`TRUNCATE TABLE` 语句不会触发。

查看使用 `TRUNCATE TABLE` 语句的示例：

```
TRUNCATE TABLE person_info
```

## 10.4 - DELETE 与 TRUNCATE

`DELETE` 和 `TRUNCATE` 看起来的效果相同，但工作方式不同。以下是这两个语句之间的一些区别：

- `DELETE` 允许根据 `WHERE` 子句过滤要删除的行，而 `TRUNCATE` 不支持 `WHERE` 子句，它直接删除所有行。
- `TRUNCATE` 比 `DELETE` 更快且消耗的系统资源更少，因为 `DELETE` 会扫描表生成影响行计数，然后逐行删除，而 `TRUNCATE` 则直接删除所有行。
- `TRUNCATE TABLE` 语句会将自增值重置为初始值（通常为 1）。

如果你只想删除所有行并重建整个表，请使用 `TRUNCATE`。如果你想根据特定条件删除行，或不想重置自增值，请使用 `DELETE`。

## 10.5 - CAST

MySQL `CAST` 函数将值从一种数据类型转换为另一种数据类型。

`CAST` 函数的语法如下：

```
CAST( value AS type )
```

`value` – 要转换为另一种数据类型的值。

`type` – 你希望将值转换的数据类型。

它可以是以下之一：

| 值 | 描述 |
| --- | --- |
| DATE | 将值转换为 `DATE` 类型，仅包含日期部分。格式为 'YYYY-MM-DD'。范围为 '1000-01-01' 到 '9999-12-31'。 |
| DATETIME | 将值转换为 `DATETIME` 类型，同时日期时间和部分。格式为 'YYYY-MM-DD HH:MM:SS'。范围为 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'。 |
| TIME | 将值转换为 `TIME` 类型，包含时间部分。格式为 'HH:MM:SS'。范围为 '-838:59:59' 到 '838:59:59'。 |
| CHAR | 将值转换为 `CHAR` 类型，这是一个固定长度字符串。 |
| SIGNED | 将值转换为 `SIGNED` 类型，这是一个有符号的 64 位整数。 |
| UNSIGNED | 将值转换为 `UNSIGNED` 类型，这是一个无符号的 64 位整数。 |
| BINARY | 将值转换为 `BINARY` 类型，这是一个二进制字符串。 |

让我们看看如何使用 `CAST` 函数的一些实际示例。

```sql
SELECT CAST('2020-02-28' AS DATE);
Result: '2020-02-28'
```

此 CAST 示例获取值 '2020-02-28' 并将其转换为 DATE 类型。

```sql
SELECT CAST('2020-02-28 08:14:57' AS DATETIME);
Result: '2020-02-28 08:14:57'
```

此 CAST 示例获取值 '2020-02-28 08:14:57' 并将其转换为 DATETIME 类型。

```sql
SELECT CAST('08:14:57' AS TIME);
Result: '08:14:57'
```

此 CAST 示例获取值 '08:14:57' 并将其转换为 TIME 类型。

```sql
SELECT CAST(125 AS CHAR);
Result: '125'
```

此 CAST 示例获取值 125 并将其转换为值为 '125' 的 CHAR 数据类型。

```sql
SELECT CAST(3-4 AS SIGNED);
Result: -1
```

此 CAST 示例获取值 3-4 并将其转换为值为 -1 的 SIGNED 数据类型。

```sql
SELECT CAST(4-6 AS UNSIGNED);
Result: 18446744073709551614
```

此 CAST 示例获取值 4-6 并将其转换为值为 18446744073709551614 的 UNSIGNED 数据类型。

```sql
SELECT CAST('4' AS BINARY);
Result: '4'
```

此 CAST 示例获取值 '4' 并将其转换为具有二进制字符串值 '4' 的 BINARY 数据类型。

## 10.6 - CONVERT

MySQL `CONVERT` 函数将值从一种数据类型转换为另一种数据类型，或从一个字符集转换为另一个字符集。

`CONVERT` 函数有两种有效的语法形式：一种用于转换数据类型，另一种用于转换字符集。

`CONVERT` 函数的第一种语法用于在 MySQL 中将一种数据类型转换为另一种数据类型：

```sql
CONVERT( value, type )
```

或者

```sql
CONVERT( value USING character_set )
```

- `value` – 要要转换的值。
- `character_set` – 要转换到的目标字符集。
- `type` – 你希望将值转换到的数据类型。类型可以是以下之一：

| Value | Description |
|---|---|
| DATE | 将值转换为 DATE 类型，该类型仅包含日期部分。格式为 'YYYY-MM-DD'。支持范围为 '1000-01-01' 到 '9999-12-31'。 |
| DATETIME | 将值转换为 DATETIME 类型，该类型包含日期和时间部分。格式为 'YYYY-MM-DD HH:MM:SS'。支持范围为 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'。 |
| TIME | 将值转换为 TIME 类型，该类型仅包含时间部分。格式为 'HH:MM:SS'。支持范围为 '-838:59:59' 到 '838:59:59'。 |
| CHAR | 将值转换为 CHAR 类型，这是一个固定长度字符串。 |
| SIGNED | 将值转换为 SIGNED 类型，该类型是有符号的 64 位整数。 |
| UNSIGNED | 将值转换为 UNSIGNED 类型，该类型是无符号的 64 位整数。 |
| BINARY | 将值转换为 BINARY 类型，这是一个二进制字符串。 |

让我们来看 `CONVERT` 函数的实际示例。

```sql
SELECT CONVERT('2020-02-28', DATE);
Result: '2020-02-28'
```
此 CONVERT 示例获取值 '2020-02-28' 并将其转换为 DATE 数据类型。

```sql
SELECT CONVERT('2020-02-28 08:14:57', DATETIME);
Result: '2020-02-28 08:14:57'
```

此 CONVERT 示例获取值 '2020-02-28 08:14:57' 并将其转换为 DATETIME 数据类型。

```sql
SELECT CONVERT('08:14:57', TIME);
Result: '08:14:57'
```
此 CONVERT 示例获取值 '08:14:57' 并将其转换为 TIME 数据类型。

```sql
SELECT CONVERT(125, CHAR);
Result: '125'
```

此 CONVERT 示例获取值 125 并将其转换为值为 '125' 的 CHAR 数据类型。

```sql
SELECT CONVERT(4-6, SIGNED);
Result: -2
```
此 CONVERT 示例获取值 4-6 并将其转换为值为 -2 的 SIGNED 数据类型。

## UNSIGNED
此 CONVERT 函数展示了如何将值转换为 UNSIGNED

```sql
SELECT CONVERT(4-6, UNSIGNED);
Result: 18446744073709551614
```
此 CONVERT 示例获取值 4-6 并将其转换为值为 18446744073709551614 的 UNSIGNED 数据类型。

```sql
SELECT CONVERT('4', BINARY);
Result: '4'
```

此 CONVERT 示例获取值 '4' 并将其转换为具有二进制字符串值 '4' 的 BINARY 数据类型。

## 10.7 - CAST vs. CONVERT

`CAST` 和 `CONVERT` 函数都用于将数据从一种类型转换为另一种。然而，它们在语法和功能上存在差异。

`CAST` 函数通常用于简单的数据类型转换，而 `CONVERT` 可以用于更复杂的操作，包括字符集转换。此外，`CAST` 也可以用于转换字符集。

| Feature | CAST | CONVERT |
|---|---|---|
| **语法** | `CAST(expression AS type)` | `CONVERT(expression, type)` 或 `CONVERT(expression USING character_set)` |
| **标准** | ANSI SQL 标准 | MySQL 特有 |
| **字符集** | 支持有限 | 通过 `USING` 支持 |
| **复杂度** | 简单 | 更灵活 |

以下是一些对比 CAST 和 CONVERT 的示例：

```sql
SELECT CAST('2020-02-28' AS DATE);
Result: '2020-02-28'
```

```sql
SELECT CONVERT('2020-02-28', DATE);
Result: '2020-02-28'
```

```sql
SELECT CAST(125 AS CHAR);
Result: '125'
```

```sql
SELECT CONVERT(125, CHAR);
Result: '125'
```

# 第 11 章：GROUP BY 子句和聚合函数

MySQL `GROUP BY` 子句用于根据列或表达式的值将行分组为子。`GROUP BY` 子句根据列或表达式的值将一组行分组一组摘要行（summary rows）。`GROUP BY` 子句为每个组返回一行。换句话说，它减少了结果集的行数。

你经常将 `GROUP BY` 子句与聚合函数一起使用，如 `SUM`、`AVG`、`MAX`、`MIN` 和 `COUNT`。出现在 `SELECT` 子句中的聚合函数提供了有关每个组的信息。聚合函数对多个值进行计算并返回单个值。例如，你可以使用 `AVG()` 聚合函数，它接收多个数字并返回这些数字的平均值。

`GROUP BY` 子句是 `SELECT` 语句中的一个可选子句（此处原文可能有误，通常指查询语句的一部分）。`GROUP BY` 子句的语法如下：

```
SELECT column_1, column_2... column_n, aggregate_function(column_x)
FROM table_name
WHERE where_conditions
GROUP BY column_1, column_2... column_n;
```

`GROUP BY` 子句必须出现在 `FROM` 和 `WHERE` 子句之后。`GROUP BY` 关键字之后是一个用逗号分隔的列列表。

MySQL 在 `FROM`、`WHERE` 和 `SELECT` 子句之后、`HAVING`、`ORDER BY` 和 `LIMIT` 子句之前评估 `GROUP BY` 子句。让我们通过实际示例来应用 `GROUP BY` 子句：

![](img/989605394af9c1cdcfc5a952af3b7bd1_196_0.png) （注：原文此处文本结构较为混乱，已按逻辑翻译）

`SELECT LastName, COUNT(*)`，我们想要显示表中每个姓氏的计数。来自 `person_info`，这是包含数据的表。`GROUP BY LastName`，结果如下：

| LastName | COUNT(*) |
| Rogers |

没有 `GROUP BY`，`COUNT(*)` 函数无法按预期工作。

## 11.1 - 聚合函数

`COUNT` 函数是一个返回表中行数的聚合函数。`COUNT` 函数允许你计算匹配指定条件的行数。

`COUNT` 函数有三种形式：`COUNT(*)`、`COUNT(expression)` 和 `COUNT(DISTINCT expression)`：

- 1. `COUNT(*)` 函数：`COUNT(*)` 函数返回 `SELECT` 语句结果集中行数，包括重复值和 NULL 值。
- 2. `COUNT(expression)`：`COUNT(expression)` 返回结果集中不为 NULL 的行数。
- 3. `COUNT(DISTINCT expression)`：`COUNT(DISTINCT expression)` 返回结果集中唯一值的行数。
