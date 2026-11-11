The call to `nextInt` reads the array length but not the trailing newline character.
We must consume the newline so that the `readData` method can get the next input
line when it calls the `nextLine` method.

# Listing 2.1  `textFile/TextFileTest.java`

```
```java
package textFile;

import java.io.*;
import java.time.*;
import java.util.*;

/**
 * @version 1.14 2016-07-11
 * @author Cay Horstmann
 */
public class TextFileTest
{
   public static void main(String[] args) throws IOException
   {
      Employee[] staff = new Employee[3];

      staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);
      staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
      staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

      // save all employee records to the file employee.dat
      try (PrintWriter out = new PrintWriter("employee.dat", "UTF-8"))
      {
         writeData(staff, out);
      }

      // retrieve all records into a new array
      try (Scanner in = new Scanner(
            new FileInputStream("employee.dat"), "UTF-8"))
      {
         Employee[] newStaff = readData(in);

         // print the newly read employee records
         for (Employee e : newStaff)
            System.out.println(e);
      }
   }

   /**
    * Writes all employees in an array to a print writer
    * @param employees an array of employees
    */
```
```

*Continues*