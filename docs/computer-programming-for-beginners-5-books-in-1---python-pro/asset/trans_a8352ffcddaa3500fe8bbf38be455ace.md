
相关的。

下面是一些示例语法，用于将数据库用户关联到登录名，并为其分配数据库角色。这可能有点繁琐，但我已将其分解为四个部分，以便更容易理解。

```sql
--Using the database that we'd like to add the user to
USE [AdventureWorks2012]
GO
--Creating the user called 'User A' for the login 'User A'
CREATE USER [User A] FOR LOGIN [User A]
GO
--Using AdventureWorks2012 again, since the database level role needs to be properly
--mapped to the user
USE [AdventureWorks2012]
GO
--Altering the role for db_datawriter and adding the database user 'User A' so
--the user can add, delete or modify existing data within AdventureWorks2012
ALTER ROLE [db_datawriter] ADD MEMBER [User A]
GO
```

## LIKE 子句

SQL 为我们提供了 LIKE 子句，它可以帮助我们使用通配符将某个值与相似的值进行比较。

与 LIKE 子句一起使用的通配符包括百分号（%）和下划线（_）。

这些符号的语法如下：

```sql
SELECT * FROM tableName
WHERE column LIKE 'XXX%'
```

或者以下语法：

```sql
SELECT * FROM tableName
WHERE column LIKE '%XXX%'
```

或者以下语法：

```sql
SELECT * FROM tableName
WHERE column LIKE 'XXX_'
```

或者以下语法：

```sql
SELECT * FROM tableName
WHERE column LIKE '_XXX'
```

或者以下语法：

```sql
SELECT * FROM tableName
WHERE column LIKE '_XXX_'
```

如果有多个条件，请使用连接运算符（AND、OR）将它们组合起来。上述情况中的 XXX 代表任何字符串或数值。

下面描述一些可以使用 LIKE 子句创建的语句的含义：

- 1. `WHERE SALARY LIKE '300%'`

  返回任何以 300 开头的值。

- 2. `WHERE SALARY LIKE '%300%'`

  这将返回任何位置包含 300 的值。

- 3. `WHERE SALARY LIKE '_00%'`

  这将查找第二个和第三个位置为 00 的值。

- 4. `WHERE SALARY LIKE '4_%_%'`

  这将查找以 4 开头且长度至少为 3 个字符的值。

- 5. `WHERE SALARY LIKE '%3'`

  这将查找以 3 结尾的值。

- 6. `WHERE SALARY LIKE '_3%4'`

  这将查找第二个位置为 3 且以 4 结尾的值。

- 7. `WHERE SALARY LIKE '3_____4'`

  这将查找一个 5 位数字中以 3 开头、以 4 结尾的值。

现在，我们需要演示如何使用这个子句。我们将使用 EMPLOYEES 表，其数据如下所示：

| ID | NAME | ADDRESS | AGE | SALARY |
|---:|---|---|---:|---:|
| 2 | Mercy | Mercy32 | 25 | 3500.00 |
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 4 | Alice | Alice442 | 31 | 2500.00 |
| 5 | Nicholas | nichol442 | 45 | 5000.00 |
| 6 | Milly | mil342 | 32 | 2000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |

让我们运行一条命令，显示薪水以 400 开头的所有记录：

```sql
SELECT * FROM EMPLOYEES
WHERE SALARY LIKE '400%';
```

该命令返回以下结果：

```
mysql> SELECT * FROM EMPLOYEES
    -> WHERE SALARY LIKE '400%';
```

| ID | NAME | ADDRESS | AGE | SALARY |
|---:|---|---|---:|---:|
| 3 | Joel | Joel42 | 30 | 4000.00 |
| 7 | Grace | gra361 | 35 | 4000.00 |

```
2 rows in set (0.13 sec)
```

## SQL 函数⁶³

语法如下：

```sql
SELECT COUNT(<expression>)
FROM table_name;
```

| ID | EMP_NAME | SALES | BRANCH |
|---|---|---|---|
| 1001 | ALAN MARSCH | 3000.00 | NEW YORK |
| 1098 | NEIL BANKS | 5400.00 | LOS ANGELES |
| 2005 | RAIN ALONZO | 4000.00 | NEW YORK |
| 3008 | MARK FIELDING | 3555.00 | CHICAGO |
| 4356 | JENNER BANKS | 14600.00 | NEW YORK |
| 4810 | MAINE ROD | 7000.00 | NEW YORK |
| 5783 | JACK RINGER | 6000.00 | CHICAGO |
| 6431 | MARK TWAIN | 10000.00 | LOS ANGELES |
| 7543 | JACKIE FELTS | 3500.00 | CHICAGO |
| 8934 | MARK GOTH | 5400.00 | AUSTIN |

10 rows in set (0.00 sec)

在此语句中，表达式可以指算术运算或列名。如果要计算表中存储的总记录数，也可以指定 (*)。¹

要执行简单的计数操作，例如计算 SALES_REP 表中有多少行，请输入：

```sql
SELECT COUNT(EMP_NAME)
FROM SALES_REP;
```

结果如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_206_0.png)

你也可以使用 (*) 而不是指定列名。

```sql
SELECT COUNT(*)
FROM SALES_REP;
```

该语句将产生相同的结果，因为 EMP_NAME 字段没有 NULL 值。但是，假设 EMP_NAME 字段中的某个值包含 NULL 值，那么这个 NULL 值不会包含在指定 EMP_NAME 的语句中，但如果你使用 * 符号作为参数，它将会包含在 COUNT() 结果中。

```sql
SELECT BRANCH, COUNT(*) FROM SALES_REP
GROUP BY BRANCH;
```

输出如下：

| BRANCH | COUNT(*) |
| --- | ---: |
| AUSTIN | 1 |
| CHICAGO | 3 |
| LOS ANGELES | 2 |
| NEW YORK | 4 |

4 rows in set (0.04 sec)

COUNT() 函数可以与 DISTINCT 一起使用，以查找不同条目的数量。例如，如果你想了解 SALES_REP 表中保存了多少个不同的分公司，请输入以下语句：

```sql
SELECT COUNT (DISTINCT BRANCH)
FROM SALES_REP;
```

| COUNT(DISTINCT BRANCH) |
|---:|
| 4 |

1 row in set (0.15 sec)

## SQL AVG 函数⁴

语法如下：

```sql
SELECT AVG(<expression>)
FROM table_name;
```

| ID | EMP_NAME | SALES | BRANCH |
|---:|---|---:|---|
| 1001 | ALAN MARSCH | 3000.00 | NEW YORK |
| 1098 | NEIL BANKS | 5400.00 | LOS ANGELES |
| 2005 | RAIN ALONZO | 4000.00 | NEW YORK |
| 3008 | MARK FIELDING | 3555.00 | CHICAGO |
| 4356 | JENNER BANKS | 14600.00 | NEW YORK |
| 4810 | MAINE ROD | 7000.00 | NEW YORK |
| 5783 | JACK RINGER | 6000.00 | CHICAGO |
| 6431 | MARK TWAIN | 10000.00 | LOS ANGELES |
| 7543 | JACKIE FELTS | 3500.00 | CHICAGO |
| 8934 | MARK GOTH | 5400.00 | AUSTIN |

10 rows in set (0.00 sec)

在上述语句中，表达式可以指算术运算或列名。算术运算可以包含单列或多列。

在第一个示例中，你将使用 AVG() 函数计算平均销售额。可以输入以下语句：

```sql
SELECT AVG(Sales) FROM Sales_Rep;
```

结果如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_210_0.png)

https://docs.microsoft.com/en-us/sql/t-sql/statements/create-function-transact-sql?view=sql-server-2017

数字 6245.500000 是 Sales_Rep 表中所有销售数据的平均值，其计算方法是将 Sales 字段相加，并将结果除以记录数（在本示例中为 10 行）。

AVG() 函数可用于算术运算。例如，假设销售税为销售额的 6.6%，你可以使用以下语句计算平均销售税额：

```sql
SELECT AVG(Sales*.066) FROM Sales_Rep;
```

结果如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_211_0.png)

https://docs.microsoft.com/en-us/sql/t-sql/statements/create-function-transact-sql?view=sql-server-2017

为了获得该结果，SQL 必须先计算算术运算 `Sales *.066` 的结果，然后再应用 AVG 函数。

```sql
SELECT Branch, AVG(Sales) FROM Sales_Rep
GROUP BY Branch;
```

结果如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_212_0.png)

| Branch | AVG(Sales) |
|---|---:|
| AUSTIN | 5400.000000 |
| CHICAGO | 4351.666667 |
| LOS ANGELES | 7700.000000 |
| NEW YORK | 7150.000000 |

4 rows in set (0.06 sec)

https://docs.microsoft.com/en-us/sql/t-sql/statements/create-function-transact-sql?view=sql-server-2017

## SQL ROUND 函数

以下是 SQL ROUND() 函数的语法：

```sql
ROUND (expression, [decimal place])
```

在上述语句中，decimal place（小数位数）指定将返回的小数点位数。例如，指定 -1 将把数字四舍五入到最接近的十位数。

