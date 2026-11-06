

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

匹配后，代码将返回以下内容：

```text
Match words that begin with 'S':
The Expression is: \bS\S*
Splitting
String
Substrings
```

输出显示，已从输入字符串中匹配到三个单词。我们匹配的是任何以 S 开头的单词，结果找到了其中三个。

考虑下面给出的下一个示例：

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

代码将给出以下结果：

```text
Match words beginning with 's' and ending with 'e':
The input expression is: \bs\S*e\b
she
same
```

在上面的示例中，我们匹配以 s 开头并以 e 结尾的单词。我们成功地在输入字符串中匹配到了两个单词。下面是另一个示例：

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

代码返回以下内容：

```text
The input string is: Hi    learner
The string after replacement is: Hi learner
```

这段代码所做的是替换多余的空格。“Hi”和“learner”之间有一个很大的空格。多余的那个已被替换或删除。

```csharp
} finally {
    // statements to execute
}
```

如果 *try* 块引发了多个异常，可以使用多个 catch 语句，以捕获许多不同的异常。

在 C# 中，异常使用类来表示。*System.Exception* 充当 C# 中所有异常类的基类，因为所有其他类都直接或间接地派生自它。

### 处理异常

在 C# 中，可以使用 *try* 和 *catch* 块来处理异常。借助这些块，我们可以将核心程序语句与处理错误的语句分开。我们可以使用 *try*、*catch* 和 *finally* 关键字来处理错误。

例如，除以零应该引发异常，因为数学上不支持这样做。让我们创建一些代码来处理这种情况：

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

代码应返回下面给出的异常：

```text
Exception caught: System.DivideByZeroException: Attempted to divide by zero.
   at ExceptionHandlingApp.DivisionClass.Division (System.Int32 x, System.Int32 y) [0x00000]
Answer: 0
```

我们创建了 *division()* 函数，它接受两个整数类型的参数 x 和 y。然后我们将 12 和 0 传递给该函数，这意味着我们将用 12 除以 0。然而，这产生了一个异常，因为不允许除以零。

### 用户定义的异常

C# 允许程序员定义自己的异常。我们从 *Exception* 类派生此类用户定义的异常类。考虑下面给出的示例：

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

代码将返回以下内容：

```text
TempIsZeroException: We found Zero Temperature
```

### 嵌套 try-catch

C# 允许我们创建嵌套的 try-catch 块。在这种情况下，异常将在发生异常的那个 try 块之后的 catch 块中被捕获。考虑以下示例：

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

代码打印以下内容：

```text
The inner catch
```

如果内部 catch 块没有必要的异常类型，异常将流向外部 catch 块，直到找到合适的异常筛选器。下面是一个示例：

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

在上面给出的示例中，语句 *emp.EmployeeName* 将生成 NullReferenceException，但我们没有处理 NullReferenceException 或 Exception 类型的 catch 块。外部块将处理此异常。代码返回以下内容：

外部 catch

## 第18章：文件 I/O[40]

文件由名称和目录路径来表征。一旦打开文件，它就变成一个 *流*。文件通常是为了读取或写入目的而打开的。

流只是通过通信路径的字节序列。流有两种类型：

- 输入流
- 输出流

输入流帮助我们读取文件中的数据，即读操作；而输出流帮助我们将数据写入文件，即写操作。

### 输入/输出类

C# 为我们提供了许多可用于处理文件的类。这些类可用于访问目录、文件，创建新文件，打开现有文件，以及将文件从一个目录移动到另一个目录。这些类定义在 System.IO 类中。让我们讨论其中一些类：

- **BinaryReader** - 此类帮助我们从二进制流中读取基元数据。
- **BinaryWriter** - 此类帮助我们将基元数据以二进制格式写入。
- **BufferedStream** - 它充当流字节的临时存储。
- **Directory** - 此类帮助我们操作目录结构。
- **DriveInfo** - 此类向我们提供有关驱动器的信息。
- **File** - 此类用于操作文件。
- **FileInfo** - 帮助对文件执行操作。
- **FileStream** - 用于从文件中的任何位置写入和读取。
- **MemoryStream** - 帮助随机访问保存在内存中的数据。
- **Path** - 用于对路径信息执行操作。
- **StreamReader** - 从字节流中读取字符。
- **StreamWriter** - 将字符写入流。

