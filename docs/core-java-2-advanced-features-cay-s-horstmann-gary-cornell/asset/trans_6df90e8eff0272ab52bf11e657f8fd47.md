
## 清单 5.2 *（续）*

```java
53        catch (SQLException ex)
54        {
55            for (Throwable e : ex)
56                e.printStackTrace();
57        }
58    }
59}
60
61catch (SQLException e)
62{
63    for (Throwable t : e)
64        t.printStackTrace();
65}
66}
67
68/**
69 * Gets a connection from the properties specified in the file database.properties.
70 * @return the database connection
71 */
72public static Connection getConnection() throws SQLException, IOException
73{
74    Properties props = new Properties();
75    try (InputStream in = Files.newInputStream(Paths.get("database.properties")))
76    {
77        props.load(in);
78    }
79
80    String drivers = props.getProperty("jdbc.drivers");
81    if (drivers != null) System.setProperty("jdbc.drivers", drivers);
82
83    String url = props.getProperty("jdbc.url");
84    String username = props.getProperty("jdbc.username");
85    String password = props.getProperty("jdbc.password");
86
87    return DriverManager.getConnection(url, username, password);
88}
89
90/**
91 * Prints a result set.
92 * @param result the result set to be printed
93 */
94public static void showResultSet(ResultSet result) throws SQLException
95{
96    ResultSetMetaData metaData = result.getMetaData();
97    int columnCount = metaData.getColumnCount();
```

如何高效地完成此操作。通过准备查询并重复使用它，你可以确保规划步骤只执行一次。

预处理查询中的每个宿主变量都用 ? 表示。如果有多个变量，在设置值时必须跟踪这些 ? 的位置。例如，我们预处理后的查询变为

```java
String publisherQuery =
    "SELECT Books.Price, Books.Title" +
    " FROM Books, Publishers" +
    " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";
PreparedStatement stat = conn.prepareStatement(publisherQuery);
```

在执行预处理语句之前，必须使用 set 方法将宿主变量绑定到实际值。与 ResultSet 接口的 get 方法一样，针对各种类型有不同的 set 方法。这里，我们要将一个字符串设置为出版商名称。

```java
stat.setString(1, publisher);
```

第一个参数是要设置的宿主变量的位置编号。位置 1 表示第一个 ?。第二个参数是要赋给该宿主变量的值。

如果重用已经执行过的预处理查询，所有宿主变量都保持绑定状态，除非你用 set 方法更改它们或调用 clearParameters 方法。这意味着你只需对那些在每次查询之间发生变化的宿主变量调用 setXxx 方法。

一旦所有变量都绑定到值，就可以执行该预处理语句：

```java
ResultSet rs = stat.executeQuery();
```

> **提示：** 通过拼接字符串手动构建查询既繁琐又可能危险。你必须担心引号等特殊字符，而且如果你的查询涉及用户输入，还必须防范注入攻击。因此，只要查询涉及变量，就应使用预处理语句。

价格更新功能通过一条 UPDATE 语句实现。请注意，我们调用的是 executeUpdate，而不是 executeQuery，因为 UPDATE 语句不返回结果集。executeUpdate 的返回值是更改的行数。

```java
int r = stat.executeUpdate();
System.out.println(r + " rows updated");
```

> 注意：关联的 Connection 对象关闭后，PreparedStatement 对象会失效。但是，许多数据库会自动缓存预处理语句。如果同一条查询被准备两次，数据库会直接重用查询策略。因此，不必担心调用 prepareStatement 的开销。

以下列表简要描述示例程序的结构。

- 作者和出版商数组列表通过运行两个查询来填充，这两个查询返回数据库中的所有作者名和出版商名。

- 涉及作者的查询比较复杂。一本书可以有多个作者，因此 BooksAuthors 表存储作者与图书之间的对应关系。例如，ISBN 为 0-201-96426-0 的图书有两个作者，代码分别为 DATE 和 DARW。BooksAuthors 表中有以下行

    ```
    0-201-96426-0, DATE, 1
    0-201-96426-0, DARW, 2
    ```

    以表示这一事实。第三列列出作者的顺序。（我们不能只使用表中行的位置。关系表中没有固定的行顺序。）因此，查询必须连接 Books、BooksAuthors 和 Authors 表，以便将作者名与用户选择的作者名进行比较。

    ```sql
    SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors, Publishers
    WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN
    AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ? AND Publishers.Name = ?
    ```

    > 提示：有些 Java 程序员会避免使用这样复杂的 SQL 语句。一个出奇常见但效率很低的变通做法是编写大量 Java 代码来遍历多个结果集。但是，数据库执行查询代码的能力比 Java 程序强得多——这是数据库的核心能力。一条经验法则：如果能在 SQL 中完成，就不要在 Java 中完成。

- changePrices 方法执行一条 UPDATE 语句。注意，UPDATE 语句的 WHERE 子句需要出版商代码，而我们只知道出版商名称。这个问题通过嵌套子查询解决：

    ```sql
    UPDATE Books
    SET Price = Price + ?
    WHERE Books.Publisher_Id = (SELECT Publisher_Id FROM Publishers WHERE Name = ?)
    ```

清单 5.3 是完整的程序代码。

## 清单 5.3 `query/QueryTest.java`

```java
package query;

import java.io.*;
import java.nio.file.*;
import java.sql.*;
import java.util.*;

/**
 * This program demonstrates several complex database queries.
 * @version 1.30 2012-06-05
 * @author Cay Horstmann
 */
public class QueryTest
{
   private static final String allQuery = "SELECT Books.Price, Books.Title FROM Books";

   private static final String authorPublisherQuery = "SELECT Books.Price, Books.Title"
         + " FROM Books, BooksAuthors, Authors, Publishers"
         + " WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN"
         + " AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ?"
         + " AND Publishers.Name = ?";

   private static final String authorQuery
         = "SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors"
         + " WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN"
         + " AND Authors.Name = ?";

   private static final String publisherQuery
         = "SELECT Books.Price, Books.Title FROM Books, Publishers"
         + " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";

   private static final String priceUpdate = "UPDATE Books " + "SET Price = Price + ?"
         + " WHERE Books.Publisher_Id = (SELECT Publisher_Id FROM Publishers WHERE Name = ?)";

   private static Scanner in;
   private static ArrayList<String> authors = new ArrayList<>();
   private static ArrayList<String> publishers = new ArrayList<>();

   public static void main(String[] args) throws IOException
   {
      try (Connection conn = getConnection())
      {
         in = new Scanner(System.in);
         authors.add("Any");
46        publishers.add("Any");
47        try (Statement stat = conn.createStatement())
48        {
49            // Fill the authors array list
50            String query = "SELECT Name FROM Authors";
51            try (ResultSet rs = stat.executeQuery(query))
52            {
53                while (rs.next())
54                    authors.add(rs.getString(1));
55
56            }
57            // Fill the publishers array list
58            query = "SELECT Name FROM Publishers";
59            try (ResultSet rs = stat.executeQuery(query))
60            {
61                while (rs.next())
62                    publishers.add(rs.getString(1));
63            }
64        }
65        boolean done = false;
66        while (!done)
67        {
68            System.out.print("(Q)uery (C)hange prices (E)xit: ");
69            String input = in.next().toUpperCase();
70            if (input.equals("Q"))
71                executeQuery(conn);
72            else if (input.equals("C"))
73                changePrices(conn);
74            else
75                done = true;
76        }
77        }
78        catch (SQLException e)
79        {
80            for (Throwable t : e)
81                System.out.println(t.getMessage());
82        }
83    }
84
85    /**
86     * Executes the selected query.
87     * @param conn the database connection
88     */
89    private static void executeQuery(Connection conn) throws SQLException
90    {
91        String author = select("Authors.", authors);
92        String publisher = select("Publishers.", publishers);
```
