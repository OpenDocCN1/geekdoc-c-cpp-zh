
regular expressions, so it needs to be escaped with a `\` character. That character needs to be escaped by another `\`, yielding the `"\\"` expression.

The complete program is in Listing 2.1. The static method

```java
void writeData(Employee[] e, PrintWriter out)
```

first writes the length of the array, then writes each record. The static method

```java
Employee[] readData(Scanner in)
```

first reads in the length of the array, then reads in each record. This turns out to be a bit tricky:

```java
int n = in.nextInt();
in.nextLine(); // consume newline
var employees = new Employee[n];
for (int i = 0; i < n; i++)
{
   employees[i] = new Employee();
   employees[i].readData(in);
}
```

The call to nextInt reads the array length but not the trailing newline character. We must consume the newline so that the readData method can get the next input line when it calls the nextLine method.

### Listing 2.1 textFile/TextFileTest.java

```java
package textFile;

import java.io.*;
import java.nio.charset.*;
import java.time.*;
import java.util.*;

/**
 * @version 1.15 2018-03-17
 * @author Cay Horstmann
 */
public class TextFileTest
{
    public static void main(String[] args) throws IOException
    {
        var staff = new Employee[3];

        staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);
        staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

        // save all employee records to the file employee.dat
        try (var out = new PrintWriter("employee.dat", StandardCharsets.UTF_8))
        {
            writeData(staff, out);
        }

        // retrieve all records into a new array
        try (var in = new Scanner(
                new FileInputStream("employee.dat"), "UTF-8"))
        {
            Employee[] newStaff = readData(in);

            // print the read employee records
            for (Employee e : newStaff)
                System.out.println(e);
        }
    }

    /**
     * Writes all employees in an array to a print writer
     * @param employees an array of employees
     * @param out a print writer
     */
    private static void writeData(Employee[] employees, PrintWriter out)
            throws IOException
    {
        // write number of employees
        out.println(employees.length);

        for (Employee e : employees)
            writeEmployee(out, e);
    }

    /**
     * Reads an array of employees from a scanner
     * @param in the scanner
     * @return the array of employees
     */
    private static Employee[] readData(Scanner in)
    {
        // retrieve the array size
        int n = in.nextInt();
        in.nextLine(); // consume newline

        var employees = new Employee[n];
        for (int i = 0; i < n; i++)
        {
            employees[i] = readEmployee(in);
        }
        return employees;
    }

    /**
     * Writes employee data to a print writer
     * @param out the print writer
     */
    public static void writeEmployee(PrintWriter out, Employee e)
    {
        out.println(e.getName() + "|" + e.getSalary() + "|" + e.getHireDay());
    }

    /**
     * Reads employee data from a buffered reader
     * @param in the scanner
     */
    public static Employee readEmployee(Scanner in)
    {
        String line = in.nextLine();
        String[] tokens = line.split("\\|");
        String name = tokens[0];
        double salary = Double.parseDouble(tokens[1]);
        LocalDate hireDate = LocalDate.parse(tokens[2]);
        int year = hireDate.getYear();
        int month = hireDate.getMonthValue();
        int day = hireDate.getDayOfMonth();
        return new Employee(name, salary, year, month, day);
    }
}
```

## 2.1.8 Character Encodings

Input and output streams are for sequences of bytes, but in many cases you will work with texts—that is, sequences of characters. It then matters how characters are encoded into bytes.

Java uses the Unicode standard for characters. Each character, or “code point,” has a 21-bit integer number. There are different *character encodings*—methods for packaging those 21-bit numbers into bytes.

The most common encoding is UTF-8, which encodes each Unicode code point into a sequence of one to four bytes (see Table 2.1). UTF-8 has the advantage that the characters of the traditional ASCII character set, which contains all characters used in English, only take up one byte each.

### Table 2.1 UTF-8 Encoding

| Character Range | Encoding |
|---|---|
| `0...7F` | `0xxxxxxx` |
| `80...7FF` | `110xxxxx 10xxxxxx` |
| `800...FFFF` | `1110xxxx 10xxxxxx 10xxxxxx` |
| `10000...10FFFF` | `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx` |

### Table 2.2 UTF-16 Encoding

| Character Range | Encoding |
|---|---|
| `0...FFFF` | `xxxxxxxxxxxxxxxx` |
| `10000...10FFFF` | `110110xxxxxxxxxx 110111xxxxxxxxxx` where `xxxxxxxxxxxx = xxxxxxxxxxxxxxxx - 1` |

Another common encoding is UTF-16, which encodes each Unicode code point into one or two 16-bit values (see Table 2.2). This is the encoding used in Java strings. Actually, there are two forms of UTF-16, called “big-endian” and “little-endian.” Consider the 16-bit value 0x2122. In the big-endian format, the more significant byte comes first: 0x21 followed by 0x22. In the little-endian format, it is the other way around: 0x22 0x21. To indicate which of the two is used, a file can start with the “byte order mark,” the 16-bit quantity 0xFEFF. A reader can use this value to determine the byte order and then discard it.

> **CAUTION:** Some programs, including Microsoft Notepad, add a byte order mark at the beginning of UTF-8 encoded files. Clearly, this is unnecessary since there are no byte order issues in UTF-8. But the Unicode standard allows it, and even suggests that it’s a pretty good idea since it leaves little doubt about the encoding. It is supposed to be removed when reading a UTF-8 encoded file. Sadly, Java does not do that, and bug reports against this issue are closed as “will not fix.” Your best bet is to strip out any leading \uFEFF that you find in your input.

In addition to the UTF encodings, there are partial encodings that cover a character range suitable for a given user population. For example, ISO 8859-1 is a one-byte code that includes accented characters used in Western European languages. Shift-JIS is a variable-length code for Japanese characters. A large number of these encodings are still in widespread use.

There is no reliable way to automatically detect the character encoding from a stream of bytes. Some API methods let you use the “default charset”—the character encoding preferred by the operating system of the computer. Is that the same encoding that is used by your source of bytes? These bytes may well originate from a different part of the world. Therefore, you should always explicitly specify the encoding. For example, when reading a web page, check the `Content-Type` header.

> **NOTE:** The platform encoding is returned by the static method `Charset.defaultCharset`. The static method `Charset.availableCharsets` returns all available `Charset` instances, as a map from canonical names to `Charset` objects.

> **CAUTION:** The Oracle implementation of Java has a system property `file.encoding` for overriding the platform default. This is not an officially supported property, and it is not consistently followed by all parts of Oracle’s implementation of the Java library. You should not set it.

The `StandardCharsets` class has static variables of type `Charset` for the character encodings that every Java virtual machine must support:

- `StandardCharsets.UTF_8`
- `StandardCharsets.UTF_16`
- `StandardCharsets.UTF_16BE`
- `StandardCharsets.UTF_16LE`
- `StandardCharsets.ISO_8859_1`
- `StandardCharsets.US_ASCII`

To obtain a `Charset` for another encoding, use the static `forName` method:

```java
Charset shiftJIS = Charset.forName("Shift-JIS");
```

Use the `Charset` object when reading or writing text. For example, you can turn an array of bytes into a string as follows:

```java
var str = new String(bytes, StandardCharsets.UTF_8);
```

> **TIP:** As of Java 10, all methods in the `java.io` package allow you to specify a character encoding with a `Charset` object or a string. Choose the `StandardCharsets` constants, so that any spelling errors are caught at compile time.

> **CAUTION:** Some methods (such as the `String(byte[])` constructor) use the default platform encoding if you don’t specify any; others (such as `Files.readAllLines`) use UTF-8.
