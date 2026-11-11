
| API | Version |
|---|---|
| `java.sql.SQLWarning` | 1.1 |

- `SQLWarning getNextWarning()`  
  returns the next warning chained to this one, or null at the end of the chain.

| API | Version |
|---|---|
| `java.sql.Connection` | 1.1 |
| `java.sql.Statement` | 1.1 |
| `java.sql.ResultSet` | 1.1 |

- `SQLWarning getWarnings()`  
  returns the first of the pending warnings, or null if no warnings are pending.

| API | Version |
|---|---|
| `java.sql.DataTruncation` | 1.1 |

- `boolean getParameter()`  
  returns true if the data truncation applies to a parameter, false if it applies to a column.
- `int getIndex()`  
  returns the index of the truncated parameter or column.
- `int getDataSize()`  
  returns the number of bytes that should have been transferred, or -1 if the value is unknown.
- `int getTransferSize()`  
  returns the number of bytes that were actually transferred, or -1 if the value is unknown.

## 5.4.4 Populating a Database

We are now ready to write our first real JDBC program. Sure, it would be nice to try some of the fancy queries discussed earlier, but we have a problem: Right now, there are no data in the database. We need to populate the database, and a simple way of doing that is with a set of SQL instructions to create tables and insert data into them. Most database programs can process a set of SQL instructions from a text file, but there are pesky differences about statement terminators and other syntactical issues.

For that reason, we will use JDBC in a simple program that reads a file with SQL instructions, one instruction per line, and executes them.

Specifically, the program reads data from a text file in a format such as

```sql
CREATE TABLE Publishers (Publisher_Id CHAR(6), Name CHAR(30), URL CHAR(80));
INSERT INTO Publishers VALUES ('Q201', 'Addison-Wesley', 'www.aw-bc.com');
INSERT INTO Publishers VALUES ('Q471', 'John Wiley & Sons', 'www.wiley.com');
. . . .
```

Listing 5.2 contains the code for the program that reads a file with SQL statements and executes them. You don’t have to read through the code; simply use the program so you can populate your database and run the examples in the remainder of this chapter.

Make sure that your database server is running, and run the program as follows:

```bash
java -classpath driverPath:. exec.ExecSQL Books.sql
java -classpath driverPath:. exec.ExecSQL Authors.sql
java -classpath driverPath:. exec.ExecSQL Publishers.sql
java -classpath driverPath:. exec.ExecSQL BooksAuthors.sql
```

Before running the program, check that the file database.properties is set up properly for your environment (see Section 5.3.5, “Connecting to the Database,” on p. 296).

> **NOTE:** Your database may also have a utility to read SQL files directly. For example, with Derby, you can run
>
> `java -jar derby/lib/derbyrun.jar ij -p ij.properties Books.sql`
>
> (The ij.properties file is described in Section 5.3.3, “Starting the Database,” on p. 294.)
>
> In the data format for the ExecSQL command, we allow an optional semicolon at the end of each line because most database utilities expect this format.

The following steps briefly describe the ExecSQL program:

- 1. Connect to the database. The getConnection method reads the properties in the file database.properties and adds the jdbc.drivers property to the system properties. The driver manager uses the jdbc.drivers property to load the appropriate database driver. The getConnection method uses the jdbc.url, jdbc.username, and jdbc.password properties to open the database connection.
- 2. Open the file with the SQL statements. If no file name was supplied, prompt the user to enter the statements on the console.
- 3. Execute each statement with the generic execute method. If it returns true, the statement had a result set. The four SQL files that we provide for the book database all end in a `SELECT *` statement so that you can see that the data were successfully inserted.
- 4. If there was a result set, print out the result. Since this is a generic result set, we need to use metadata to find out how many columns the result has. For more information, see Section 5.8, “Metadata,” on p. 334.
- 5. If there is any SQL exception, print the exception and any chained exceptions that may be contained in it.
- 6. Close the connection to the database.

Listing 5.2 shows the code for the program.

### **Listing 5.2** `exec/ExecSQL.java`

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

## 5.5 Query Execution

In this section, we write a program that executes queries against the COREJAVA database. For this program to work, you must have a COREJAVA database populated with tables as described in the preceding section.

When querying the database, you can select the author and the publisher or leave either of them as Any.

You can also change the data in the database. Select a publisher and type an amount. All prices of that publisher are adjusted by the amount you entered, and the program displays how many rows were changed. After a price change, you might want to run a query to verify the new prices.
