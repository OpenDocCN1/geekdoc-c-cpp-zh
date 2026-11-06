
值。这里有一个示例：

```sql
CREATE TABLE CUSTOMERS(
    ID INT            NOT NULL,
    NAME VARCHAR (20) NOT NULL,
    AGE INT           NOT NULL,
    ADDRESS CHAR (25),
    SALARY DECIMAL (18, 2) DEFAULT 5000.00,
    PRIMARY KEY (ID)
);
```

这段代码生成了一个名为 CUSTOMERS 的表并将其分为 5 列。正如你所见，“ 5000.00 ” 被标记为薪资列的默认值。这意味着如果使用 INSERT INTO 命令无法添加任何值，该列将自动接收 5000.00。

要删除此约束，您可以使用以下语法：

*ALTER TABLE（在此处插入表名）*

```sql
ALTER COLUMN (insert name of column here) DROP DEFAULT;
```

- NOT NULL – 列可以包含 NULL 值。但是，如果您不希望某些列中存在 NULL 值，则可以使用此约束。此约束将阻止系统在您指定的列中输入 NULL 值。

重要提示：NULL 值表示未知信息。因此，它们与“ 无信息。 ” 不同。

下面的屏幕截图向您展示了如何使用 SQL 应用 NOT NULL 约束：

```sql
CREATE TABLE CUSTOMERS(
    ID INT            NOT NULL,
    NAME VARCHAR (20) NOT NULL,
    AGE INT           NOT NULL,
    ADDRESS CHAR (25),
    SALARY DECIMAL (18, 2),
    PRIMARY KEY (ID)
);
```

上面的代码生成了一个名为 CUSTOMERS 的表并创建了 5 列。由于 NOT NULL 约束已应用于它们，因此您无法在 ID、AGE 和 NAME 中输入 NULL 值。

要对现有列应用 NOT NULL，请使用以下语法：

```sql
ALTER TABLE (name of table here)

    MODIFY (name of column) (specify value type) NOT NULL;
```

- CHECK – 此约束可以检查您存储到表中的值。如果指定的条件给出“ 假，”，您将无法向记录中添加值。请分析下面的代码：

```sql
CREATE TABLE CUSTOMERS(
    ID INT NOT NULL,
    NAME VARCHAR (20) NOT NULL,
    AGE INT NOT NULL CHECK (AGE >= 18),
    ADDRESS CHAR (25),
    SALARY DECIMAL (18, 2),
    PRIMARY KEY (ID)
);
```

该代码创建了一个名为 CUSTOMERS 的表并将其分为五列。CHECK 约束应用于 AGE。根据其条件（即 >= 18），您将无法添加年龄低于 18 岁的客户。

要将此约束应用于现有表，您应使用以下语法：

```sql
ALTER TABLE (name of table you want to edit)

    MODIFY (name of column you want to use) (specify the value type) NOT NULL CHECK (name of column and the condition you want to apply);
```

- INDEX – 您应该使用此约束快速生成或检索数据。创建索引时，您可以选择单个列或一组列。活动索引在整理信息之前为每一行接收一个 ROWID。

良好的索引对于提高数据库的可靠性和性能是必要的。但是，在创建索引时您应格外小心。您应该选择在运行数据库搜索时使用的字段。下面的 SQL 语句创建了一个名为 CUSTOMERS 的表并将其分为 5 列：

```sql
CREATE TABLE CUSTOMERS(
    ID INT          NOT NULL,
    NAME VARCHAR (20)  NOT NULL,
    AGE INT         NOT NULL,
    ADDRESS CHAR (25) ,
    SALARY DECIMAL (18, 2),
    PRIMARY KEY (ID)
);
```

- Primary Key – 这是标识表中每个记录的字段。创建主键时，您可以使用单个字段或组合多个字段。涉及多个字段的键称为“ 复合键。 ”主键必须保存唯一值（即它们不会接受重复或 NULL 值）。

- 如何在创建新表时分配主键 - 在新表中定义主键时使用以下语法：

```sql
CREATE TABLE CUSTOMERS(
    ID INT          NOT NULL,
    NAME VARCHAR (20)  NOT NULL,
    AGE INT         NOT NULL,
    ADDRESS CHAR (25) ,
    SALARY DECIMAL (18, 2),
    PRIMARY KEY (ID)
);
```

- 如何为现有表分配主键 – 您应使用的语法如下：

*ALTER TABLE（在此处插入表名）ADD PRIMARY KEY（在此处指定列名）；*

重要提示：如果您将列指定为主键，您必须确保它不会接受 NULL 值。

- 如何删除主键 - 要禁用主键，您应使用以下语法：

*ALTER TABLE（表名）DROP PRIMARY KEY；*

- Foreign Key – 此键允许您链接数据表。因此，一些程序员将外键称为“ 引用键。 ”

外键是其值与另一表的主键相同的列。这意味着一个表的主键必须与不同表的外键匹配。

为了帮助您理解这一概念，让我们使用两个示例表：CUSTOMERS 和 ORDERS。

CUSTOMERS 表：

```sql
CREATE TABLE CUSTOMERS(
    ID INT NOT NULL,
    NAME VARCHAR (20) NOT NULL,
    AGE INT NOT NULL,
    ADDRESS CHAR (25) ,
    SALARY DECIMAL (18, 2),
    PRIMARY KEY (ID)
);
```

ORDERS 表：

```sql
CREATE TABLE ORDERS (
    ID INT NOT NULL,
    DATE DATETIME,
    CUSTOMER_ID INT references CUSTOMERS(ID),
    AMOUNT double,
    PRIMARY KEY (ID)
);
```

如果您想在现有表上分配外键，您应使用以下语法：

*ALTER TABLE（在此处插入表名）*

*ADD FOREIGN KEY（指定要用作外键的列）REFERENCES（要用作引用的表名）（第二个表的主键名）；*

## 第 3 章：SQL 语句的语法

SQL 语言使用一组独特的规则，称为“ 语法。”本章将教您 SQL 中使用的基本语法。请仔细学习本材料，因为它将帮助您在 2 周内掌握这种计算机语言。

每个 SQL 命令都以以下关键字之一开头：USE、DROP、SHOW、ALTER、UPDATE、INSERT、SELECT、DELETE 或 CREATE。此外，每个命令都以分号结束。

您应该知道 SQL 语句不区分大小写。这意味着在 SQL 命令中，DELETE 和 delete 是相同的。但是，如果您使用的是 MySQL，则应按数据库中显示的方式输入名称。

### 基本 SQL 命令的语法

### SELECT 语句

```sql
SELECT column1, column2....columnN
FROM   table_name;
```

此语句具有以下子句：

- DISTINCT 子句 –

```sql
SELECT DISTINCT column1, column2....columnN
FROM   table_name;
```

- WHERE 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  CONDITION;
```

- AND/OR 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  CONDITION-1 {AND|OR} CONDITION-2;
```

- IN 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  column_name IN (val-1, val-2....val-N);
```

- BETWEEN 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  column_name BETWEEN val-1 AND val-2;
```

- LIKE 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  column_name LIKE { PATTERN };
```

- ORDER BY 子句 –

```sql
SELECT column1, column2....columnN
FROM   table_name
WHERE  CONDITION
ORDER BY column_name {ASC|DESC};
```

- GROUP BY 子句 –

```sql
SELECT SUM(column_name)
FROM   table_name
WHERE  CONDITION
GROUP BY column_name;
```

- COUNT 子句 –

```sql
SELECT COUNT(column_name)
FROM   table_name
WHERE  CONDITION;
```

- HAVING 子句 –

```sql
SELECT SUM(column_name)
FROM table_name
WHERE CONDITION
GROUP BY column_name
HAVING (arithmetic function condition);
```

### CREATE TABLE 命令

```sql
CREATE TABLE table_name(
column1 datatype,
column2 datatype,
column3 datatype,
.....
columnN datatype,
PRIMARY KEY( one or more columns )
);
```

### DROP TABLE 命令

```sql
DROP TABLE table_name;
```

### CREATE INDEX 命令

```sql
CREATE UNIQUE INDEX index_name
ON table_name ( column1, column2,...columnN);
```

### DROP INDEX 命令

```sql
ALTER TABLE table_name
DROP INDEX index_name;
```

### DESC 命令

```sql
DESC table_name;
```

### TRUNCATE TABLE 命令

```sql
TRUNCATE TABLE table_name;
```

### ALTER TABLE 命令

```sql
ALTER TABLE table_name {ADD|DROP|MODIFY} column_name (data_type);
```

### ALTER TABLE 命令（用于重命名表）

```sql
ALTER TABLE table_name RENAME TO new_table_name;
```
