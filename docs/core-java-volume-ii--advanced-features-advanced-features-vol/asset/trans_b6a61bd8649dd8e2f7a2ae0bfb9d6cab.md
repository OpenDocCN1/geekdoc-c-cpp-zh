
| API | 版本 |
|---|---|
| `java.sql.SQLWarning` | 1.1 |

- `SQLWarning getNextWarning()`  
  返回链接到当前警告的下一个警告；如果已到警告链末尾，则返回 null。

| API | 版本 |
|---|---|
| `java.sql.Connection` | 1.1 |
| `java.sql.Statement` | 1.1 |
| `java.sql.ResultSet` | 1.1 |

- `SQLWarning getWarnings()`  
  返回待处理警告中的第一个；如果没有待处理的警告，则返回 null。

| API | 版本 |
|---|---|
| `java.sql.DataTruncation` | 1.1 |

- `boolean getParameter()`  
  如果数据截断适用于参数，则返回 true；如果适用于列，则返回 false。
- `int getIndex()`  
  返回被截断的参数或列的索引。
- `int getDataSize()`  
  返回本应传输的字节数；如果该值未知，则返回 -1。
- `int getTransferSize()`  
  返回实际传输的字节数；如果该值未知，则返回 -1。

## 5.4.4 填充数据库

我们现在准备编写第一个真正的 JDBC 程序。当然，尝试前面讨论过的一些复杂查询会很好，但我们有一个问题：目前数据库中没有数据。我们需要填充数据库，而一种简单的方法是使用一组 SQL 指令来创建表并向其中插入数据。大多数数据库程序可以处理来自文本文件的一组 SQL 指令，但在语句终止符和其他语法问题方面存在一些令人烦恼的差异。

因此，我们将在一个简单的程序中使用 JDBC，该程序读取包含 SQL 指令的文件（每行一条指令）并执行它们。

具体来说，该程序从文本文件中读取如下格式的数据

```sql
CREATE TABLE Publishers (Publisher_Id CHAR(6), Name CHAR(30), URL CHAR(80));
INSERT INTO Publishers VALUES ('Q201', 'Addison-Wesley', 'www.aw-bc.com');
INSERT INTO Publishers VALUES ('Q471', 'John Wiley & Sons', 'www.wiley.com');
. . . .
```

代码清单 5.2 包含该程序的代码，该程序读取包含 SQL 语句的文件并执行它们。你不必通读代码；只需使用该程序来填充数据库，并运行本章其余部分的示例。

确保数据库服务器正在运行，然后按如下方式运行程序：

```bash
java -classpath driverPath:. exec.ExecSQL Books.sql
java -classpath driverPath:. exec.ExecSQL Authors.sql
java -classpath driverPath:. exec.ExecSQL Publishers.sql
java -classpath driverPath:. exec.ExecSQL BooksAuthors.sql
```

在运行程序之前，请检查文件 database.properties 是否已针对你的环境正确设置（参见第 296 页的 5.3.5 节“连接到数据库”）。

> **注意：** 你的数据库可能还提供了一个直接读取 SQL 文件的工具。例如，使用 Derby 时，可以运行
>
> `java -jar derby/lib/derbyrun.jar ij -p ij.properties Books.sql`
>
> （ij.properties 文件在第 294 页的 5.3.3 节“启动数据库”中进行了说明。）
>
> 在 ExecSQL 命令的数据格式中，我们允许在每行末尾使用可选的分号，因为大多数数据库工具都期望这种格式。

以下步骤简要描述了 ExecSQL 程序：

- 1. 连接到数据库。getConnection 方法读取文件 database.properties 中的属性，并将 jdbc.drivers 属性添加到系统属性中。驱动程序管理器使用 jdbc.drivers 属性来加载相应的数据库驱动程序。getConnection 方法使用 jdbc.url、jdbc.username 和 jdbc.password 属性来打开数据库连接。
- 2. 打开包含 SQL 语句的文件。如果未提供文件名，则提示用户在控制台上输入语句。
- 3. 使用通用的 execute 方法执行每条语句。如果它返回 true，则该语句有一个结果集。我们为本书数据库提供的四个 SQL 文件都以 `SELECT *` 语句结尾，以便你可以看到数据已成功插入。
- 4. 如果有结果集，则打印出结果。由于这是一个通用结果集，我们需要使用元数据来查明结果有多少列。有关更多信息，请参见第 334 页的 5.8 节“元数据”。
- 5. 如果出现任何 SQL 异常，则打印该异常以及其中可能包含的任何链式异常。
- 6. 关闭与数据库的连接。

代码清单 5.2 显示了该程序的代码。

### **代码清单 5.2** `exec/ExecSQL.java`

```java
package exec;

import java.io.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;
import java.sql.*;

/**
 * Executes all SQL statements in a file. Call this program as <br>
 * java -classpath driverPath:. ExecSQL commandFile
 *
 * @version 1.33 2018-05-01
 * @author Cay Horstmann
 */
class ExecSQL
{
   public static void main(String args[]) throws IOException
   {
      try (Scanner in = args.length == 0 ? new Scanner(System.in)
            : new Scanner(Paths.get(args[0]), StandardCharsets.UTF_8))
      {
         try (Connection conn = getConnection();
               Statement stat = conn.createStatement())
         {
            while (true)
            {
               if (args.length == 0) System.out.println("Enter command or EXIT to exit:");

               if (!in.hasNextLine()) return;

               String line = in.nextLine().trim();
               if (line.equalsIgnoreCase("EXIT")) return;
               if (line.endsWith(";")) // remove trailing semicolon
                  line = line.substring(0, line.length() - 1);
               try
               {
                  boolean isResult = stat.execute(line);
                  if (isResult)
                  {
                     try (ResultSet rs = stat.getResultSet())
                     {
                        showResultSet(rs);
                     }
                  }
                  else
                  {
                     int updateCount = stat.getUpdateCount();
                     System.out.println(updateCount + " rows updated");
                  }
               }
               catch (SQLException e)
               {
                  for (Throwable t : e)
                     t.printStackTrace();
               }
            }
         }
         catch (SQLException e)
         {
            for (Throwable t : e)
               t.printStackTrace();
         }
      }
   }

   /**
    * Gets a connection from the properties specified in the file database.properties
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

   /**
    * Prints a result set.
    * @param result the result set to be printed
    */
   public static void showResultSet(ResultSet result) throws SQLException
   {
      ResultSetMetaData metaData = result.getMetaData();
      int columnCount = metaData.getColumnCount();

      for (int i = 1; i <= columnCount; i++)
      {
         if (i > 1) System.out.print(", ");
         System.out.print(metaData.getColumnLabel(i));
      }
      System.out.println();

      while (result.next())
      {
         for (int i = 1; i <= columnCount; i++)
         {
            if (i > 1) System.out.print(", ");
            System.out.print(result.getString(i));
         }
         System.out.println();
      }
   }
}
```

## 5.5 查询执行

在本节中，我们编写一个针对 COREJAVA 数据库执行查询的程序。要使该程序正常工作，你必须拥有一个已按上一节所述填充了表的 COREJAVA 数据库。

查询数据库时，你可以选择作者和出版商，或者将其中任意一个保留为 Any。

你还可以更改数据库中的数据。选择一个出版商并输入一个金额。该出版商的所有价格都会按你输入的金额进行调整，并且程序会显示更改了多少行。更改价格后，你可能想运行一个查询来验证新价格。

