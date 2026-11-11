
要从表中删除列。要从 STUDENTS 表中删除 COURSE 列，我们运行以下命令：

```
ALTER TABLE STUDENTS DROP COLUMN COURSE;
```

![](img/239ff1e8a63502805c86c4dfbd71509a_267_0.png)

然后，我们可以通过 describe 命令查看表详细信息，以确认该列是否已成功删除。

![](img/239ff1e8a63502805c86c4dfbd71509a_267_1.png)

上图显示该列已成功删除。

关于授权标识符。正如你在第二章所学，授权标识符是表示一个或多个可访问/修改数据库内信息的用户的对象。

## 更多参考资料

### MTA 98-364 认证

你可以在此处找到该认证的信息：[https://www.microsoft.com/en-us/learning/exam-98-364.aspx](https://www.microsoft.com/en-us/learning/exam-98-364.aspx)。到达该页面后，请务必展开“技能考核范围”部分中的主题，因为你在这些领域的数据库知识将会受到检验。

暂时就到这里。

## 参考文献

- 1keydata.com. (2019). *SQL - CREATE VIEW 语句 | 1Keydata。* [在线] 可访问于：https://www.1keydata.com/sql/sql-create-view.html [访问于 2019 年 2 月 3 日]。
- Chartio. (2019). *如何在 SQL Server 中将列从 Null 改为 Not Null。* [在线] 可访问于：https://chartio.com/resources/tutorials/how-to-alter-a-column-from-null-to-not-null-in-sql-server/ [访问于 2019 年 2 月 3 日]。
- Docs.microsoft.com. (2019). *主键和外键约束 - SQL Server。* [在线] 可访问于：https://docs.microsoft.com/en-us/sql/relational-databases/tables/primary-and-foreign-key-constraints?view=sql-server-2017 [访问于 2019 年 2 月 3 日]。
- Sites.google.com. (2019). *DDL 命令 - Create - Drop - Alter - Rename - Truncate - 编程语言。* [在线] 可访问于：https://sites.google.com/site/prgmr/sql/ddl-commands---create---drop---alter [访问于 2019 年 2 月 3 日]。
- Techonthenet.com. (2019). *SQL：UNION ALL 运算符。* [在线] 可访问于：https://www.techonthenet.com/sql/union_all.php [访问于 2019 年 2 月 3 日]。
- 1keydata.com. (2019). *SQL - RENAME COLUMN | 1Keydata。* [在线] 可访问于：https://www.1keydata.com/sql/alter-table-rename-column.html [访问于 2019 年 2 月 3 日]。
- Docs.microsoft.com. (2019). *创建检查约束 - SQL Server。* [在线] 可访问于：https://docs.microsoft.com/en-us/sql/relational-databases/tables/create-check-constraints?view=sql-server-2017 [访问于 2019 年 2 月 3 日]。
- Docs.microsoft.com. (2019). *创建主键 - SQL Server。* [在线] 可访问于：https://docs.microsoft.com/en-us/sql/relational-databases/tables/create-primary-keys?view=sql-server-2017 [访问于 2019 年 2 月 3 日]。
- Docs.microsoft.com. (2019). *删除表（数据库引擎）- SQL Server。* [在线] 可访问于：https://docs.microsoft.com/en-us/sql/relational-databases/tables/delete-tables-database-engine?view=sql-server-2017 [访问于 2019 年 2 月 3 日]。
- Docs.microsoft.com. (2019). *修改列（数据库引擎）- SQL Server。* [在线] 可访问于：https://docs.microsoft.com/en-us/sql/relational-databases/tables/modify-columns-database-engine?view=sql-server-2017 [访问于 2019 年 2 月 3 日]。
- query?, H., M, D., K., R., Singraul, D., Singh, A. and kor, p. (2019). *如何使用 SQL 查询更改表名？* [在线] Stack Overflow。可访问于：https://stackoverflow.com/questions/886786/how-to-change-a-table-name-using-an-sql-query [访问于 2019 年 2 月 3 日]。
- SQL Joins Explained. (2019). *SQL 连接类型 — SQL 连接详解*。 [在线] 可访问于：http://www.sql-join.com/sql-join-types/ [访问于 2019 年 2 月 3 日]。
- Techonthenet.com. (2019). *SQL：ALTER TABLE 语句*。 [在线] 可访问于：https://www.techonthenet.com/sql/tables/alter_table.php [访问于 2019 年 2 月 3 日]。
- Techonthenet.com. (2019). *SQL：GROUP BY 子句*。 [在线] 可访问于：https://www.techonthenet.com/sql/group_by.php [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL DEFAULT 约束*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-default.htm [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL INDEX 约束*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-index.htm [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL INNER JOIN*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-inner-joins.htm [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL LIKE 子句*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-like-clause.htm [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL NOT NULL 约束*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-not-null.htm [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). *SQL TOP、LIMIT 或 ROWNUM 子句*。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-top-clause.htm [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). *SQL INNER JOIN 关键字*。 [在线] 可访问于：https://www.w3schools.com/sql/sql_join_inner.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). *SQL LEFT JOIN 关键字*。 [在线] 可访问于：https://www.w3schools.com/sql/sql_join_left.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). *SQL NOT NULL 约束*。 [在线] 可访问于：https://www.w3schools.com/sql/sql_notnull.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). SQL PRIMARY KEY 约束。 [在线] 可访问于：https://www.w3schools.com/sql/sql_primarykey.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). SQL RIGHT JOIN 关键字。 [在线] 可访问于：https://www.w3schools.com/sql/sql_join_right.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). SQL UNION 运算符。 [在线] 可访问于：https://www.w3schools.com/sql/sql_union.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). SQL UNION 运算符。 [在线] 可访问于：https://www.w3schools.com/sql/sql_union.asp [访问于 2019 年 2 月 3 日]。
- W3schools.com. (2019). SQL UNIQUE 约束。 [在线] 可访问于：https://www.w3schools.com/sql/sql_unique.asp [访问于 2019 年 2 月 3 日]。
- www.tutorialspoint.com. (2019). SQL 主键。 [在线] 可访问于：https://www.tutorialspoint.com/sql/sql-primary-key.htm [访问于 2019 年 2 月 3 日]。

## ARDUINO 编程

### 学习 Arduino 编程的分步终极初学者指南

Ryan Turner

## © 版权所有 2019 - Ryan Turner - 保留所有权利。

未经作者或出版商的直接书面许可，不得复制、翻印或传播本书中包含的内容。

在任何情况下，出版商或作者均不对因本书所含信息而直接或间接导致的任何损害、赔偿或金钱损失承担任何责任或法律责任。

## 法律声明

本书受版权保护。本书仅供个人使用。未经作者或出版商同意，你不得修改、分发、销售、使用、引用或转述本书的任何部分或本书中的内容。

## 免责声明

请注意，本文档中包含的信息仅用于教育和娱乐目的。我们已尽一切努力提供准确、最新、可靠且完整的信息。我们不作任何明示或暗示的保证。读者知悉，作者不提供法律、财务、医疗或专业建议。本书中的内容来自各种来源。在尝试本书中概述的任何技术之前，请咨询持证专业人士。

阅读本文档即表示读者同意：在任何情况下，作者均不对因使用本文档中包含的信息而招致的任何直接或间接损失负责，包括但不限于——错误、遗漏或不准确之处。

## 目录

- [Arduino 简介](#introduction-to-arduino)
- [什么是 Arduino？](#what-is-arduino)
  - [Arduino 的历史](#history-of-arduino)
  - [但 Arduino 到底是什么？](#but-what-is-arduino)
  - [谁在使用 Arduino？](#who-uses-arduino)
- [Arduino 的 6 大优势](#the-6-advantages-of-arduino)
- [理解 Arduino 的关键术语](#key-terms-in-understanding-arduino)

