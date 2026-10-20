

## 可移植性提示 28.7

根据 Java API 文档中关于 CallableStatement 接口的说明，为了在数据库系统之间获得最大的可移植性，程序应在获取任何输出参数的值之前，先处理从 CallableStatement 返回的更新计数（表示已更新行数）或 ResultSet。

## 28.13 事务处理

许多数据库应用程序需要保证一系列数据库插入、更新和删除操作在应用程序继续处理下一个数据库操作之前正确执行。例如，当您在银行账户之间进行电子转账时，有多个因素决定交易是否成功。您首先指定源账户以及希望从该账户转入目标账户的金额。接下来，您指定目标账户。银行检查源账户以确定其资金是否足以完成转账。如果足够，银行将提取指定金额，并且如果一切顺利，则将其存入目标账户以完成转账。如果银行从源账户取款后转账失败，会发生什么？在正规的银行系统中，银行会将资金重新存入源账户。如果资金从您的源账户中被扣除而银行未将资金存入目标账户，您会作何感想？

事务处理使与数据库交互的程序能够将一个数据库操作（或一组操作）视为单个操作。这样的操作也称为原子操作或事务。在事务结束时，可以决定提交事务或回滚事务。提交事务会将数据库操作最终确定；作为事务的一部分执行的所有插入、更新和删除操作，在不进行新的数据库操作的情况下无法撤销。回滚事务会使数据库恢复到该数据库操作之前的状态。当事务的一部分未能正确完成时，这很有用。在我们讨论的银行账户转账示例中，如果无法将存款存入目标账户，则事务将被回滚。

Java 通过接口 Connection 的方法提供事务处理。方法 setAutoCommit 指定每条 SQL 语句是在完成后提交（参数为 true），还是将多条 SQL 语句分组为一个事务（参数为 false）。如果 setAutoCommit 的参数为 false，则程序必须在事务的最后一条 SQL 语句之后调用 Connection 方法 commit（将更改提交到数据库）或 Connection 方法 rollback（将数据库恢复到事务之前的状态）。接口 Connection 还提供方法 getAutoCommit 来确定该 Connection 的自动提交状态。

## 28.14 本章回顾

在本章中，您学习了基本的数据库概念、如何使用 SQL 查询和操作数据库中的数据，以及如何使用 JDBC 让 Java 应用程序与 MySQL 和 Java DB 数据库交互。您学习了 SQL 命令 SELECT、INSERT、UPDATE 和 DELETE，以及 WHERE、ORDER BY 和 INNER JOIN 等子句。您学习了获取数据库 Connection、创建与数据库数据交互的 Statement、执行语句和处理结果的步骤。然后您使用了 RowSet 来简化连接数据库和创建语句的过程。您使用 PreparedStatement 创建预编译的 SQL 语句。您还学习了如何使用预定义的 SQL 脚本在 MySQL 和 Java DB 中创建和配置数据库。我们还概述了 CallableStatement 和事务处理。在下一章中，您将学习使用 JavaServer Faces 进行 Web 应用程序开发。

## 28.15 网络资源

www.oracle.com/technetwork/java/javadb/overview/index.html
Oracle Java DB 主页。

db.apache.org/derby/papers/DerbyTut/index.html
Apache Derby 教程。包括 Linux 安装说明。

download.oracle.com/javase/tutorial/jdbc/index.html
Java Tutorial 的 JDBC 专题。

www.sql.org
该 SQL 门户网站提供了许多资源的链接，包括 SQL 语法、技巧、教程、书籍、杂志、讨论组、提供 SQL 服务的公司、SQL 顾问和免费软件。

download.oracle.com/javase/6/docs/technotes/guides/jdbc/index.html
Oracle JDBC API 文档。

www.mysql.com
该网站是 MySQL 数据库主页。您可以下载最新版本的 MySQL 和 MySQL Connector/J，并访问其在线文档。

dev.mysql.com/doc/refman/5.5/en/index.html
MySQL 参考手册。

download.oracle.com/javase/6/docs/technotes/guides/jdbc/getstart/rowsetImpl.html
概述 RowSet 接口及其子接口。该网站还讨论了 Sun 对这些接口的参考实现及其用法。

## 总结

### 28.1 节 引言

- 数据库（第1172页）是数据的集成集合。数据库管理系统（DBMS；第1172页）提供了存储、组织、检索和修改数据的机制。
- 当今最流行的数据库管理系统是关系数据库（第1173页）系统。
- SQL（第1172页）是用于查询（第1172页）和操作关系数据的国际标准语言。
- 程序通过接口连接到关系数据库并与之交互——接口是促进数据库管理系统与程序之间通信的软件。
- JDBC 驱动程序（第1172页）使 Java 应用程序能够连接到特定 DBMS 中的数据库，并允许您检索和操作数据库数据。

### 28.2 节 关系数据库

- 关系数据库（第1173页）将数据存储在表（第1173页）中。表由行（第1173页）组成，行由存储值的列组成。
- 表的主键（第1173页）提供唯一的值，在各行之间不能重复。
- 表的每一列（第1173页）表示一个不同的属性。

ON 子句（第1183页）指定要比较的各表中的列，以确定哪些行被连接。如果 SQL 语句使用多个表中同名的列，则必须通过在列名前加上表名和一个点（.）来完全限定（第1183页）这些列名。

### 28.4.5 节 INSERT 语句

- INSERT 语句（第1184页）向表中插入新行。该语句的基本形式为

  INSERT INTO tableName ( columnName1, columnName2, ..., columnNameN )
  VALUES ( value1, value2, ..., valueN )

  其中 tableName 是要插入行的表。tableName 后跟圆括号内以逗号分隔的列名列表。列名列表后跟 SQL 关键字 VALUES（第1184页）和圆括号内以逗号分隔的值列表。
- SQL 使用单引号（'）来分隔字符串。要在 SQL 中指定包含单引号的字符串，请用另一个单引号转义单引号（即''）。

### 28.4.6 节 UPDATE 语句

- UPDATE 语句（第1185页）修改表中的数据。UPDATE 语句的基本形式为

  UPDATE tableName
  SET columnName1 = value1, columnName2 = value2, ..., columnNameN = valueN
  WHERE criteria

  其中 tableName 是要更新的表。关键字 SET（第1185页）后跟以逗号分隔的 columnName = value 对列表。可选的 WHERE 子句确定要更新的行。

### 28.4.7 节 DELETE 语句

- DELETE 语句（第1186页）从表中删除行。DELETE 语句的最简单形式为

  DELETE FROM tableName WHERE criteria

  其中 tableName 是要从中删除一行（或多行）的表。可选的 WHERE criteria 确定要删除的行。如果省略该子句，则删除表中的所有行。

### 28.8.1 节 连接到数据库并查询

- java.sql 包中包含用于在 Java 中访问关系数据库的类和接口。
- Connection 对象（第1191页）管理 Java 程序与数据库之间的连接。Connection 对象使程序能够创建访问数据的 SQL 语句。
- DriverManager（第1191页）的 getConnection 方法（第1191页）尝试连接到指定 URL 的数据库，该 URL 指定通信协议、通信子协议（第1191页）和数据库名称。
- Connection 的 createStatement 方法（第1192页）创建 Statement 对象（第1192页），该对象可用于向数据库提交 SQL 语句。
- Statement 的 executeQuery 方法（第1192页）执行查询并返回 ResultSet 对象（第1192页）。ResultSet 方法使程序能够操作查询结果。
- ResultSetMetaData 对象（第1192页）描述 ResultSet 的内容。程序可以以编程方式使用元数据来获取有关 ResultSet 列名和类型的信息。
- ResultSetMetaData 的 getColumnCount 方法（第1192页）检索 ResultSet 的列数。
- ResultSet 的 next 方法（第1193页）将 ResultSet 游标定位到下一行，如果该行存在则返回 true；否则返回 false。由于游标最初位于第一行之前，因此必须调用此方法才能开始处理 ResultSet。

