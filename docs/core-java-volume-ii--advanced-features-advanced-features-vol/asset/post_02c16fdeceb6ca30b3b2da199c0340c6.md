
## 5.5.1 Prepared Statements

In this program, we use one new feature, *prepared statements*. Consider the SQL query for all books by a particular publisher, regardless of the author:

```sql
SELECT Books.Price, Books.Title
FROM Books, Publishers
WHERE Books.Publisher_Id = Publishers.Publisher_Id
AND Publishers.Name = the name from the list box
```

Instead of building a separate query statement every time the user launches such a query, we can prepare a query with a host variable and use it many times, each time filling in a different string for the variable. That technique improves performance. Whenever the database executes a query, it first computes a strategy of how to do it efficiently. By preparing the query and reusing it, you ensure that the planning step is done only once.

Each host variable in a prepared query is indicated with a ?. If there is more than one variable, you must keep track of the positions of the ? when setting the values. For example, our prepared query becomes

```java
String publisherQuery
    = "SELECT Books.Price, Books.Title"
    + " FROM Books, Publishers"
    + " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";
PreparedStatement stat = conn.prepareStatement(publisherQuery);
```

Before executing the prepared statement, you must bind the host variables to actual values with a set method. As with the get methods of the ResultSet interface, there are different set methods for the various types. Here, we want to set a string to a publisher name:

```java
stat.setString(1, publisher);
```

The first argument is the position number of the host variable that we want to set. The position 1 denotes the first ?. The second argument is the value that we want to assign to the host variable.

If you reuse a prepared query that you have already executed, all host variables stay bound unless you change them with a set method or call the clearParameters method. That means you only need to call a setXxx method on those host variables that change from one query to the next.

Once all variables have been bound to values, you can execute the prepared statement:

```java
ResultSet rs = stat.executeQuery();
```

> **TIP:** Building a query manually, by concatenating strings, is tedious and potentially dangerous. You have to worry about special characters such as quotes—and, if your query involves user input, you have to guard against injection attacks. Therefore, use prepared statements whenever your query involves variables.

The price update feature is implemented as an UPDATE statement. Note that we call executeUpdate, not executeQuery, because the UPDATE statement does not return a result set. The return value of executeUpdate is the count of changed rows.

```java
int r = stat.executeUpdate();
System.out.println(r + " rows updated");
```

> **NOTE:** A PreparedStatement object becomes invalid after the associated Connection object is closed. However, many databases automatically cache prepared statements. If the same query is prepared twice, the database simply reuses the query strategy. Therefore, don’t worry about the overhead of calling prepareStatement.

The following list briefly describes the structure of the example program:

- The author and publisher array lists are populated by running two queries that return all author and publisher names in the database.

- The queries involving authors are complex. A book can have multiple authors, so the BooksAuthors table stores the correspondence between authors and books. For example, the book with ISBN 0-201-96426-0 has two authors with codes DATE and DARW.

  ```
  0-201-96426-0, DATE, 1
  0-201-96426-0, DARW, 2
  ```

  to indicate this fact. The third column lists the order of the authors. (We can’t just use the position of the rows in the table. There is no fixed row ordering in a relational table.) Thus, the query has to join the Books, BooksAuthors, and Authors tables to compare the author name with the one selected by the user.

  ```sql
  SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors, Publishers
  WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN
  AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ?
  AND Publishers.Name = ?
  ```

> **TIP:** Some Java programmers avoid complex SQL statements such as this one. A surprisingly common, but very inefficient, workaround is to write lots of Java code that iterates through multiple result sets. But the database is a lot better at executing query code than a Java program can be—that's the core competency of a database. A rule of thumb: If you can do it in SQL, don't do it in Java.

- The `changePrices` method executes an `UPDATE` statement. Note that the `WHERE` clause of the `UPDATE` statement needs the publisher *code* and we only know the publisher *name*. This problem is solved with a nested subquery:

  ```sql
  UPDATE Books
  SET Price = Price + ?
  WHERE Books.Publisher_Id = (SELECT Publisher_Id FROM Publishers WHERE Name = ?)
  ```

Listing 5.3 is the complete program code.

### **Listing 5.3** query/QueryTest.java

```java
 1 package query;
 2
 3 import java.io.*;
 4 import java.nio.file.*;
 5 import java.sql.*;
 6 import java.util.*;
 7
 8 /**
 9  * This program demonstrates several complex database queries.
10  * @version 1.31 2018-05-01
11  * @author Cay Horstmann
12  */
13 public class QueryTest
14 {
15    private static final String allQuery = "SELECT Books.Price, Books.Title FROM Books";
16
17    private static final String authorPublisherQuery = "SELECT Books.Price, Books.Title"
18       + " FROM Books, BooksAuthors, Authors, Publishers"
19       + " WHERE Authors.Author_Id = BooksAuthors.Author_Id AND BooksAuthors.ISBN = Books.ISBN"
20       + " AND Books.Publisher_Id = Publishers.Publisher_Id AND Authors.Name = ?"
21       + " AND Publishers.Name = ?";
22
23    private static final String authorQuery
24       = "SELECT Books.Price, Books.Title FROM Books, BooksAuthors, Authors"
25       + " WHERE Authors.Author_Id = BooksAuthors.Author_Id"
26       + " AND BooksAuthors.ISBN = Books.ISBN"
27       + " AND Authors.Name = ?";

    private static final String publisherQuery
        = "SELECT Books.Price, Books.Title FROM Books, Publishers"
        + " WHERE Books.Publisher_Id = Publishers.Publisher_Id AND Publishers.Name = ?";

    private static final String priceUpdate = "UPDATE Books SET Price = Price + ?"
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
            publishers.add("Any");
            try (Statement stat = conn.createStatement())
            {
                // Fill the authors array list
                var query = "SELECT Name FROM Authors";
                try (ResultSet rs = stat.executeQuery(query))
                {
                    while (rs.next())
                        authors.add(rs.getString(1));
                }

                // Fill the publishers array list
                query = "SELECT Name FROM Publishers";
                try (ResultSet rs = stat.executeQuery(query))
                {
                    while (rs.next())
                        publishers.add(rs.getString(1));
                }
            }
            var done = false;
            while (!done)
            {
                System.out.print("?Query C)hange prices E)xit: ");
                String input = in.next().toUpperCase();
                if (input.equals("Q"))
                    executeQuery(conn);
                else if (input.equals("C"))
                    changePrices(conn);
                else
                    done = true;
            }
77    }
78    catch (SQLException e)
79    {
80        for (Throwable t : e)
81            System.out.println(t.getMessage());
82    }
83 }
84
85 /**
86  * Executes the selected query.
87  * @param conn the database connection
88  */
89 private static void executeQuery(Connection conn) throws SQLException
90 {
91     String author = select("Authors:", authors);
92     String publisher = select("Publishers:", publishers);
93     PreparedStatement stat;
94     if (!author.equals("Any") && !publisher.equals("Any"))
95     {
96         stat = conn.prepareStatement(authorPublisherQuery);
97         stat.setString(1, author);
98         stat.setString(2, publisher);
99     }
100    else if (!author.equals("Any") && publisher.equals("Any"))
101    {
102        stat = conn.prepareStatement(authorQuery);
103        stat.setString(1, author);
104    }
105    else if (author.equals("Any") && !publisher.equals("Any"))
106    {
107        stat = conn.prepareStatement(publisherQuery);
108        stat.setString(1, publisher);
109    }
110    else
111        stat = conn.prepareStatement(allQuery);
112
113    try (ResultSet rs = stat.executeQuery())
114    {
115        while (rs.next())
116            System.out.println(rs.getString(1) + ", " + rs.getString(2));
117    }
118 }
119
120 /**
121  * Executes an update statement to change prices.
122  * @param conn the database connection
123  */
```
