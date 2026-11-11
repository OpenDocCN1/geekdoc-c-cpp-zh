
| ID | 名 | 姓 | 职位 | 资金 | 地址 |
| --- | --- | --- | --- | --- | --- |
| 1 | Robert | Page | 职员 | 5000 | 282 Patterson Avenue, Illinois |
| 2 | John | Nalley | 主管 | 7000 | 5 Lake View New York |
| 3 | Kristen | Johnston | 职员 | 4000 | 25 Jump Road Florida |
| 4 | Jack | Burns | 代理人 | 5000 | 5 Green Meadows California |
| 5 | James | Hunt | NULL | 7500 | NULL |

已选择 5 行。

## 删除列

此时，Position 列不再适用。你可以使用以下语句删除该列：

```sql
ALTER TABLE INVESTORS
DROP COLUMN Position;
```

以下是更新后的 INVESTORS 表：

| ID | 名 | 姓 | 资金 | 地址 |
| --- | --- | --- | --- | --- |
| 1 | Robert | Page | 5000 | 282 Patterson Avenue, Illinois |
| 2 | John | Nalley | 7000 | 5 Lake View New York |
| 3 | Kristen | Johnston | 4000 | 25 Jump Road Florida |
| 4 | Jack | Burns | 5000 | 5 Green Meadows California |
| 5 | James | Hunt | 7500 | NULL |

结果集中有 5 行（0.00 秒）

## 添加新列

由于你现在处理的是另一组数据，你可能会决定再添加一列，使 INVESTORS 表中的数据更具相关性。你可以添加一列，用于存储每位投资者持有的股票数量。你可以将新列命名为 STOCKS。该列将接受最多 9 位的整数。

你可以使用以下语句添加 STOCKS 列：

```sql
ALTER TABLE INVESTORS ADD STOCKS INT(9);
```

以下是更新后的 INVESTORS 表：

![](img/239ff1e8a63502805c86c4dfbd71509a_231_0.png)

| ID | 名 | 姓 | 资金 | 地址 | 股票 |
| --- | --- | --- | --- | --- | --- |
| 1 | Robert | Page | 5000.00 | 282 Patterson Avenue, Illinois | NULL |
| 2 | John | Nalley | 7000.00 | 5 Lake View New York | NULL |
| 3 | Kristen | Johnston | 4000.00 | 25 Jump Road Florida | NULL |
| 4 | Jack | Burns | 5000.00 | 5 Green Meadows California | NULL |
| 5 | James | Hunt | 7500.00 | NULL | NULL |

## 在不更改名称的情况下修改现有列

你还可以将 ALTER TABLE 命令与 MODIFY 关键字结合使用，以更改表的数据类型和规格。为演示这一点，你可以使用以下语句将 CAPITAL 列的数据类型从 INT 类型修改为最多 9 位、包含两位小数的 DECIMAL 类型。

```sql
ALTER TABLE INVESTORS MODIFY CAPITAL DECIMAL(9,2) NOT NULL;
```

此时，你可能想查看 INVESTORS 表的列名和属性。你可以使用 ‘SHOW COLUMNS’ 语句显示表结构。输入以下语句：

```sql
SHOW COLUMNS FROM INVESTORS;
```

以下是结果的截图。

| 字段 | 类型 | 空 | 键 | 默认值 | 额外 |
| --- | --- | --- | --- | --- | --- |
| ID | int(6) | 否 |  | 0 |  |
| FIRST_NAME | varchar(32) | 否 |  | NULL |  |
| LAST_NAME | varchar(32) | 否 |  | NULL |  |
| CAPITAL | decimal(9,2) | 否 |  | NULL |  |
| ADDRESS | varchar(50) | 是 |  | NULL |  |
| STOCKS | int(9) | 是 |  | NULL |  |

结果集中有 6 行（0.00 秒）

## 使用 ALTER TABLE 时要记住的规则

- 向数据库表添加列

添加新列时，请记住，不能向已有数据的表添加具有 NOT NULL 属性的列。你通常会将列指定为 NOT NULL，以表示该列将保存值。如果现有数据在新列中没有值，添加 NOT NULL 列将与该约束冲突。

- 修改字段/列

  - 1. 你可以轻松修改列的数据类型
  - 2. 你可以增加数值数据类型可容纳的位数，但只有当表中存储的最大位数等于或小于所需位数时，才能减少位数。
  - 3. 只要不超过允许的最大小数位数，你就可以增加或减少数值数据类型的小数位数。

如果处理不当，删除和修改表可能会导致有价值的信息丢失。因此，在执行 ALTER TABLE 和 DROP TABLE 语句时要格外小心。

## 删除表

删除表还会移除其数据、关联索引、触发器、约束和权限数据。使用此语句时应小心。

以下是语法：

```sql
DROP TABLE table_name;
```

例如，如果你想从 xyzcompany 数据库中删除 INVESTORS 表，可以使用以下语句：

```sql
DROP TABLE INVESTORS;
```

DROP TABLE 命令已从当前数据库中有效移除 INVESTORS 表。

如果你尝试使用以下命令访问 INVESTORS 表：

```sql
SELECT * FROM INVESTORS;
```

SQL 将返回如下错误：

![](img/239ff1e8a63502805c86c4dfbd71509a_233_0.png)

[https://docs.microsoft.com/en-us/sql/relational-databases/tables/delete-tables-database-engine?view=sql-server-2017](https://docs.microsoft.com/en-us/sql/relational-databases/tables/delete-tables-database-engine?view=sql-server-2017)

## 合并和连接表

如果多个表之间存在公共字段，你可以合并这些表中的数据。为此，请使用 JOIN 语句。

SQL 支持多种类型的 JOIN 操作：

### 内连接（INNER JOIN）

INNER JOIN（或简称为 JOIN）是最常用的 JOIN 类型。当要连接的表具有匹配字段时，它会显示这些行。

以下是语法：⁵

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;
```

在此变体中，使用 JOIN 子句代替 INNER JOIN。

```sql
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```

### 左连接（LEFT JOIN）

LEFT JOIN 操作返回左表的所有行以及与右表匹配的行。如果未找到匹配项，右侧返回 NULL。

以下是 LEFT JOIN 的语法：

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;
```

在某些数据库系统中，使用关键字 LEFT OUTER JOIN 代替 LEFT JOIN。以下是此变体的语法：

```sql
SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

### 右连接（RIGHT JOIN）

此 JOIN 操作返回右表的所有行以及与左表匹配的行。

以下是此操作的语法：

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name=table2.column_name;
```

在某些数据库系统中，使用 RIGHT OUTER JOIN 代替 RIGHT JOIN。以下是此变体的语法：

```sql
SELECT column_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

[http://www.sql-join.com/sql-join-types/](http://www.sql-join.com/sql-join-types/)

### 全外连接（FULL OUTER JOIN）

当至少一个表满足条件时，此 JOIN 操作会显示所有行。它结合了 RIGHT 和 LEFT 连接操作的结果。

以下是语法：

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

为了演示 SQL 中的 JOIN 操作，请使用 Branch_Sales 和 Branch_Location 表：

Branch_Sales 表

| 分支 | 产品ID | 销售额 |
| --- | --- | --- |
| 纽约 | 101 | 7500.00 |
| 洛杉矶 | 102 | 6450.00 |
| 芝加哥 | 101 | 1560.00 |
| 费城 | 101 | 1980.00 |
| 丹佛 | 102 | 3500.00 |
| 西雅图 | 101 | 2500.00 |
| 底特律 | 102 | 1450.00 |

Location 表

| 地区 | 分支 |
| --- | --- |
| 东 | 纽约市 |
| 东 | 芝加哥 |
| 东 | 费城 |
| 东 | 底特律 |
| 西 | 洛杉矶 |
| 西 | 丹佛 |
| 西 | 西雅图 |

目标是按地区获取销售额。Location 表包含地区和分支的数据，而 Branch_Sales 表保存每个分支的销售数据。要查找每个地区的销售额，你需要合并 Location 表和 Branch_Sales 表中的数据。注意，这些表有一个公共字段 Branch，它是连接两个表的字段。

以下语句将演示如何使用表别名连接这两个表：

```sql
SELECT A1.Region Region, SUM(A2.Sales) Sales
FROM Location A1, Branch_Sales A2
WHERE A1.Branch = A2.Branch
GROUP BY A1.Region;
```

结果将如下所示：

