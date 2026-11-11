
要查询并显示所创建视图的记录，请使用以下 select 语句：

```sql
SELECT * FROM [Female Depositors]
```

执行上述 select 语句将生成以下视图：

| cust_id | first_nm | second_nm | lastname | sex | Date_of_birth |
|---|---|---|---|---|---|
| 03051 | Mary | Ellen | Brown | Female | 1980-10-19 |
| 03231 | Juan |  | Maslow | Female | 1978-11-18 |

然而，必须注意，视图从不存储在内存中，而是在需要时重新创建。视图可以像处理真实表一样进行处理。

表 4.2 customer_personal_info

```sql
SELECT a.acct_no, b.first_nm AS first_name, b.lastname AS surname, b.sex,
a.acct_bal
FROM customer_accounts AS a
INNER JOIN customer_personal_info AS b
ON b.cust_id = a.cust_id
```

上述 SQL 查询将产生下面表 4.3 中的结果集：

| acct_no | first_name | surname | sex | acct_bal |
|---|---|---|---|---|
| 0411003 | Juan | Maslow | Female | 2540.33 |
| 0412007 | John | Pascal | Male | 10350.02 |
| 0412010 | Alan | Basal | Male | 7500.00 |

表 4.3

### SQL RIGHT JOIN

当与 SQL SELECT 语句一起使用时，“RIGHT JOIN”关键字会包含右数据表中的所有记录，即使在左数据表中找不到匹配记录也是如此。使用语法如下所述：

```sql
SELECT column-1, column-2… column-n
FROM left-data_table
RIGHT JOIN right-data_table
ON left-data_table.keyColumn = right-data_table.foreign_keycolumn
```

例如，要跨两个表（customer_accounts 和 customer_personal_info）选择客户的 acct_no、first_name、surname、sex 和 account_bal 详细信息，并显示客户个人信息，无论他们是否有活跃账户。我们使用以下 SQL“RIGHT JOIN”查询：

```sql
SELECT a.acct_no, b.first_nm AS first_name, b.lastname AS surname, b.sex,
a.acct_bal
FROM customer_accounts AS a
RIGHT JOIN customer_personal_info AS b
ON b.cust_id = a.cust_id
```

上述 SQL RIGHT JOIN 查询的执行结果展示在

### SQL UNION 命令

两个或更多 SQL select 语句的结果集可以通过“UNION”命令连接。使用语法如下所述：

```sql
SELECT column-1, column-2… column-n
FROM data_table-1
UNION
SELECT column-1, column-2… column-n
FROM data_table-2
```

来源⁸

例如，要显示我们虚拟银行在英国和美国分行的客户列表，你可以根据下面表 4.6 和表 4.7，为在两个分行都有账户的客户只显示一条记录：

| acct_no | first_name | surname | sex | acct_bal |
|---|---|---|---|---|
| 0411003 | Juan | Maslow | Female | 2540.33 |
| 0412007 | John | Pascal | Male | 10350.02 |
| 0412010 | Alan | Basal | Male | 7500.00 |

表 4.6 London_Customers

| acct_no | first_name | surname | sex | acct_bal |
|---|---|---|---|---|
| 0413112 | Deborah | Johnson | Female | 4500.33 |
| 0414304 | John | Pascal | Male | 13360.53 |
| 0414019 | Rick | Bright | Male | 5500.70 |
| 0413014 | Authur | Warren | Male | 220118.02 |

表 4.7 Washington_Customers

我们使用以下 SQL 查询：

```sql
SELECT first_name, surname, sex, acct_bal
FROM London_Customers
UNION
SELECT first_name, surname, sex, acct_bal
FROM Washington_Customers²
```

以下是上述 SQL 查询执行得到的结果集：

| first_name | surname | sex | acct_bal |
|---|---|---|---:|
| Juan | Maslow | Female | 2540.33 |
| John | Pascal | Male | 10350.02 |
| Alan | Basal | Male | 7500.00 |
| Deborah | Johnson | Female | 4500.33 |
| Rick | Bright | Male | 5500.70 |
| Authur | Warren | Male | 220118.02 |

表 4.8 SQL UNION

请注意，客户（John Pascal）的记录只列出一次，即使他是两个分行的客户。这是因为 UNION 命令只列出各表中不重复的记录。因此，要显示关联表中的所有记录，请改用“UNION ALL”。

### SQL UNION ALL 命令

UNION ALL 命令与 UNION 命令基本相同，不同之处在于它会显示联合表中的所有记录，如前所述。使用语法如下所述：

```sql
SELECT column-1, column-2… column-n
FROM data_table-1
UNION
SELECT column-1, column-2… column-n
FROM data_table-2
```

使用以下 SQL 查询对“London_Customers”和“Washington_Customers”两个表的数据应用“UNION ALL”命令：

```sql
SELECT first_name, surname, sex, acct_bal
FROM London_Customers
UNION ALL
SELECT first_name, surname, sex, acct_bal
FROM Washington_Customers
```

记录随后将显示在两个表中，如下所示：

| first_name | surname | sex | acct_bal |
|---|---|---|---:|
| Juan | Maslow | Female | 2540.33 |
| John | Pascal | Male | 10350.02 |
| Alan | Basal | Male | 7500.00 |
| Deborah | Johnson | Female | 4500.33 |
| John | Pascal | Male | 13360.53 |
| Rick | Bright | Male | 5500.70 |
| Authur | Warren | Male | 220118.02 |

表 4.9

## 第 3 章：如何确保数据完整性

> “拥有事实是知识，运用事实是智慧。”——托马斯·杰斐逊

SQL 数据库不只是存储信息。如果信息的完整性受到损害，其可靠性就变得可疑。如果数据不可靠，包含它的数据库也会变得不可靠。

为确保数据完整性，SQL 提供了多种规则，可限制表所能容纳的值。这些规则称为“完整性约束”，作用于列和表。本章将解释每一种约束。

### 完整性约束——基础

SQL 用户将完整性约束分为以下类别：

- 断言（Assertions）——你需要在单独的定义（称为“断言定义”）中定义此约束。这意味着你无需在表定义中指明断言。在 SQL 中，可以将断言应用于多个表。
- 与表相关的约束（Table-Related Constraints）——这是需要在表定义内部定义的约束。你可以将约束定义为表或列定义的一个组成部分。
- 域约束（Domain Constraints）——与断言类似，你需要在单独的定义中创建域约束。这种约束作用于你在相关域内声明的列。

表相关约束提供了多种约束选项。因此，如今它是最流行的一类完整性约束。你可以将这一类分为两种：列约束和表约束。前者属于列的定义，后者则作为表的元素起作用。

表和列约束可与不同种类的约束配合使用。然而，域约束和断言只能与一种约束类型配合使用。

### NOT NULL 约束

在上一章中，你了解到“null”表示未知/未定义的值。请记住，未定义/未知不同于零、空白、默认值和空字符串。相反，它表示缺少值。你可以将此值视为一个“标志”（即表示某列相关数据的位、数字或字符）。如果你将某列留空，因而该值为 null，系统会放置该“标志”以表明它是未知值。

列有一个称为“可空性”的属性。此属性表明列是否可以接受未知值。在 SQL 中，列被设置为可接受 null 值。不过，你可以根据需要更改此属性。要禁用列的可空性，只需使用 NOT NULL 约束。此约束告知 SQL，该列不接受任何 null 值。

在这种语言中，你需要在列上使用 NOT NULL。这意味着你不能在断言、域约束或基于表的约束上使用此约束。使用 NOT NULL 的过程很简单。只需将以下语法添加到列定义中：

```sql
(name of column) [ ( domain) | (data type) ] NOT NULL
```

例如，假设你需要生成一个名为 FICTION_NOVEL_AUTHORS 的表。此表需要有三列：AUTHOR_ID、AUTHOR_NAME 和 AUTHOR_DOB。你需要确保添加的每个条目都具有 AUTHOR_ID 和 AUTHOR_NAME 的值。为此，你必须将 NOT NULL 约束插入到这两列的定义中。代码如下：

```sql
CREATE TABLE FICTION_NOVEL_AUTHORS
(
  AUTHOR_ID     INT          NOT NULL,
  AUTHOR_NAME   CHARACTER(50) NOT NULL,
  AUTHOR_DOB    CHARACTER(50)
);
```

如你所见，此代码没有为 AUTHOR_DOB 列设置 NOT NULL。因此，如果新条目没有 AUTHOR_DOB 的任何值，系统将在该列中插入 null 值。

### UNIQUE 约束

表和列约束接受唯一约束。在 SQL 中，唯一约束属于以下两种类型之一：

-   1. UNIQUE
