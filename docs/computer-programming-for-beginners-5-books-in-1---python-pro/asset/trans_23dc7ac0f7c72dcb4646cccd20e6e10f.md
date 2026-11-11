
好的。这些是我们之前提到的访问级别、隔离级别和诊断大小模式。

下面是一个 START TRANSACTION 命令的示例：

```sql
START TRANSACTION
    READ ONLY
    ISOLATION LEVEL SERIALIZABLE
    DIAGNOSTICS SIZE 10;
```

输入上述语法后，START TRANSACTION 将执行该语句及其操作。

### 设置约束

处理事务时，你可能会遇到工作情况与数据库中已建立的约束相冲突的场景。让我们举个例子。

假设你有一个包含 NOT NULL 约束的表。现在，当你处理该表时，你意识到在那个时间点可能没有值可以用来替代 NOT NULL 约束。但你又不能不在输入值的情况下离开。这迫使你向该列插入随机值。

为避免这种情况，你可以将约束定义为可延迟的。

此操作的语法如下所示：

```sql
SET CONSTRAINTS {constraint names} DEFERRED/IMMEDIATE
```

要指定多个约束名，需要用竖线将它们分隔开。例如：

```sql
(constraint_1 | constraint_2 | constraint_3)
```

然而，如果你希望选择所有约束——当数据库中有大量约束时，这可能很有用——那么你只需使用 ALL 一词。

下面是一个示例：

```sql
SET CONSTRAINTS ALL DEFERRED/IMMEDIATE
```

另一点需要注意的是，你不必同时指定 DEFERRED 和 IMMEDIATE。你必须选择适合当时活动的那个。

例如，如果你正在处理数据库，你会选择延迟约束，在这种情况下，你的语句应如下所示：

```sql
SET CONSTRAINTS ALL DEFERRED
```

完成数据库上的操作后，你可以选择应用更改。在这种情况下，语句将如下所示：

```sql
SET CONSTRAINTS ALL IMMEDIATE
```

因此，通过本章，你已经理解了 SQL 事务背后的思想，以及为什么它们在使用 SQL 编程时至关重要。

## 第 8 章：登录名、用户和角色

> “首先要看清设计是否明智而公正；一旦确定，就坚决执行。”——威廉·莎士比亚

### 服务器登录名

服务器登录名是在 SQL Server 中创建的用户账户，使用 SQL Server 身份验证，这需要输入密码和用户名才能登录到 SQL Server 实例。SQL Server 身份验证与 Windows 身份验证不同，因为 Windows 不会提示你输入密码。

可以授予这些登录名访问权限，使其能够登录到 SQL Server，但根据所分配的权限，它们不一定拥有数据库访问权限。还可以为它们分配某些服务器级角色，这些角色提供 SQL Server 内的某些服务器权限。

### 服务器级角色

服务器级角色将权限封装到登录名中。服务器级角色决定用户拥有哪些类型的权限。

预定义的服务器级角色有九种：

- Sysadmin——可在服务器上执行任何操作，本质上是最高访问级别。
- Serveradmin——可更改服务器配置并关闭 SQL Server。
- Securityadmin——如果用户有权访问数据库，则可授予（GRANT）、拒绝（DENY）和撤销（REVOKE）服务器级和数据库级权限。Securityadmin 还可以重置 SQL Server 密码。
- Processadmin——提供结束 SQL Server 实例中正在运行的进程的能力。
- Setupadmin——可通过使用 SQL 命令添加或删除链接服务器。
- Diskadmin——此角色用于管理 SQL Server 中的磁盘文件。
- Dbcreator——提供使用 DDL 语句的能力，例如 CREATE、ALTER、DROP，甚至 RESTORE 数据库。
- Public——所有登录名都属于‘public’角色；如果登录名没有特定的服务器或数据库对象权限，则会继承‘public’角色的权限。

如果你确实想更深入地探讨这个主题（当然，我鼓励你这样做），那就继续 [点击此链接](#)，通过 Microsoft 网站获取有关服务器角色的更多信息。

下面是一个可用于创建服务器登录名的语法示例。为登录名分配服务器级角色时，你可以将‘dbcreator’替换为上述任意角色。

你还会注意到，例如围绕‘master’和‘User Name’的方括号 []。这些是分隔标识符，我们之前已经讨论过。

- 首先，使用 master 数据库

  ```sql
  USE [master]
  GO
  ```

- 创建登录名——将 'User A' 替换为你想要使用的登录名

- 在 'Password' 字段中输入密码——建议使用强密码

- 同时为其提供默认数据库 'master'

  ```sql
  CREATE LOGIN [User A] WITH PASSWORD= N'123456',
  DEFAULT_DATABASE=[master]
  GO¹
  ```

创建一个登录名为 Server User 的用户。为此用户设置简单密码 123456，并授予其默认数据库‘master’的访问权限。

### 分配服务器角色

在 SQL Server 中，有几种不同的方法可以为用户登录名分配这些角色。其中一种选择是使用 Management Studio 中的界面，另一种是使用 SQL 语法。

下面是向用户授予特定服务器角色的语法。如果你还记得我们之前用来为‘User A’创建登录名的语法，那么下面这条语句将为‘User A’授予 dbcreator 服务器角色。

- 为用户登录名授予 'dbcreator' 角色（默认情况下它具有 public 角色）

  ```sql
  ALTER SERVER ROLE dbcreator ADD MEMBER [User A]
  GO
  ```

对于你上面创建的名为 Server User 的用户，为其授予 serveradmin 服务器角色。

成功完成练习后，你将收到一条消息，告知你的命令已成功完成。现在你可以使用该账户登录 SQL Server 了！

要登录，只需在对象资源管理器窗口中导航到‘连接对象资源管理器’按钮并单击它，以打开连接窗口。

![](img/239ff1e8a63502805c86c4dfbd71509a_196_0.png)

当登录窗口出现时，选择显示‘Windows 身份验证’的下拉菜单，并改选‘SQL Server 身份验证’。只需输入用户名和密码并登录即可！

![](img/239ff1e8a63502805c86c4dfbd71509a_197_0.png)

一旦你能够使用此用户登录，请尝试在对象资源管理器中打开数据库（系统数据库除外）。它应该看起来像下面这样；当你尝试展开某个数据库时，它反而会显示为空白。

### 对象资源管理器

连接

- HOME (SQL Server 13.0.4206 - HOME\jacob)
- HOME (SQL Server 13.0.4206 - User A)
  - 数据库
    - 系统数据库
    - 数据库快照
    - AdventureWorks2012
    - Company
    - ReportServer
    - ReportServerTempDB
    - Sample2
    - testdb
  - 安全性
  - 服务器对象
  - 复制
  - 管理

![](img/239ff1e8a63502805c86c4dfbd71509a_199_0.png)

你应当无法做到这一点，因为此用户没有任何数据库访问权限。我们将在下一节更详细地介绍这一点。

### 数据库用户

数据库用户通常是与登录名关联并映射到一个数据库或一组数据库的用户。此数据库用户的目的是提供对服务器自身内部数据库的访问权限。你还可以限制对其他数据库的访问。

在许多情况下，一个服务器实例上有多个数据库，而你并不希望将所有数据库的访问权限都授予所有用户。

### 数据库级角色

与服务器级角色非常相似，也有数据库级角色可以分配给用户，以控制其在特定数据库中的权限。

预定义的数据库角色有九种：

- Db_owner——提供在数据库上执行所有配置和维护作业的能力。此角色还允许用户 DROP 数据库——这是一条强大的命令！
- Db_securityadmin——提供修改角色成员身份和管理权限的能力。
- Db_accessadmin——提供为 Windows 登录名、Windows 组和 SQL 登录名添加或移除数据库访问权限的能力。
- Db_backupoperator——允许用户备份数据库。
- Db_ddladmin——提供在 SQL Server 中运行任何 DDL 语句的能力。
- Db_datawriter——提供在任何用户表中添加、删除或修改数据的能力。
- Db_datareader——提供查看用户表中任何数据的能力。
- Db_denydatawriter——不能在任何用户表中添加、删除或修改数据。
- db_denydatareader——不能查看用户表中的任何数据。

### 分配数据库角色和创建用户

与分配服务器角色和创建登录名一样，你可以使用 Management Studio 或 SQL 语法来创建数据库用户，并为该特定用户分配数据库级角色。你还可以将该用户映射到登录名，以便两者……
