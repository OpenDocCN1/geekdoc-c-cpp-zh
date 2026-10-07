
```sql
SELECT SUBTIME('01:15:23.000001', '8:12:15.003441');
```
Result: '-06:56:52.003440'

```sql
SELECT SUBTIME('01:15:23.000001', '-8:12:15.003441');
```
Result: '09:27:38.003442'

## 17.5 - CURRENT DATE

MySQL `CURRENT_DATE` 返回当前日期。如果 `CURDATE` 函数提供的信息不够，请使用此函数。

`CURRENT_DATE` 的语法如下：

```sql
CURRENT_DATE()
```

`CURRENT_DATE` 函数返回当前日期是 `CURDATE` 函数的同义词。如果在字符串上下文中使用，`CURRENT_DATE` 函数将以 `'YYYY-MM-DD'` 格式返回当前日期；如果在数字上下文中使用，则返回 `YYYYMMDD`。

以下是一些使用 `CURRENT_DATE` 的示例：

```sql
SELECT CURRENT_DATE();
```
Result: '2020-01-28'

```sql
SELECT CURRENT_DATE() + 0;
```
Result: 20200128

```sql
SELECT CURRENT_DATE() + 1;
```
Result: 20200129

## 17.6 - CURRENT TIMESTAMP

MySQL `CURRENT_TIMESTAMP` 函数返回当前日期和时间。如果 `NOW` 函数提供的信息不够，请使用此函数。

`CURRENT_TIMESTAMP` 的语法如下：

```sql
CURRENT_TIMESTAMP()
```

`CURRENT_TIMESTAMP`、`LOCALTIME` 和 `LOCALTIMESTAMP` 是 `NOW` 函数的同义词。如果在字符串上下文中使用，`CURRENT_TIMESTAMP` 函数将以 `'YYYY-MM-DD HH:MM:SS'` 格式返回当前日期和时间；如果在数字上下文中使用，则返回 `YYYYMMDDHMMSS`。

以下是一些使用 `CURRENT_TIMESTAMP` 的示例：

```sql
SELECT CURRENT_TIMESTAMP();
```
Result: '2020-01-28 13:48:41'

```sql
SELECT CURRENT_TIMESTAMP() + 0;
```
Result: 20200128134841

```sql
SELECT CURRENT_TIMESTAMP() + 1;
```
Result: 20200129134842

## 17.7 - DATE DIFF

MySQL `DATEDIFF` 函数返回两个日期值之间的天数差。

`DATEDIFF` 的语法如下：

```sql
DATEDIFF(date_1, date_2)
```

`date_1` and `date_2` – 要计算差值的两个日期。计算方式为 `date1- date2`，或 `date_1 MINUS date_2`

计算 只使用 `date_1` 和 `date_2` 的日期部分。`date_1` 和 `date_2` 的时间部分会被忽略。

以下是一些使用 `DATEDIFF` 的示例：

```sql
SELECT DATEDIFF('2020-01-28', '2020-01-27');
```
Result: 1

```sql
SELECT DATEDIFF('2020-01-28 11:41:14', '2020-01-27 12:10:08');
```
Result: 1

```sql
SELECT DATEDIFF('2020-01-28 11:41:14', '2020-01-27');
```
Result: 1

```sql
SELECT DATEDIFF('2020-02-15', '2020-02-10');
```
Result: 5

```sql
SELECT DATEDIFF('2020-01-28', '2019-12-31');
```
Result: 28

```sql
SELECT DATEDIFF('2019-12-31', '2020-01-28');
```
Result: -28

```sql
SELECT DATEDIFF(CURDATE(), '2020-02-14');
```
结果：当前日期与 `'2020-02-14'` 之间的差

## 17.8 - DAY

MySQL `DAY` 函数返回日期值中的日期部分。

`DAY` 的语法如下：

- `date_value` – 要从中提取日期的日期或日期时间值。

`DAY` 函数根据给定的日期值返回月份中的几几（1 到 31 之间的数字）。

`DAY` 函数是 `DAYOFMONTH` 函数的同义词。

以下是一些使用 `DAY` 的示例：

```sql
SELECT DAY('2020-01-28');
```
结果：28

```sql
SELECT DAY('2020-01-28 15:21:05');
```
结果：28

```sql
SELECT DAY('2020-10-15');
```
结果：15

```sql
SELECT DAY(CURDATE())
```
结果：这将返回当前日期。

## 17.9 - WEEK

MySQL `WEEK` 函数返回日期值中的周部分。

`WEEK` 的语法如下：

```sql
WEEK( date_value, mode )
```

- `date_value` – 要从中提取周的日期或日期时间值。
- `mode` – 这是一个可选参数。用于指定周从哪天开始。可以是以下值之一：

| Mode | 解释 | 返回 |
|---|---|---|
| 0 | 周的第一天是周日 | 0-53 |
| 1 | 周的第一天是周一，且第一周超过 3 天 | 0-53 |
| 2 | 周的第一天是周日 | 1-53 |
| 3 | 周的第一天是周一，且第一周超过 3 天 | 1-53 |
| 4 | 周的第一天是周日，且第一周超过 3 天 | 0-53 |
| 5 | 周的第一天是周一 | 0-53 |
| 6 | 周的第一天是周日，且第一周超过 3 天 | 1-53 |
| 7 | 周的第一天是周一 | 1-53 |

`WEEK` 函数将根据指定的 `mode` 返回 0-53 或 1-53 之间的值。

如果你运行的是 MySQL 4.0.14+ 且未指定 `mode`，`WEEK` 函数将使用系统变量 `default_week_format` 中的值作为 `mode`。

如果你运行的是比 4.0.14 更版本的 MySQL 且未指定 `mode`，`WEEK` 函数将使用 0 作为 `mode`。

以下是一些使用 `WEEK` 的示例：

```sql
SELECT WEEK('2020-01-01');
```
结果：0

```sql
SELECT WEEK('2020-04-20');
```
结果：16

```sql
SELECT WEEK('2020-07-16');
```
结果：28

```sql
SELECT WEEK('2020-10-15');
```
结果：41

```sql
SELECT WEEK(CURDATE());
```
结果：这将选择当前日期的周部分。

## 17.10 - MONTH

MySQL `MONTH` 函数返回日期值中的月份部分。

`MONTH` 的语法如下：

```sql
MONTH( date_value )
```

- `date_value` - 要从中提取月份的日期或日期时间值。

`MONTH` 函数根据给定的日期值返回月份（1 到 12 之间的数字）。

以下是一些使用 `MONTH` 的示例：

```sql
SELECT MONTH('2020-01-28');
```
结果：1

```sql
SELECT MONTH('2020-01-28 15:21:05');
```
结果：1

```sql
SELECT MONTH('2020-10-15');
```
结果：10

```sql
SELECT MONTH(CURDATE())
```
结果：这将选择当前日期的月份部分。

## 17.11 - YEAR

MySQL `YEAR` 函数返回日期值中的年份部分。

`YEAR` 的语法如下：

```sql
YEAR(date_value )
```
- `date_value` - 从从中提取年份的日期或日期时间值。

`YEAR` 函数根据日期值返回四位年份（1000 到 9999 之间的数字）。

以下是一些使用 `YEAR` 的示例：

```sql
SELECT YEAR('2020-01-28');
```
结果：2020

```sql
SELECT YEAR('2020-01-28 15:21:05');
```
结果：2020

```sql
SELECT YEAR('2015-10-15');
```
结果：2015

```sql
SELECT YEAR(CURDATE());
```
结果：这将选择当前日期的年份部分。

## 17.12 - TO_DAYS

MySQL `TO_DAYS` 函数将日期转换为天数。这是一个非常有用的函数。例如，我们可以使用 `TO_DAYS` 函数查看剩余多少天。

`TO_DAYS` 的语法如下：

```sql
TO_DAYS( date )
```
- `date` – 要转换为天数的日期。

`TO_DAYS` 函数用于格列哥日历内的日期。如果 `date` 为 `'0000-00-00'`，`TO_DAYS` 函数将返回 `NULL`。以下是一些使用 `TO_DAYS` 的示例：

```sql
SELECT TO_DAYS('2020-02-17');
```
结果：735246

```sql
SELECT TO_DAYS('2014-02-17');
```
结果：735246

```sql
SELECT TO_DAYS('2014-02-18');
```
结果：735247

```sql
SELECT TO_DAYS('2014-02-19 05:30:00');
```
结果：735248

```sql
SELECT TO_DAYS('0000-01-01');
```
结果：1

```sql
SELECT TO_DAYS('0000-00-00');
```
结果：NULL

## 第 18 章：项目项目

此项目整合了你通过这本书学到的信息。这将测试你对 MySQL 知识以及相关语法的掌握。让我们开始吧！

创建一个包含两个员工信息的数据库：

```sql
CREATE TABLE employee_info(
  EmployeeID int PRIMARY KEY,
  FirstName varchar(255),
  LastName varchar(255),
  Title varchar(255)
);
CREATE TABLE salary_info(
  EmployeeID int,
  SalaryYear int,
  SalaryValue float,
  PRIMARY KEY (EmployeeID,SalaryYear),
  FOREIGN KEY (EmployeeID) REFERENCES employee_info (EmployeeID)
);
```

主表应该是 `employee_info`，并包含 `EmployeeID`、`FirstName` 和 `Title`。第二张表应该是 `salary_info`，包含 `EmployeeID`、`SalaryYear` 和 `SalaryValue`（如果员工有多年的工资数据，则会有多行）。确定每个表中哪些列应该是主键和外键。

现在我们已经创建了表并定义了主键外键，我们需要向表中填充数据。首先，将行插入到 `employee_info` 表。它看起来如下：

```sql
INSERT INTO employee_info(EmployeeID, FirstName, LastName, Title)
VALUES (1,'John', 'Judge', 'Senior Manager'),
(2,'Aaron', 'Moore', 'Manager'),
(3,'Sally', 'Hunter', 'Administrative Assistant'),
(4,'Molly', 'Potter', 'CEO'),
(5,'Patricia', 'Culver', 'Analytics Consultant'),
(6,'Leo', 'Costa', 'Data Analyst'),
(7,'Ryan', 'Jetson', 'Human Resources Manager'),
(8,'Barbara', 'Henry', 'Analytics Consultant'),
(9,'Priscilla', 'Harrison', 'Manager'),
(10,'Alec', 'Flanders', 'Data Analyst');
```

接下来，将你的数据行插入到 `salary_info` 表。它应该类似于图片中的 SQL 命令：

```sql
INSERT INTO salary_info(EmployeeID, SalaryYear, SalaryValue)
VALUES
(1,2019,85700),
(2,2018,79000),
(3,2019,44000),
(4,2018,125600),
(5,2019,115000),
(6,2019,71000),
(7,2019,68200),
(8,2019,74700),
(9,2018,67000),
(10,2019,61500);
```

现在使用你创建的表完成以下任务！

1. 选择数据库中所有唯一的 `Title` 名称

![](img/989605394af9c1cd5a952af3b7bd1_1299_0.png)

2. 更新一个人获得年度加薪，将其最新一年的工资增加 10%

```sql
UPDATE salary_info
SET SalaryValue = SalaryValue*1.1
WHERE EmployeeID = 1 and SalaryYear = 2019
```

3. 确定数据库中今年所有员工的平均工资。创建一个存储过程，能够根据输入的年份进行此计算。

```sql
DELIMITER //
CREATE PROCEDURE avg_salary_by_year(
    IN year_of_salary int
)
BEGIN
    SELECT AVG(SalaryValue) FROM salary_info
    WHERE SalaryYear = year_of_salary;
END
DELIMITER //
```
调用 `avg_salary_by_year(2019)`;

| AVG(SalaryValue) |
|---|---|
| 77038.571428571433 |

4. 确定每个 `Title` 内在最新年份工资高于该平均水平的人数。

提示：将需要连接和子查询！

```sql
SELECT Title, COUNT(*) FROM employee_info as ei
INNER JOIN salary_info as si
ON ei.EmployeeID = si.EmployeeID
WHERE SalaryValue > (
  (SELECT AVG(SalaryValue) FROM salary_info
  WHERE SalaryYear = 2019)
)\AND SalaryYear = 2019
GROUP BY Title
```

| Title | COUNT(*) |
|---|---|
| Senior Manager | 1 |
| CEO | 1 |

## 18.1 结

恭喜你！如果你走了这一步，说明你已经掌握了令人印象深刻且基础的 MySQL 知识。你获得了一强大的技能，这些技能可以应用于许多领域、学科以及你自己的个人项目或业务。理解书中的这些概念将让你更深入地体会并理解数据在我们日常生活中所扮演的重要角色。现在，你可以成为这个全新的、革命性的数据驱动世界的一员了！
