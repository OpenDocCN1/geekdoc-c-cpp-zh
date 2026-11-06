

## 如何使用 TOP 子句

TOP 子句允许您从数据表中检索指定数量或百分比的记录。

重要提示：某些数据库不兼容此子句。例如，MySQL 使用 LIMIT 来检索记录。

带有 TOP 子句的 SELECT 命令的语法如下：

```sql
SELECT TOP number|percent column_name(s)
FROM table_name
WHERE [condition]
```

## 如何对数据进行排序

SQL 提供了 ORDER BY 子句，该子句根据您用作基准的列，以降序或升序对数据进行排序。您应使用的语法如下：

```sql
SELECT column-list
FROM table_name
[WHERE condition]
[ORDER BY column1, column2, .. columnN] [ASC | DESC];
```

您可以在此子句中包含多个列。但是，请确保您想要使用的所有列都在 column-list 中。

## 如何混合多条 SELECT 命令的结果

在 SQL 中，您可以组合多条 SELECT 命令的结果，同时防止重复行。您只需使用 UNION 子句即可。

要使用此子句，您的 SELECT 语句应具有相同数量的选定列和列表达式。这些语句还必须具有相同的数据类型和列排列。但是，这些语句不需要具有相同的长度。

此子句的语法如下：

```sql
SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]

UNION

SELECT column1 [, column2 ]
FROM table1 [, table2 ]
[WHERE condition]
```

## 第8章：如何使用 SQL 组合记录

您可以使用 JOIN 子句来组合来自多个数据库的记录。基本上，JOIN 是一种可以组合不同表中字段的方法。

### JOIN 的不同类型

SQL 计算机语言支持不同类型的 JOIN。包括：

- SELF JOIN（自连接）——如果您想将表与自身连接，就像在处理不同的表一样，可以使用此连接。执行此操作时，您应该在 SQL 命令中至少重命名一个表。
- RIGHT JOIN（右连接）——此连接从右表中检索所有数据行。即使两个表之间不存在匹配项，SQL 也会完成此任务。
- LEFT JOIN（左连接）——此连接返回左表中的所有数据行。即使所涉及的表之间不存在匹配项，SQL 语言也会完成此操作。
- FULL JOIN（全连接）——如果其中一个表存在匹配项，此连接将检索数据行。
- INNER JOIN（内连接）——如果两个表都存在匹配项，则返回数据行。
- CARTESIAN JOIN（笛卡尔连接）——此连接从连接的表中检索记录集的笛卡尔值。

让我们详细讨论每种 JOIN：

### INNER JOIN（内连接）

这是 SQL 中最重要的连接之一。它通过混合不同表的列值生成一个新表。数据库查询会检查所有表的行，以确定是否存在满足连接谓词要求的行对。如果这些行对满足连接谓词，则将这些行的值放入新表中。以下是您应使用的语法：

```sql
SELECT table1.column1, table2.column2...
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

### LEFT JOIN（左连接）

此连接检索左表中的所有数据行。即使右表没有任何匹配项，SQL 也会执行此操作。因此，如果您的命令中的 ON 子句与右表有 0 个匹配项，您仍然会从该过程中获得一个数据行。但是，右表中的列将包含 NULL 值。

此连接的语法为：

```sql
SELECT table1.column1, table2.column2...
FROM table1
LEFT JOIN table2
ON table1.common_field = table2.common_field;
```

### RIGHT JOIN（右连接）

此连接返回右侧表中的所有数据行。即使左表没有任何匹配项，SQL 语言也会执行此操作。基本上，即使您的命令中的 ON 子句与左表没有匹配项，您仍然会从该过程中获得至少一个数据行。但是，左表中的列将包含 NULL 值。

此连接的语法为：

```sql
SELECT table1.column1, table2.column2...
FROM table1
RIGHT JOIN table2
ON table1.common_field = table2.common_field;
```

### FULL JOIN（全连接）

此 SQL 连接混合了左连接和右连接的结果。新表将包含两个表中的所有记录。以下是您应使用的语法：

```sql
SELECT table1.column1, table2.column2...
FROM table1
FULL JOIN table2
ON table1.common_field = table2.common_field;
```

重要提示：FULL JOIN 使用 NULL 值来填充不匹配的记录。

### SELF JOIN（自连接）

如果您想将表与自身连接，则应使用此连接。如前所述，您必须在 SQL 语句中至少重命名其中一个表。

此连接的语法为：

```sql
SELECT a.column_name, b.column_name...
FROM table1 a, table1 b
WHERE a.common_field = b.common_field;
```

### CARTESIAN JOIN（笛卡尔连接）

此连接从您使用的表中检索记录集的笛卡尔积。因此，SQL 用户将其视为连接条件始终为真的 INNER JOIN。CARTESIAN JOIN 的语法为：

```sql
SELECT table1.column1, table2.column2...
FROM table1, table2 [, table3 ]
```

## 结论

再次感谢您下载本书！

我希望本书能够帮助您在短短两周内学习 SQL 的基础知识。

下一步是使用这门计算机语言创建和管理您自己的数据库。

最后，如果您喜欢这本书，我想请您帮个忙，您能在亚马逊上为本书留下评论吗？那将不胜感激！

[点击此处为本书在亚马逊上留下评论！](#)

另外，请务必订阅我的技术和编程通讯，以获得免费书籍并了解更多关于如何编程的知识。[点击此处](#)。

谢谢您，祝您好运！

**_[点击此处获取使用 Bluehost 设置 Wordpress 站点的分步说明。](#)_**

## 附赠：获取更多由我撰写的免费书籍！

感谢您阅读我的书！我希望您从中获得了巨大的价值。为了表示感谢，我想为您提供更多免费书籍以及与编程和技术相关的信息！

只需点击下面的链接并在我的网站上输入您的电子邮件地址！

如果您认真想要提升您的编程技能，您将获得的所有内容都会对您有用。我将提供：

- 更多由我撰写的书籍
- 我是如何以创纪录的时间学会编程的
- 关于我最喜欢的编程相关产品的信息
- 以及更多！

[点击此处获取所有这些信息！](#)

如果您还没有查看过我的新网站 *KindleBookSpot.com*，请务必去看看。这是我一直在做的一个新项目，我真诚地希望它能对读者有价值。我创建这个网站是因为我想让大家更容易在一个地方找到最热门的特价 kindle 书籍。以下是我的网站所提供内容的一些详细信息：

- 畅销免费 kindle 书籍列表
- 折扣小说和非小说类书籍
- 每周一书
- 精选书籍
- 在我的网站上推广您自己的书

这个网站不仅面向读者，也是新兴作者在成为畅销书之前推广他们新书的地方。所以如果您想推广自己的书，请访问我的网站 *KindleBookSpot.com*。

我希望这个网站对您有用，也希望在那里见到您！

订阅我们在 KindleBookSpot 不断壮大的社区，以便在最优秀的书籍打折和免费时收到通知。

## 黑客训练营

## 学习计算机黑客的基础知识

*更多折扣书籍请访问 [kindlebookspot.com](https://kindlebookspot.com)*

## 目录

- 简介
- 第1章：黑客 – 一般信息
- 第2章：编程技能
- 第3章：密码
- 第5章：渗透测试
- 结论

## 简介

我想感谢并祝贺您下载了《*学习计算机黑客的基础知识（安全、渗透测试、如何黑客）*》这本书。

本书包含有关如何黑客计算机网络的经过验证的步骤和策略。

这本电子书将教您与黑客相关的基本思想和概念。它将解释经验丰富的黑客使用的工具、方法和技术。通过阅读这些材料，您可以对目标网络进行侦察和软件攻击。

再次感谢您下载本书，希望您喜欢！

