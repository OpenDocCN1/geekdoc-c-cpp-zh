+   4. If there was a result set, print out the result. Since this is a generic result set, we need to use metadata to find out how many columns the result has. For more information, see Section 5.8, “Metadata,” on p. 334.
+   5. If there is any SQL exception, print the exception and any chained exceptions that may be contained in it.
+   6. Close the connection to the database.

Listing 5.2 shows the code for the program.

# **Listing 5.2** `exec/ExecSQL.java`

```
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
```