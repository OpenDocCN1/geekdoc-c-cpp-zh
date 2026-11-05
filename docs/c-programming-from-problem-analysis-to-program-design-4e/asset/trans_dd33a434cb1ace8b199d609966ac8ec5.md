
数据库字段标识符的名称中不能包含空格。如果数据库表的字段名含有空格，那么在 SQL 语句中该字段名必须用方括号括起来，如 [Phone Number]。

WHERE 子句的一般格式如下：

```sql
WHERE columnName = value
```

复合表达式可以使用 AND、OR 或 NOT 进行组合。关系运算符也可以与 WHERE 子句一起使用，包括 >、<、>=、<=，以及用于相等判断的单个等号。要测试“不等于”，使用 <>。要编写条件表达式来判断某个值是否在指定范围内，可以在第一个值之前插入关键字 BETWEEN。复合表达式 AND 用于连接两个值。要将日期作为值，在 Microsoft Access 中日期值需要用 # 符号括起来。如前所述，数据库管理系统使用的方言略有不同。Microsoft SQL Server 使用单引号作为日期的分隔符，而不是 # 符号，如下所示：

```sql
WHERE (aDate BETWEEN #10/12/2012# AND #10/12/2013#)--Access
WHERE (aDate BETWEEN '10/12/2012' AND '10/12/2013')--SQL Server
```

除了使用单个表选择数据进行查看外，您还可以使用 SELECT 语句通过公共字段连接多个表来检索结果。组合表的一种方式是使用 SQL JOIN 子句。JOIN 查询将一个表的列与另一个表的列组合起来，创建一个单一的表，将一个表的列与另一个表的列进行匹配。JOIN 查询不会改变任何一个表，而是临时组合每个表中的数据，使其作为一个单一表进行查看。JOIN 语句的一种类型是 INNER JOIN。

与 SELECT 语句一起使用的 INNER JOIN 返回两个表中所有匹配的行。如果一个表中的行在另一个表中没有匹配项，则不会返回这些行。要使用 JOIN 子句，需要指定应从两个表中返回的列。它们的名称以表名为前缀，并用点分隔。不是使用 WHERE 子句来标识要返回的行，而是将关键字 INNER JOIN 和 ON 与两个表一起使用。假设有一个名为 departmentTable 的第二个表，包含 major_ID、major_Name 和 major_Chair 列；示例14-6展示了如何连接这两个表。

### 示例14-6

```sql
SELECT memberTable.FirstName, memberTable.LastName,
departmentTable.major_Name
FROM memberTable INNER JOIN departmentTable ON
memberTable.major_ID = departmentTable.major_ID;
```

通常，用于连接的列是两个表中的主键和/或外键。因此，major_ID 需要出现在两个表中。它将在 memberTable 中作为外键。在示例14-6中，department 的主键是 major_ID。两个表中具有公共字段使得这两个表能够被链接。

> **注意** **主键**是唯一标识表中一行的一列（字段）或多列组合。**外键**是指向另一个表中某一列的列。外键用于链接两个表。

您可以选择希望从两个表中返回的列。不必返回用于链接表的键。但是，许多应用程序会受益于检索键列以供后续使用。在此示例中，从 memberTable 返回两列（FirstName 和 LastName），从 departmentTable 返回一列（major_Name）。

SQL 语句也可以用于创建表，或者插入、删除和更新表中的数据。当您使用 ADO.NET 时，能够编写 SQL 语句非常有用。要向表中插入值，请使用 SQL INSERT INTO 子句，后跟表名以及您有值的列。VALUES 关键字与括号中的新值列表一起使用，如示例14-7所示。

### 示例14-7

```sql
INSERT INTO memberTable(StudentID, FirstName, LastName, PhoneNumber)
VALUES (1123, 'Kathy', 'Weizel', 2345678);
```

SQL DELETE 关键字用于删除表中的行。要标识要删除的行，请使用 FROM 和 WHERE 子句。示例14-8演示了从图14-1所示的表中删除最后一条记录。

### 示例14-8

```sql
DELETE FROM memberTable
WHERE (StudentID = 1299);
```

最后一个示例演示如何编写 SQL UPDATE 语句。通常使用 SET 和 WHERE 子句来标识要更改的行和值。回到图14-1，要将 Rachel Smith 的姓氏改为 Hakim，您可以编写如示例14-9所示的 UPDATE SQL 语句。

### 示例14-9

```sql
UPDATE memberTable
SET LastName = 'Hakim'
WHERE (StudentID = 1234);
```

SQL 本身是一种非常强大的编程语言。为了充分利用 ADO 类和 Visual Studio 的工具，了解 SQL 语句是很有帮助的。关于这个主题有很多书籍。鼓励您探索和学习编写 SQL 语句的语法要求。在互联网上使用您喜欢的搜索引擎，您会发现许多与 SQL 相关的文章、教程和参考资料。

本章不讨论通过 Web 使用 SQL 直通查询访问数据库记录所涉及的数据库安全问题。允许用户直接为查询数据库表的参数提供值的应用程序容易受到黑客入侵和攻击。例如，SQL 注入攻击涉及键入或插入实际的 SQL 查询或命令作为输入（而不是所请求的值，例如用户登录名），从而获得对表的访问权限，然后窃取或破坏数据。使用您喜欢的搜索引擎查找有关 SQL 注入攻击的信息。在撰写本文时，以下站点提供了有关如何保护您的代码和数据库免受入侵者攻击的建议。

- 在它们阻止你之前阻止SQL注入攻击—http://msdn.microsoft.com/en-us/magazine/cc163917.aspx
- SQL注入攻击—www.unixwiz.net/techtips/sql-injection.html

## 处理数据

通过 SQL 查询检索数据后，可以使用几个类来处理数据。您可以在内存中一次检索一条记录，并在检索另一条记录之前处理该记录，或者将查询的整个结果存储在类似数组的临时数据结构中，并与数据库断开连接。

对于简单的只读数据库访问，ADO.NET 包含一个数据读取器类，可用于从数据库读取数据行。与连接类和命令类一样，每个数据提供程序在其命名空间中定义了不同的数据读取器类。用于访问 OleDb 提供程序的数据读取器类是 OleDbDataReader 类。SqlDataReader 类用于 SQL Server 数据库。

### 使用数据读取器检索数据

OleDbDataReader 和 SqlDataReader 类允许对数据库进行只读的向前数据检索。结果在查询执行时返回。使用数据读取器，您可以按顺序循环遍历查询结果。当您需要检索大量数据时，这是访问数据库中数据的一个特别好的选择。数据不会缓存在内存中。默认情况下，使用这些数据读取器类时，每次只在内存中存储一行。下面的讨论重点介绍 OleDbDataReader 类；但是，这些概念同样适用于 SqlDataReader 类。

要使用数据读取器处理数据，您需要声明一个 OleDbDataReader 类的对象，然后调用 ExecuteReader( ) 方法。OleDbCommand 类的 ExecuteReader( ) 方法用于构建 OleDbDataReader 对象。您在前一节中看到，OleDbCommand 对象包含 SQL 命令和表示数据提供程序的连接字符串。

要将 OleDbDataReader 对象定位到第一个检索到的查询结果的行，可以使用 OleDbDataReader 类的 Read( ) 方法。Read( ) 方法也用于在处理完前一条记录后前进到下一条记录。要理解使用 Read( ) 方法检索数据的过程，您可以将使用数据读取器对象单次访问所检索到的内容视为一个一维表，由该行的字段组成。可以使用表示字段在记录中物理位置的实际序号索引来引用这些字段，就像您对一维数组进行索引一样。因此，使用图14-1中所示的数据库表，当您编写 dbReader[0] 时，对名为 dbReader 的数据读取器对象第一次调用 Read( ) 方法会引用值“1234”。dbReader[1] 引用“Rachel”，dbReader[2] 引用“Smith”，或者如果您使用示例14-9中演示的 UPDATE 命令更改了记录，则引用“Hakim”。

您还可以使用表的字段名作为数据读取器对象的索引。如果数据库中的表包含名为 StudentID、FirstName、LastName 和 PhoneNumber 的字段，如图14-1所示，那么当 dbReader 被实例化为 OleDbDataReader 类的对象时，dbReader[1] 引用名字，dbReader["FirstName"] 也引用名字。因此，除了使用序号位置提取值之外，您还可以使用单独的数据库字段名（如 LastName）来提取值。这有时更方便，并能使代码更易读。但是，使用序号索引检索更快。

> **注意**
>
> 当写入 dbReader["StudentID"] 时，第一次调用 dbReader.Read( ) 指的是值 1234。dbReader["FirstName"] 指的是“Rachel”。您应该注意，当您使用字段名作为索引器时，字段名必须用双引号括起来。

除了通过索引访问数据之外，OleDbDataReader 类还包含许多类型化访问器方法成员。传递给每个方法的参数是数据字段的序号位置，或列号（第一列为列 0）。这些方法中的每一个都返回指定类型的值。如果您不使用这些方法，则必须执行额外的步骤，即将返回的对象转换为其正确的数据类型。表14-6列出了 OleDbDataReader 类的一些类型化访问器方法和其他成员。

