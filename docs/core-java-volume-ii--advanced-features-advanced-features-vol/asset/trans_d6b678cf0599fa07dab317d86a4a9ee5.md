

**表 5.5** 常见 SQL 数据类型

| 数据类型 | 描述 |
| --- | --- |
| INTEGER 或 INT | 通常为 32 位整数 |
| SMALLINT | 通常为 16 位整数 |
| NUMERIC(*m*,*n*)、DECIMAL(*m*,*n*) 或 DEC(*m*,*n*) | 定点十进制数，共 *m* 位数字，小数点后 *n* 位数字 |
| FLOAT(*n*) | 具有 *n* 位二进制精度的浮点数 |
| REAL | 通常为 32 位浮点数 |
| DOUBLE | 通常为 64 位浮点数 |
| CHARACTER(*n*) 或 CHAR(*n*) | 长度为 *n* 的定长字符串 |
| VARCHAR(*n*) | 最大长度为 *n* 的变长字符串 |
| BOOLEAN | 布尔值 |
| DATE | 日历日期，取决于具体实现 |
| TIME | 一天中的时间，取决于具体实现 |
| TIMESTAMP | 日期和一天中的时间，取决于具体实现 |
| BLOB | 二进制大对象 |
| CLOB | 字符大对象 |

## 5.3 JDBC 配置

当然，你需要一个可获取 JDBC 驱动程序的数据库程序。有许多优秀的选择，例如 IBM DB2、Microsoft SQL Server、MySQL、Oracle 和 PostgreSQL。

你还必须创建一个供实验使用的数据库。我们假设将其命名为 `COREJAVA`。请创建一个新数据库，或者让数据库管理员创建一个具有相应权限的数据库。你需要能够在数据库中创建、更新和删除表。

如果你以前从未安装过客户端/服务器数据库，可能会发现设置数据库有些复杂——诊断失败原因可能很困难。如果你的设置无法正常工作，最好寻求专家帮助。

如果这是你第一次使用数据库，我们建议你使用 Apache Derby 数据库，可从 [http://db.apache.org/derby](http://db.apache.org/derby) 获取。

如果你的驱动程序的 JAR 文件不支持自动注册，你需要查明供应商使用的 JDBC 驱动程序类的名称。典型的驱动程序名称为

```
org.apache.derby.jdbc.ClientDriver
org.postgresql.Driver
```

有两种方法可以向 DriverManager 注册驱动程序。一种方法是在 Java 程序中加载驱动程序类。例如，

```java
Class.forName("org.postgresql.Driver"); // force loading of driver class
```

该语句会加载驱动程序类，从而执行注册驱动程序的静态初始化器。

或者，你可以设置 jdbc.drivers 属性。你可以通过命令行参数指定该属性，例如

```
java -Djdbc.drivers=org.postgresql.Driver ProgramName
```

或者，你的应用程序可以通过如下调用设置系统属性

```java
System.setProperty("jdbc.drivers", "org.postgresql.Driver");
```

你也可以提供多个驱动程序；用冒号分隔它们，例如：

```
org.postgresql.Driver:org.apache.derby.jdbc.ClientDriver
```

### 5.3.5 连接数据库

在 Java 程序中，像这样打开数据库连接：

```java
String url = "jdbc:postgresql:COREJAVA";
String username = "dbuser";
String password = "secret";
Connection conn = DriverManager.getConnection(url, username, password);
```

驱动程序管理器会遍历已注册的驱动程序，以找到一个能够使用数据库 URL 中指定子协议的驱动程序。

getConnection 方法返回一个 Connection 对象。在接下来的几节中，你将看到如何使用 Connection 对象执行 SQL 语句。

要连接数据库，你需要数据库的用户名和密码。

> **注意：** 默认情况下，Derby 允许使用任意用户名连接，并且不检查密码。会为每个用户生成一组单独的表。默认用户名为 app。

清单 5.1 中的测试程序运用了这些步骤。它从名为 `database.properties` 的文件中加载连接参数，并连接到数据库。示例代码随附的 `database.properties` 文件包含 Derby 数据库的连接信息。如果你使用不同的数据库，请将特定于你的数据库的连接信息放入该文件。以下是连接 PostgreSQL 数据库的示例：

```
jdbc.drivers=org.postgresql.Driver
jdbc.url=jdbc:postgresql:COREJAVA
jdbc.username=dbuser
jdbc.password=secret
```

连接到数据库后，测试程序会执行以下 SQL 语句：

```
CREATE TABLE Greetings (message CHAR(20))
INSERT INTO Greetings VALUES ('Hello, World!')
SELECT * FROM Greetings
```

SELECT 语句的结果会被打印出来，你应该会看到如下输出

```
Hello, World!
```

然后通过执行以下语句删除该表

```
DROP TABLE Greetings
```

要运行此测试，请如前所述启动数据库，并按如下方式启动程序

```
java -classpath .;driverJAR test.TestDb
```

（一如既往，Windows 用户需要使用 ; 而不是 : 来分隔路径元素。）

> **提示：** 调试 JDBC 相关问题的一种方法是启用 JDBC 跟踪。调用 `DriverManager.setLogWriter` 方法将跟踪消息发送到 `PrintWriter`。跟踪输出包含 JDBC 活动的详细列表。大多数 JDBC 驱动程序实现都提供了额外的跟踪机制。例如，使用 Derby 时，你可以向 JDBC URL 添加 `traceFile` 选项：`jdbc:derby://localhost:1527/COREJAVA;create=true;traceFile=trace.out`。

| API | 版本 |
|---|---|
| `java.sql.DriverManager` | 1.1 |

- `static Connection getConnection(String url, String user, String password)` 建立到给定数据库的连接，并返回一个 `Connection` 对象。

### 清单 5.1  `test/TestDB.java`

```java
package test;

import java.nio.file.*;
import java.sql.*;
import java.io.*;
import java.util.*;

/**
 * This program tests that the database and the JDBC driver are correctly configured.
 * @version 1.03 2018-05-01
 * @author Cay Horstmann
 */
public class TestDB
{
   public static void main(String args[]) throws IOException
   {
      try
      {
         runTest();
      }
      catch (SQLException ex)
      {
         for (Throwable t : ex)
            t.printStackTrace();
      }
   }

   /**
    * Runs a test by creating a table, adding a value, showing the table contents, and
    * removing the table.
    */
   public static void runTest() throws SQLException, IOException
   {
      try (Connection conn = getConnection();
         Statement stat = conn.createStatement())
      {
         stat.executeUpdate("CREATE TABLE Greetings (Message CHAR(20))");
         stat.executeUpdate("INSERT INTO Greetings VALUES ('Hello, World!')");

         try (ResultSet result = stat.executeQuery("SELECT * FROM Greetings"))
         {
            if (result.next())
               System.out.println(result.getString(1));
         }
         stat.executeUpdate("DROP TABLE Greetings");
      }
   }

    /**
     * Gets a connection from the properties specified in the file database.properties.
     * @return the database connection
     */
    public static Connection getConnection() throws SQLException, IOException
    {
        var props = new Properties();
        try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
        {
            props.load(in);
        }
        String drivers = props.getProperty("jdbc.drivers");
        if (drivers != null) System.setProperty("jdbc.drivers", drivers);
        String url = props.getProperty("jdbc.url");
        String username = props.getProperty("jdbc.username");
        String password = props.getProperty("jdbc.password");

        return DriverManager.getConnection(url, username, password);
    }
}
```

## 5.4 使用 JDBC 语句

在接下来的几节中，你将看到如何使用 JDBC Statement 执行 SQL 语句、获取结果并处理错误。然后我们会向你展示一个用于填充数据库的简单程序。

### 5.4.1 执行 SQL 语句

要执行 SQL 语句，首先创建一个 Statement 对象。要创建语句对象，请使用通过调用 DriverManager.getConnection 获得的 Connection 对象。

```
    Statement stat = conn.createStatement();
```

接下来，将要执行的语句放入一个字符串中，例如：

```
    String command = "UPDATE Books"
        + " SET Price = Price - 5.00"
        + " WHERE Title NOT LIKE \"%Introduction%\"";
```

然后，调用 Statement 接口的 executeUpdate 方法：

```
    stat.executeUpdate(command);
```

executeUpdate 方法返回受 SQL 语句影响的行数；对于不返回行数的语句，则返回零。对于

