
- 应将哪一列（或多列）用作主键？
- 可以为每一列分配什么类型的数据？
- 每一列的最大宽度是多少？
- 哪些列可以为空，哪些列不应为空？

以下示例在 xyzcompany 数据库中创建一个新表。该表将命名为 EMPLOYEES：

```sql
CREATE TABLE EMPLOYEES(
ID INT(6) AUTO_INCREMENT NOT NULL,
FIRST_NAME VARCHAR(35) NOT NULL,
LAST_NAME VARCHAR(35) NOT NULL,
POSITION VARCHAR(35),
SALARY DECIMAL(9,2),
ADDRESS VARCHAR(50),
PRIMARY KEY (ID)
);
```

这段代码创建了一个包含 6 列的表。ID 字段被指定为主键。第一列是 INT 数据类型，精度为 6。它不接受 NULL 值。第二列 FIRST_NAME 是 VARCHAR 类型，最大范围为 35 个字符。第三列 LAST_NAME 也是 VARCHAR 类型，最多 35 个字符。第四列 POSITION 是 VARCHAR 类型，设置为最多 35 个字符。第五列 SALARY 是 DECIMAL 类型，精度为 9、小数位为 2。最后，第六列 ADDRESS 是 VARCHAR 类型，最多 50 个字符。ID 列被指定为主键。

## 基于现有表创建新表

可以通过将 CREATE TABLE 关键字与 SELECT 一起使用，基于现有表创建新表。

语法如下：³¹

```sql
CREATE TABLE new_table_name AS
(
SELECT [column_name1, column_name2, ..., column_nameN]
FROM existing_table_name
[WHERE]
);
```

执行此代码将创建一个新表，其列定义与原表相同。你可以复制所有列，或为新表选择特定列。新表将由原表中的值填充。

为了演示，在 xyzcompany 中基于现有的 EMPLOYEES 表创建一个名为 STOCKHOLDERS 的副本表。代码如下：

```sql
CREATE TABLE STOCKHOLDERS AS
SELECT ID, FIRST_NAME, LAST_NAME, POSITION, SALARY, ADDRESS
FROM EMPLOYEES;
```

## 向表中插入数据

SQL 的数据操作语言（DML）用于对数据库执行更改。你可以使用 DML 子句用新数据填充表并更新现有表。

### 用新数据填充表

用新信息填充表有两种方式：手动输入，或通过计算机程序自动输入。

手动填充数据涉及使用键盘进行数据录入，而自动输入涉及从外部源加载数据。它还可能包括将数据从一个数据库传输到目标数据库。

与不区分大小写的 SQL 关键字或子句不同，数据区分大小写。因此，在使用或引用数据时必须确保一致性。例如，如果你将员工的名字存储为‘Martin’，那么以后应始终以‘Martin’来引用它，绝不要写成‘MARTIN’或‘martin’。

### INSERT 关键字

INSERT 关键字用于向表中添加记录。它将新的数据行插入现有表。

使用 INSERT 关键字添加数据有两种方式。在第一种格式中，只需为每个字段提供值，这些值将按顺序分配给表的列。如果需要向所有列添加数据，通常使用这种形式。

第一种形式将使用以下语法：

```sql
INSERT INTO table_name
VALUES ('value1', 'value2', [NULL]);
```

在第二种形式中，必须包含列名。值将根据列出现的顺序进行分配。如果希望向特定列添加记录，通常使用这种形式。

语法如下：

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES ('value1', 'value2', 'value3');
```

请注意，在两种形式中，都使用逗号分隔列和值。此外，必须将字符/字符串和日期/时间数据括在引号内。

假设你有以下员工记录：

- 名：Robert
- 姓：Page
- 职位：文员
- 薪资：5,000.00
- 地址：282 Patterson Avenue, Illinois

要将这些数据插入 EMPLOYEES 表，可以使用以下语句：

```sql
INSERT INTO EMPLOYEES (FIRST_NAME, LAST_NAME, POSITION,
SALARY, ADDRESS)
VALUES ('Robert', 'Page', 'Clerk', 5000.00, '282 Patterson Avenue, Illinois');
```

要查看更新后的表，语法如下：

```sql
SELECT * FROM table_name;
```

要显示存储在 EMPLOYEES 表中的数据，请使用以下语句：

```sql
SELECT * FROM EMPLOYEES;
```

通配符（*）字符告诉数据库系统选择表中的所有字段。

结果截图如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_154_0.png)

现在，尝试为另一组员工录入以下数据：

| 名 | 姓 | 职位 | 薪资 | 地址 |
| --- | --- | --- | ---: | --- |
| John | Malley | 主管 | 7,000.00 | 5 Lake View, New York |
| Kristen | Johnston | 文员 | 4,500.00 | 25 Jump Road, Florida |
| Jack | Burns | 代理 | 5,000.00 | 5 Green Meadows, California |

你将不得不重复使用 INSERT INTO 关键字，将每位员工的数据输入数据库。这些语句如下所示：

```sql
INSERT INTO EMPLOYEES(FIRST_NAME, LAST_NAME, POSITION, SALARY, ADDRESS)
VALUES('John', 'Malley', 'Supervisor', 7000.00, '5 Lake View New York');

INSERT INTO EMPLOYEES(FIRST_NAME, LAST_NAME, POSITION, SALARY, ADDRESS)
VALUES('Kristen', 'Johnston', 'Clerk', 4000.00, '25 Jump Road, Florida');

INSERT INTO EMPLOYEES(FIRST_NAME, LAST_NAME, POSITION, SALARY, ADDRESS)
VALUES('Jack', 'Burns', 'Agent', 5000.00, '5 Green Meadows, California');
```

要获取更新后的 EMPLOYEES 表，请使用带有通配符的 SELECT 命令。

```sql
SELECT * FROM EMPLOYEES;
```

结果截图如下：

![](img/239ff1e8a63502805c86c4dfbd71509a_155_0.png)

请注意，SQL 为你输入的每组数据分配了一个 ID 编号。这是因为你使用 auto_increment 属性定义了 ID 列。此属性会阻止你在插入数据时使用第一种形式。因此，你必须在 INSERT INTO table_name 行中指定其余列。

### 向特定列插入数据

也可以向特定列插入数据。可以通过在 INSERT INTO 语句的列列表中指定列名，并在 VALUES 列表中指定对应值来实现。例如，如果你只想输入员工的全名和职位，需要在列列表中指定列名 FIRST_NAME、LAST_NAME 和 SALARY，并在 VALUES 列表中指定名、姓和薪资的值。

要了解其工作方式，请尝试将以下数据输入 EMPLOYEES 表：

| 名 | 姓 | 职位 | 薪资 | 地址 |
| --- | --- | --- | ---: | --- |
| James | Hunt |  | 7,500.00 |  |

更新后的 EMPLOYEES 表截图如下。

![](img/239ff1e8a63502805c86c4dfbd71509a_156_0.png)

### 插入 NULL 值

在某些情况下，你可能必须向列中输入 NULL 值。例如，你可能没有现成数据来输入新员工的薪资。随便提供任何薪资数字都可能产生误导。

语法如下：

```sql
INSERT INTO schema.table_name
VALUES ('column1', NULL, 'column3');
```

你需要这份答案表来检查每个练习中的语法，以确保其正确。如果你在某个练习中卡住了，也非常欢迎使用它。在每个练习结束时，我鼓励你检查答案。

每个练习都会在你开始应用各节所学内容之前，提供概述和示例。

下面是接下来几个练习中将要使用的 Product 表示例。

| 产品 ID | 名称 | 产品编号 | 颜色 | 标准成本 | 列表价格 | 尺寸 |
| --- | --- | --- | --- | ---: | ---: | --- |
| 317 | LL Craniums | CA-5965 | 黑色 | 0 | 0 | NULL |
| 318 | ML Craniums | CA-6738 | 黑色 | 0 | 0 | NULL |
| 319 | HL Cranium | CA-7457 | 黑色 | 0 | 0 | NULL |
| 320 | Churning Balls | TB-2903 | 银色 | 0 | 0 | NULL |
| 321 | Churning Nut | CN-6817 | 银色 | 0 | 0 | NULL |

## 查询结构与 SELECT 语句

理解语法及其结构将来会对你非常有帮助。让我们深入了解最常见语句之一的基础知识：SELECT 语句，它仅用于检索数据。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
```

在上述查询中，你从整个表中选择两列和所有行。由于只选择两列，该查询的执行速度将比像下面这样选择所有列快得多：

```sql
SELECT *
FROM Table_Name
```

从 Production.Product 表中选择所有列。

使用同一个表，仅选择 ProductID、Name、Product Number、Color 和 Safety Stock Level 列。

*（提示：表中的列名不包含空格！）*

### WHERE 子句

WHERE 子句用于筛选查询返回的行数。该子句通过使用条件来工作，例如某列等于、大于
