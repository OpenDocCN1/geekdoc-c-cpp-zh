
```sql
ALTER COLUMN ARREARS DROP DEFAULT;
```

## 唯一约束

该约束帮助我们避免在同一列中出现两条或更多具有相似值的记录。例如，在“employees”表中，我们可能需要防止两名或更多员工共享同一个ID。

以下SQL查询展示了如何创建名为“STUDENTS”的表。我们将对“ADMISSION”列施加UNIQUE约束：

```sql
CREATE TABLE STUDENTS(
    ADMISSION INT NOT NULL UNIQUE,
    NAME VARCHAR (15) NOT NULL,
    AGE INT NOT NULL,
    COURSE CHAR (20),
    PRIMARY KEY (ADMISSION)
);
```

```sql
mysql> CREATE TABLE STUDENTS(
    -> ADMISSION INT NOT NULL UNIQUE,
    -> NAME VARCHAR (15) NOT NULL,
    -> AGE INT NOT NULL,
    -> COURSE CHAR (20),
    -> PRIMARY KEY (ADMISSION)
    -> );
Query OK, 0 rows affected (0.11 sec)

mysql>
```

正确创建的索引能提高大型数据库的效率。选择在哪些字段上创建索引，取决于你频繁使用的SQL查询。

也许你已经创建了没有UNIQUE约束的STUDENTS表。可以通过运行以下命令在ADMISSION列上添加该约束：

```sql
ALTER TABLE STUDENTS
MODIFY ADMISSION INT NOT NULL UNIQUE;
```

如下所示：

```sql
ALTER TABLE STUDENTS
ADD CONSTRAINT uniqueConstraint UNIQUE(ADMISSION, AGE);
```

该约束被命名为“uniqueConstraint”，并指定了两个列：ADMISSION和AGE。

任何时候需要删除该约束，可以运行以下同时使用ALTER和DROP命令的命令：

```sql
ALTER TABLE STUDENTS
DROP CONSTRAINT uniqueConstraint;
```

该约束将从这两个列中删除。对于MySQL用户，上述命令不起作用。只需运行下面的命令：

```sql
ALTER TABLE STUDENTS
DROP INDEX uniqueConstraint;
```

![](img/239ff1e8a63502805c86c4dfbd71509a_259_0.png)

## 主键

主键约束帮助我们唯一标识每一行。被指定为主键的列必须具有唯一值。此外，该列不允许有NULL值。

每个表只允许有一个主键，它可以由单个或多个字段组成。当我们使用多个字段作为主键时，这些字段被称为复合键。如果表的某一列被声明为主键，那么该字段中就不会有两条记录具有相同的值。

主键是唯一标识符。在STUDENTS表中，我们可以将ADMISSION定义为主键，因为它能唯一标识每个学生。不应有两个学生拥有相同的ADMISSION编号。以下是创建该属性的方法：

```sql
CREATE TABLE STUDENTS(
    ADMISSION INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    AGE INT NOT NULL,
    PRIMARY KEY (ADMISSION)
);
```

ADMISSION已被设置为该表的主键。如果我们描述该表，你会发现该字段是主键，如下所示：

![](img/239ff1e8a63502805c86c4dfbd71509a_260_0.png)

在上面的“Key”字段中，“PRI”表示ADMISSION字段是主键。

你可能希望在一个已存在的表上施加主键约束。可以通过运行以下命令来完成：

```sql
ALTER TABLE STUDENTS
    ADD CONSTRAINT PK_STUDADM PRIMARY KEY (ADMISSION, NAME);
```

在上述命令中，主键约束被命名为“PK_STUDADM”，并指定给两列：ADMISSION和NAME。这意味着这两列的值在任意两行中都不会相同。

可以通过执行以下命令从表中删除主键约束：

```sql
ALTER TABLE STUDENTS DROP PRIMARY KEY;
```

运行上述命令后，你可以描述STUDENTS表，查看它是否还有主键：

![](img/239ff1e8a63502805c86c4dfbd71509a_261_0.png)

这表明主键已成功删除。

## 外键

该约束用于将两个表链接在一起。有时也被称为引用键。外键是一个列或一组列，与另一个表中的主键匹配。

请考虑下面给出结构的表：

STUDENTS表：

```sql
CREATE TABLE STUDENTS(
    ADMISSION INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    AGE INT NOT NULL,
    PRIMARY KEY (ADMISSION)
);
```

FEE表：

```sql
CREATE TABLE FEE (
    ID INT NOT NULL,
    DATE DATETIME,
    STUDENT_ADM INT references STUDENTS (ADMISSION),
    AMOUNT float,
    PRIMARY KEY (ID)
);
```

在FEE表中，STUDENT_ADM字段引用了STUDENTS表中的ADMISSION字段。这使得FEE表的STUDENT_ADM列成为外键。

如果我们创建FEE表时没有包含外键，我们仍然可以通过以下命令添加它：

```sql
ALTER TABLE FEE
ADD FOREIGN KEY (STUDENT_ADM) REFERENCES STUDENTS (ADMISSION);
```

外键将被添加到表中。如果需要删除外键，请运行以下命令：

```sql
ALTER TABLE FEE
DROP FOREIGN KEY;
```

然后外键将从表中删除。

## CHECK 约束

该约束用于创建一个条件，以验证输入到记录中的值。如果条件为假，则该记录违反了约束，因此不会输入到表中。

我们想要创建一个名为STUDENTS的表，并且不希望有任何年龄在12岁以下的学生。如果学生不满足此约束，他们将不会被添加到表中。该表可以按如下方式创建：

```sql
CREATE TABLE STUDENTS (
    ADMISSION INT NOT NULL,
    NAME VARCHAR (15) NOT NULL,
    AGE INT NOT NULL CHECK (AGE >= 12),
    PRIMARY KEY (ADMISSION)
);
```

```sql
mysql> CREATE TABLE STUDENTS (
    -> ADMISSION INT NOT NULL,
    -> NAME VARCHAR (15) NOT NULL,
    -> AGE INT NOT NULL CHECK (AGE >= 12),
    -> PRIMARY KEY (ADMISSION)
    -> );
Query OK, 0 rows affected (0.57 sec)

mysql>
```

表已成功创建。

如果你已经创建了没有该约束的STUDENTS表，但后来需要实现它，请运行下面的命令：

```sql
ALTER TABLE STUDENTS
    MODIFY AGE INT NOT NULL CHECK (AGE >= 12);
```

该约束将成功添加到AGE列。

你也可以为约束指定一个名称。可以使用以下语法完成：

```sql
ALTER TABLE STUDENTS
    ADD CONSTRAINT checkAgeConstraint CHECK(AGE >= 12);
```

## 索引约束

索引帮助我们快速从数据库中检索数据。要创建索引，我们可以依赖数据库表中的一列或一组列。一旦创建了索引，系统会在排序数据之前为每一行分配一个ROWID。

```sql
mysql> ALTER TABLE STUDENTS
    ->        DROP INDEX age_idx;
Query OK, 1 row affected (0.13 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql>
```

## ALTER TABLE 命令

SQL为我们提供了ALTER TABLE命令，可用于添加、删除和修改表列。该命令还帮助我们向表添加和移除约束。

假设你有一个包含以下数据的STUDENTS表：

| ADMISSION | NAME | AGE |
| --- | --- | --- |
| 3420 | NICHOLAS | 10 |
| 1234 | john | 32 |
| 3456 | mercy | 23 |

```sql
mysql> ALTER TABLE STUDENTS ADD COURSE VARCHAR(10);
Query OK, 3 rows affected (0.15 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql>
```

当我们查询表的内容时，得到以下结果：

| ADMISSION | NAME | AGE | COURSE |
| --- | --- | --- | --- |
| 3420 | NICHOLAS | 10 | NULL |
| 1234 | john | 32 | NULL |
| 3456 | mercy | 23 | NULL |

这表明该列已被添加，并且每条记录在该列中被分配了一个NULL值。

要将COURSE列的数据类型从VarChar更改为Char，请执行以下命令：

```sql
ALTER TABLE STUDENTS MODIFY COLUMN COURSE Char(1);
```

```sql
mysql> ALTER TABLE STUDENTS MODIFY COLUMN COURSE Char(1);
Query OK, 3 rows affected (0.13 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql>
```

我们可以将ALTER TABLE命令与DROP TABLE命令结合使用。
