
| 地区 | 销售额 |
| --- | ---: |
| 东部 | 4990.00 |
| 西部 | 12450.00 |

2 行记录（0.12 秒）

在前两行中，该语句告诉 SQL 从 Location 表中选择 ‘Region’ 字段，并从 Branch_Sales 表中选择 ‘Sales’ 字段的总和。该语句使用了表别名。‘Region’ 字段被别名为 Region，而 SALES 字段的总和被别名为 SALES。

表别名是为表或表列使用临时名称的做法。使用别名有助于使语句更易读、更简洁。例如，如果你选择不为第一行使用表别名，你将使用以下语句来获得相同的结果：

```sql
SELECT Location.Region,
SUM(Branch_Sales.Sales) SALES
```

或者，你可以通过使用 JOIN 和 ON 关键字来指定两个表之间的连接。例如，使用这些关键字，查询将如下所示：

```sql
SELECT A1.Region REGION, SUM(A2.Sales) SALES
FROM Location A1
JOIN Branch_Sales A2
ON A1.Branch = A2.Branch
GROUP BY A1.Region;
```

该查询将产生相同的结果：

![](img/239ff1e8a63502805c86c4dfbd71509a_238_0.png)

## 使用内连接

当两个表之间存在一个或多个匹配项时，内连接会显示行。为了演示这一点，请使用以下表：

Branch_Sales 表

| 分支 | 产品 ID | 销售额 |
| --- | ---: | ---: |
| 纽约 | 101 | 7500.00 |
| 费城 | 101 | 1980.00 |
| 丹佛 | 102 | 3500.00 |
| 西雅图 | 101 | 2500.00 |
| 底特律 | 102 | 1450.00 |

Location 表

| 地区 | 分支 |
| --- | --- |
| 东部 | 纽约 |
| 东部 | 芝加哥 |
| 东部 | 费城 |
| 东部 | 底特律 |
| 西部 | 洛杉矶 |
| 西部 | 丹佛 |
| 西部 | 西雅图 |

你可以通过使用 INNER JOIN 语句来实现这一点。

你可以输入以下内容：

```sql
SELECT A1.Branch BRANCH, SUM(A2.Sales) SALES
FROM Location A1
INNER JOIN Branch_Sales A2
ON A1.Branch = A2.Branch
GROUP BY A1.Branch;
```

²¹这将得到以下结果：

| 分支 | 销售额 |
| --- | ---: |
| 丹佛 | 3500.00 |
| 底特律 | 1450.00 |
| 纽约 | 7500.00 |
| 费城 | 1980.00 |
| 西雅图 | 2500.00 |

5 行记录（0.00 秒）

请注意，通过使用 INNER JOIN，结果中只包含在 Branch_Sales 表中有记录的分支，即使你实际上是在对 Location 表应用 SELECT 语句。‘芝加哥’和‘洛杉矶’分支被排除，因为 Branch_Sales 表中没有这些分支的记录。

## 使用外连接

在上一个示例中，你已经使用内连接来组合表，

TOP 命令帮助我们仅从表中检索前 TOP 数量的记录。但是，你必须注意，并非所有数据库都支持 TOP 命令。有些支持 LIMIT，而另一些支持 ROWNUM 子句。

以下是在 SELECT 语句上使用 TOP 命令的语法：

```sql
SELECT TOP number|percent columnName(s)
FROM tableName
WHERE [condition]
```

我们想使用 EMPLOYEES 表来演示如何使用该子句。该表有以下数据：

![](img/239ff1e8a63502805c86c4dfbd71509a_242_0.png)

以下查询将帮助我们获取表中的前 2 行：

```sql
SELECT TOP 2 * FROM EMPLOYEES;
```

请注意，上面给出的命令仅在 SQL Server 中有效。如果你使用的是 MySQL Server，请使用如下所示的 LIMIT 子句：

```sql
SELECT * FROM EMPLOYEES

LIMIT 2;
```

```text
mysql> SELECT * FROM EMPLOYEES
    -> LIMIT 2;
+----+------+---------+-----+----------+
| ID | NAME | ADDRESS | AGE | SALARY   |
+----+------+---------+-----+----------+
|  2 | Mercy| Mercy32 |  25 | 3500.00  |
|  3 | Joel | Joel42  |  30 | 4000.00  |
+----+------+---------+-----+----------+
2 rows in set (0.37 sec)

mysql>
```

只返回表中的前两条记录。

如果你使用的是 Oracle Server，请将 ROWNUM 与 SELECT 子句一起使用，如下所示：

```sql
SELECT * FROM EMPLOYEES
WHERE ROWNUM <= 2;
```

## ORDER BY 子句

该子句帮助我们按升序或降序对数据进行排序。可以依赖一个或多个列来完成排序。在大多数数据库中，结果默认按升序排序。

ORDER BY 子句使用以下语法：

```sql
SELECT columns_list
FROM tableName
[WHERE condition]
```

在 ORDER BY 子句中，你可以使用一个或多个列。但是，你必须确保你选择用于排序数据的列在列列表中。再次，我们将使用具有如下所示数据的 EMPLOYEES 表：

| ID | 姓名 | 地址 | 年龄 | 薪资 |
| ---: | --- | --- | ---: | ---: |
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 5 | Nicholas | nicol442 | 45 | 5000.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |

现在，我们需要使用 NAME 和 SALARY 列按升序对数据进行排序。以下命令将帮助我们实现这一点：

```sql
SELECT * FROM EMPLOYEES
ORDER BY NAME, SALARY;
```

该查询将返回以下结果：

| ID | 姓名 | 地址 | 年龄 | 薪资 |
| ---: | --- | --- | ---: | ---: |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |
| 5 | Nicholas | nicol442 | 45 | 5000.00 |

6 行记录（0.32 秒）

我们还可以使用 SALARY 列按降序对数据进行排序：

```sql
SELECT * FROM EMPLOYEES
ORDER BY SALARY DESC;
```

结果如下：

```text
mysql> SELECT * FROM EMPLOYEES
    -> ORDER BY SALARY DESC;
```

| ID | 姓名 | 地址 | 年龄 | 薪资 |
| ---: | --- | --- | ---: | ---: |
| 5 | Nicholas | nicol442 | 45 | 5000.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |

6 行记录（0.05 秒）

mysql>

[https://www.tutorialspoint.com/sql/sql-top-clause.htm](https://www.tutorialspoint.com/sql/sql-top-clause.htm)

## GROUP BY 子句

该子句与 SELECT 语句一起使用，将相关的数据分组，创建组。在 SELECT 语句中，GROUP BY 子句应位于 WHERE 子句之后，并应位于 ORDER BY 子句之前。

以下是语法：

```sql
SELECT column_1, column_2
FROM tableName
WHERE [ conditions ]
GROUP BY column_1, column_2
ORDER BY column_1, column_2
```

让我们使用具有如下所示数据的 EMPLOYEES 表：

| ID | 姓名 | 地址 | 年龄 | 薪资 |
| ---: | --- | --- | ---: | ---: |
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 5 | Nicholas | nicol442 | 45 | 5000.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |

如果你需要获取每个客户的总 SALARY，只需运行以下命令：

```sql
SELECT NAME, SALARY, SUM(SALARY) FROM EMPLOYEES
GROUP BY NAME;
```

## DISTINCT 关键字

该关键字与 SELECT 语句一起使用，帮助消除重复项，并允许选择唯一记录。

这是因为有时表中会有多个重复记录，而你的目标只是选择唯一的记录。DISTINCT 关键字可以帮助你实现这一点。该关键字可与以下语法一起使用：

```sql
SELECT DISTINCT column_1, column_2,.....column_N
FROM tableName
WHERE [condition]
```

我们将使用 EMPLOYEES 表来演示如何使用该关键字。该表有以下数据：

| ID | 姓名 | 地址 | 年龄 | 薪资 |
| ---: | --- | --- | ---: | ---: |
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 5 | Nicholas | nicol442 | 45 | 5000.00 |
| 6 | Milly | mi1342 | 32 | 2000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |

上表的 SALARY 列中有一个重复条目 4000。这可以在我们运行以下查询后看到：

```sql
SELECT DISTINCT SALARY FROM EMPLOYEES
ORDER BY SALARY;
```

