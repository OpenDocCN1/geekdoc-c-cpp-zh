
```csharp
private static void findMatch(string input, string expre) {
    Console.WriteLine("The Expression is: " + expre);
    MatchCollection mc = Regex.Matches(input, expre);
    foreach (Match x in mc) {
        Console.WriteLine(x);
    }
}
static void Main(string[] args) {
    string s = "Splitting an Input String into Substrings";

    Console.WriteLine("Match words that begin with 'S': ");
    findMatch(s, @"\bS\S*");
    Console.ReadKey();
}
}
}
```

After the match, the code will return the following:

```text
Match words that begin with 'S':
The Expression is: \bS\S*
Splitting
String
Substrings
```

The output shows that three words have been matched from the input string. We were matching any words that begin with S and three of them were found.

Consider the next example given below:

```csharp
using System.Text.RegularExpressions;
using System;
namespace RegularExpApp {
    class MyProgram {
        private static void findMatch(string input, string expre) {
            Console.WriteLine("The input expression is: " + expre);
            MatchCollection mc = Regex.Matches(input, expre);
            foreach (Match x in mc) {
                Console.WriteLine(x);
            }
        }

        static void Main(string[] args) {
            string s = "so she was the same";

            Console.WriteLine("Match words beginning with 's' and ending with 'e':");
            findMatch(s, @"\bs\S*e\b");
            Console.ReadKey();
        }
    }
}
```

The code will give the following result:

```text
Match words beginning with 's' and ending with 'e':
The input expression is: \bs\S*e\b
she
same
```

In the above example, we are matching the words that begin with s and end with e. We have successfully matched two words in the input string. Here is another example:

```csharp
using System;
using System.Text.RegularExpressions;
namespace RegularExpApp {
    class MyProgram {
        static void Main(string[] args) {
            string text = "Hi  learner  ";
            string pattern = "\\s+";
            string substitute = " ";
            Regex r = new Regex(pattern);
            string output = r.Replace(text, substitute);
            Console.WriteLine("The input string is: {0}", text);
            Console.WriteLine("The string after replacement is: {0}", output);
            Console.ReadKey();
        }
    }
}
```

The code returns the following:

```text
The input string is: Hi    learner
The string after replacement is: Hi learner
```

What we are doing in the code is that we are replacing the extra white space. There is a big space between “Hi” and “learner”. The extra one has been replaced or removed.

```csharp
} finally {
    // statements to execute
}
```

One can use many catch statements with the goal of catching many different exceptions if many exceptions are raised by the *try* block.

In C#, exceptions are represented using classes. The *System.Exception* acts as the base class for all exception classes in C# since all other classes are derived from it, either directly or indirectly.

### Handling Exceptions

In C#, exceptions can be handled using the *try* and *catch* blocks. With these blocks, we can separate the core program statements from statements for handling errors. We can handle errors using the *try*, *catch* and *finally* keywords.

A division by zero should, for example, raise an exception as it not mathematically supported. Let us create some code to handle this:

```csharp
using System;

namespace ExceptionHandlingApp {
    class DivisionClass {
        int answer;

        DivisionClass() {
            answer = 0;
        }

        public void division(int x, int y) {
            try {
                answer = x / y;
            } catch (DivideByZeroException exception) {
                Console.WriteLine("Exception caught: {0}", exception);
            } finally {
                Console.WriteLine("Answer: {0}", answer);
            }
        }
        static void Main(string[] args) {
            DivisionClass dc = new DivisionClass();
            dc.division(12, 0);
            Console.ReadKey();
        }
    }
}
```

The code should return the exception given below:

```text
Exception caught: System.DivideByZeroException: Attempted to divide by zero.
   at ExceptionHandlingApp.DivisionClass.Division (System.Int32 x, System.Int32 y) [0x00000]
Answer: 0
```

We created the *division()* function that takes two arguments, x and y, of type integer. We have then passed 12 and 0 to the function, meaning that we will be dividing 12 by 0. However, this has generated an exception since division by zero is not allowed.

### User-Defined Exceptions

C# allows programmers to define their own exceptions. We derive such user-defined exception classes from the *Exception* class. Consider the example given below:

```csharp
using System;

namespace ExceptionHandlingApp {
    class TemperatureTest {
        static void Main(string[] args) {
            TemperatureClass tc = new TemperatureClass();
            try {
                tc.displayTemperature();
            } catch(TempIsZeroException exception) {
                Console.WriteLine("TempIsZeroException: {0}", exception.Message);
            }
            Console.ReadKey();
        }
    }
}
public class TempIsZeroException: Exception {
    public TempIsZeroException(string msg): base(msg) {
    }
}
public class TemperatureClass {
    int temp = 0;

    public void displayTemperature() {
        if(temp == 0) {
            throw (new TempIsZeroException("We found Zero Temperature"));
        } else {
            Console.WriteLine("Temperature is: {0}", temp);
        }
    }
}
```

The code will return the following:

```text
TempIsZeroException: We found Zero Temperature
```

### Nested try-catch

C# allows us to create a block of nested try-catch. In such a case, the exception will be caught in the catch block following the try block in which the exception occurred. Consider the following example:

```csharp
using System;

public class NestedtryCatch
{
    public static void Main()
    {
        Employee emp = null;

        try
        {
            try
            {
                emp.EmployeeName = "";
            }
            catch
            {
                Console.WriteLine("The inner catch");
            }
        }
        catch
        {
            Console.WriteLine("The outer catch");
        }
    }
}

public class Employee{
    public string EmployeeName { get; set; }
}
```

The code prints the following:

```text
The inner catch
```

In case there is no inner catch block with the necessary exception type, the exception will flow to outer catch block until an appropriate exception filter is found. Here is an example:

```csharp
using System;
public class NestedtryCatch
{
    public static void Main()
    {
        Employee emp = null;

        try
        {
            try
            {
                // This will throw a NullReferenceException
                emp.EmployeeName = "";
            }
            catch (InvalidOperationException innerException)
            {
                Console.WriteLine("The inner catch");
            }
        }
        catch
        {
            Console.WriteLine("The outer catch");
        }
    }
}

public class Employee{
    public string EmployeeName { get; set; }
}
```

In the example given above, the statement *emp.EmployeeName* will generate a NullReferenceException, but we don’t have a catch block that handles a NullReferenceException or an Exception type. The outer block will handle this. The code returns the following:

The outer catch

## Chapter 18: File I/O[40]

A file is characterized by a name and a directory path. Once you open a file, it becomes a *stream*. Files are normally opened for reading or writing purposes.

The stream is simply the sequence of bytes that pass through the communication path. Streams are of two types:

- Input stream
- Output stream

The input stream helps us to read data from a file, that is, a read operation, while the output stream helps us to write data into a file, that is, a write operation.

### Input/Output Classes

C# provides us with a number of classes that we can use for working with files. These classes can be used for accessing directories, files, creating new files, opening existing files and moving files from one directory to another. These classes are defined in the System.IO class. Let us discuss some of these classes:

- **BinaryReader** - this class helps us in reading primitive data from a binary stream.
- **BinaryWriter** - this class helps us in writing primitive data in a binary format.
- **BufferedStream** - this acts as a temporary storage for bytes of streams.
- **Directory** - this class helps us to manipulate the structure of a directory.
- **DriveInfo** - this class provides us with information about the drives.
- **File** - this class is used for manipulation of files.
- **FileInfo** - helps in performing operations on files.
- **FileStream** - used for writing and reading from any location in a file.
- **MemoryStream** - helps in randomly accessing data kept in a memory.
- **Path** - for performing operations on path information.
- **StreamReader** - reads characters from a stream of bytes.
- **StreamWriter** - writes characters to a stream.
