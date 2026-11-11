

> **注意：** JDK 中包含的 Apache Derby 版本正式名称是 JavaDB。我们认为这并不特别有用，在本章中我们将称它为 Derby。

在编写第一个数据库程序之前，你需要准备一些事项。以下各节将介绍这些事项。

### 5.3.1 数据库 URL

连接数据库时，必须使用各种特定于数据库的参数，例如主机名、端口号和数据库名。

JDBC 使用类似于普通 URL 的语法来描述数据源。以下是该语法的示例：

```
jdbc:derby://localhost:1527/COREJAVA;create=true
jdbc:postgresql:COREJAVA
```

这些 JDBC URL 指定了一个 Derby 数据库和一个名为 COREJAVA 的 PostgreSQL 数据库。

通用语法为

```
jdbc:subprotocol:other stuff
```

其中子协议选择用于连接数据库的特定驱动程序。

*其他内容*参数的格式取决于所使用的子协议。你需要查阅供应商的文档以了解具体格式。

### 5.3.2 驱动程序 JAR 文件

你需要获取包含数据库驱动程序所在的 JAR 文件。如果使用 Derby，则需要文件 `derbyclient.jar`。使用其他数据库时，你需要找到相应的驱动程序。例如，PostgreSQL 驱动程序可从 http://jdbc.postgresql.org 获取。

运行访问数据库的程序时，请将驱动程序 JAR 文件包含在类路径中。（编译时不需要该 JAR 文件。）

从命令行启动程序时，只需使用以下命令

```
java -classpath driverPath:. ProgramName
```

在 Windows 上，使用分号将当前目录（由 . 字符表示）与驱动程序 JAR 位置分隔开。

### 5.3.3 启动数据库

在连接到数据库服务器之前，需要先启动它。具体细节取决于你的数据库。

对于 Derby 数据库，请按照以下步骤操作：

- 1. 打开命令 shell，并切换到一个将用于存放数据库文件的目录。
- 2. 找到文件 `derbyrun.jar`。在某些版本的 JDK 中，它位于 `jdk/db/lib` 目录中。如果不在那里，请安装 Apache Derby，并在安装目录中找到该 JAR 文件。我们将包含 `lib/derbyrun.jar` 的目录记作 `derby`。
- 3. 运行以下命令

    ```
    java -jar derby/lib/derbyrun.jar server start
    ```

- 4. 再次确认数据库工作正常。创建一个包含以下行的文件 `ij.properties`：

    ```
    ij.driver=org.apache.derby.jdbc.ClientDriver
    ij.protocol=jdbc:derby://localhost:1527/
    ij.database=COREJAVA;create=true
    ```

    从另一个命令 shell 中，通过执行以下命令来运行 Derby 的交互式脚本工具（称为 `ij`）

    ```
    java -jar derby/lib/derbyrun.jar ij -p ij.properties
    ```

    现在可以发出 SQL 命令，例如

    ```
    CREATE TABLE Greetings (Message CHAR(20));
    INSERT INTO Greetings VALUES ('Hello, World!');
    SELECT * FROM Greetings;
    DROP TABLE Greetings;
    ```

    注意，每条命令都必须以分号结束。要退出，请输入

    ```
    EXIT;
    ```

- 5. 使用完数据库后，使用以下命令停止服务器

    ```
    java -jar derby/lib/derbyrun.jar server shutdown
    ```

如果使用其他数据库，你需要查阅文档，了解如何启动和停止数据库服务器，以及如何连接到它并发出 SQL 命令。

### 5.3.4 注册驱动程序类

许多 JDBC JAR 文件（例如 Java SE 8 中包含的 Derby 驱动程序）会自动注册驱动程序类。在这种情况下，可以跳过我们在本节中描述的手动注册步骤。如果 JAR 文件包含 META-INF/services/java.sql.Driver 文件，它就可以自动注册驱动程序类。你只需解压驱动程序的 JAR 文件即可检查。

> **注意：** 此注册机制使用了 JAR 规范中一个鲜为人知的部分；请参见 http://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html#ServiceProvider。自动注册是符合 JDBC4 的驱动程序的要求。

如果你的驱动程序的 JAR 文件不支持自动注册，你需要查明供应商所使用的 JDBC 驱动程序类的名称。典型的驱动程序名称是

```
org.apache.derby.jdbc.ClientDriver
org.postgresql.Driver
```

有两种方式向 DriverManager 注册驱动程序。一种方式是在 Java 程序中加载驱动程序类。例如，

```
Class.forName("org.postgresql.Driver"); // force loading of driver class
```

这条语句会导致驱动程序类被加载，从而执行一个注册驱动程序的静态初始化器。

或者，你可以设置 jdbc.drivers 属性。可以使用命令行参数指定该属性，例如

```
java -Djdbc.drivers=org.postgresql.Driver ProgramName
```

或者，你的应用程序可以通过如下调用设置系统属性

```
System.setProperty("jdbc.drivers", "org.postgresql.Driver");
```

你也可以提供多个驱动程序；用冒号分隔它们，例如

```
org.postgresql.Driver:org.apache.derby.jdbc.ClientDriver
```

### 5.3.5 连接到数据库

在 Java 程序中，像这样打开数据库连接：

```java
String url = "jdbc:postgresql:COREJAVA";
String username = "dbuser";
String password = "secret";
Connection conn = DriverManager.getConnection(url, username, password);
```

驱动程序管理器会遍历已注册的驱动程序，以找到能够使用数据库 URL 中指定子协议的驱动程序。

getConnection 方法返回一个 Connection 对象。在后续各节中，你将看到如何使用 Connection 对象执行 SQL 语句。

要连接到数据库，你需要拥有该数据库的用户名和密码。

> **注意：** 默认情况下，Derby 允许使用任意用户名进行连接，并且不检查密码。会为每个用户生成一组单独的表。默认用户名是 app。

代码清单 5.1 中的测试程序将这些步骤付诸实践。它从名为 database.properties 的文件中加载连接参数，并连接到数据库。示例代码随附的 database.properties 文件包含 Derby 数据库的连接信息。如果你使用其他数据库，请将你的数据库特定连接信息放入该文件。以下是连接到 PostgreSQL 数据库的示例。

```properties
jdbc.drivers=org.postgresql.Driver
jdbc.url=jdbc:postgresql:COREJAVA
jdbc.username=dbuser
jdbc.password=secret
```

连接到数据库后，测试程序执行以下 SQL 语句：

```sql
CREATE TABLE Greetings (Message CHAR(20))
INSERT INTO Greetings VALUES ('Hello, World!')
SELECT * FROM Greetings
```

SELECT 语句的结果会被打印出来，你应该会看到如下输出

```text
Hello, World!
```

然后通过执行以下语句删除该表

```sql
DROP TABLE Greetings
```

要运行此测试，请如前所述启动数据库，并按如下方式启动程序

```bash
java -classpath .:driverJAR test.TestDB
```

（一如既往，Windows 用户需要使用 `;` 而不是 `:` 来分隔路径元素。）

> **提示：** 调试 JDBC 相关问题的一种方法是启用 JDBC 跟踪。调用 `DriverManager.setLogWriter` 方法将跟踪消息发送到 `PrintWriter`。跟踪输出包含 JDBC 活动的详细列表。大多数 JDBC 驱动程序实现提供了额外的跟踪机制。例如，使用 Derby 时，你可以向 JDBC URL 添加 traceFile 选项：
> 
> `jdbc:derby://localhost:1527/COREJAVA;create=true;traceFile=trace.out`。

## 代码清单 5.1  `test/TestDB.java`

```java
package test;

import java.sql.*;
import java.io.*;
import java.util.*;

/**
 * This program tests that the database and the JDBC driver are correctly configured.
 * @version 1.02 2012-06-05
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
    * Runs a test by creating a table, adding a value, showing the table contents, and removing
    * the table.
    */
   public static void runTest() throws SQLException, IOException
   {
```

