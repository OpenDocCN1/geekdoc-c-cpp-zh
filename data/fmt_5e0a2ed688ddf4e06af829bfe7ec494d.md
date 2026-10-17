
```csharp
myClass = new AnotherClass();

myClass.number = a;

x = b;

y = c;

myDays = Days.Mon;
}

// 方法

public void PrintStatement()
{
    Console.WriteLine("x = {0}, y = {1}, myDays = {2}", x, y, myDays);
}
}

class AnotherClass
{
    public int number;
}

enum Days
{
    Mon, Tues, Wed
}
```

结构体从第 1 到第 23 行。在第 4 行，我们声明了两个 `int` 字段。在第 5 行，我们声明了另一个字段 `myClass`。该字段是 `AnotherClass` 的实例。在第 6 行，我们声明了枚举 `myDays`。这两个字段（`myClass` 和 `myDays`）特别包含在示例中，以演示如何将类实例和枚举变量作为字段。结构体（和类）可以包含枚举变量以及其他结构体类的实例。

声明结构体后，我们在第 9 到 16 行声明了结构体的构造函数，随后是打印 `x`、`y` 和 `myDays` 值的方法。

在声明结构体后，我们在第 25 到第 28 行声明了类 `AnotherClass`，第 30 行声明了枚举 `Days`。示例中，我们将类和枚举声明在 `myStruct` 外部。然而，我们可以在 `myStruct` 内部声明枚举或类。枚举、结构体或类可以嵌套在另一个结构体或类中。当我们处理书末的项目时，我们将查看在类内部声明枚举的示例。

要使用上面的结构体，我们可以向 `Main()` 中添加以下代码：

```csharp
myStruct example = new myStruct(2, 3, 5);
example.PrintStatement();
```

如果我们运行代码，我们将得到

`x = 3, y = 5, myDays = Mon`

结构体和类之间有两个主要区别。首先，结构体数据类型不支持继承。因此，你不能从一个结构体派生另一个。然而，结构体可以实现接口。实现方法与类相同。更多信息请参阅第 8 章。

# 第 10 章：LINQ

LINQ 代表语言集成查询（Language-Integrated Query），是 C# 中一个有趣的特性，允许你对程序中的数据进行。在本章中，我们将对 LINQ 进行简要介绍，并给出两个使用 LINQ 的示例。

首先，让我们学习如何编写 LINQ 查询。LINQ 查询的典型语法是来自...`from...where...select`。

假设我们有一个数字数组，想要从数组中选择所有的偶数。我们可以使用 LINQ 轻松地实现。

首先，我们声明该数组。

```csharp
int[] numbers = { 0, 1, 2, 3, 4, 5, 6 };
```

接下来，我们按照如下方式编写 LINQ 查询：

```csharp
var evenNumQuery =
from num in numbers
where (num % 2) == 0
select num;
```

查询位于第二行到第四行。有 SQL 经验的读者可能会觉得这个查询非常熟悉。该查询由三部分组成。
第一部分

```csharp
from num in numbers
```

表示我们正在对 `numbers` 数组执行查询。`num` 是我们用来表示数组中单个元素的名称。接下来的一行

```csharp
where (num % 2) == 0
```

测试单个元素，确定 `num` 除以 2 的余数是否为零。如果是，则 `num` 是一个偶数。第三行

```csharp
select num;
```

选择所有符合此标准的元素。

然后将此结果赋值给变量 `evenNumQuery`，该变量被声明为 `var` 类型。`var` 是一种特殊的数据类型，每当我们希望编译器自己确定数据类型时就会使用它。这是必要的，因为在我们的示例中，`evenNumQuery` 的数据类型相当复杂；让 C# 自己找出数据类型会更好。

创建查询语句后，我们可以通过编写以下代码来执行查询：

```csharp
foreach (int i in evenNumQuery)
    Console.WriteLine("{0} is an even number", i);
```

如果你运行这段代码，将得到：

```
0 is an even number
2 is an even number
4 is an even number
6 is an even number
```

就是这样。使用 LINQ 就这么简单。现在让我们进入一个更复杂的 LINQ 示例。

假设你有一个 `Customer` 类，具有 `Name`、`Phone`、`Address` 和 `Balance` 属性，并有一个用于初始化这些每个属性的构造函数。

我们可以在 `Main()` 方法中使用下面的代码创建一个 `Customer` 对象的列表。

```csharp
List<Customer> customers = new List<Customer>();
```

```csharp
customers.Add(new Customer("Alan", "80911291", "ABC Street", 25.60m));
customers.Add(new Customer("Bill", "198721311", "DEF Street", -32.1m));
customers.Add(new Customer("Carl", "298123711", "GHI Street", -12.2m));
customers.Add(new Customer("David", "78612312", "JKL Street", 12.6m));
```

现在我们要搜索所有余额为负的账户，可以使用以下 LINQ 查询。

```csharp
var overdue = from cust in customers
               where cust.Balance < 0
               orderby cust.Balance ascending
               select { cust.Name, cust.Balance };
```

此查询与第一个查询相似，但有两个主要区别。在这里，我们使用了两个额外的关键字 `orderby` 和 `ascending` 来按升序顺序排列结果。

此外，我们在 `select` 语句中使用了 `new` 关键字。每当我们想要从对象中选择多个一个字段时，就需要 `new` 关键字。

要执行并打印结果，我们可以使用下面的 `foreach` 循环：

```csharp
foreach (var cust in overdue)
    Console.WriteLine("Name = {0}, Balance = {1}", cust.Name,
    cust.Balance);
```

我们将得到：

```
Name = Bill, Balance = -32.1
Name = Carl, Balance = -12.2
```

# 第 11 章：文件处理

太棒了！我们来到了项目前的最后一章。在本章中，我们将学习如何读取和写入外部文件。

在之前的第 5 章中，我们学习了如何使用 `ReadLine()` 方法从用户获取输入。然而，在某些情况下，让用户向我们的程序输入数据可能并不实际，特别是当我们的程序需要处理大量数据时。在这种情况下，更方便的方法是将所需信息准备为外部文件，并让我们的程序从文件中读取信息。

C# 为我们提供了许多类来处理文件。在本章中我们将看到的类是 `File`、`StreamWriter` 和 `StreamReader` 类。这三个类都位于 `System.IO` 命名空间。要使用本章中的方法，你必须添加指令：

```csharp
using System.IO;
```

## 读取文本文件

要从文本文件中读取数据，我们使用 `StreamReader` 类。

假设我们要从位于 C 盘的 "myFile.txt" 文件读取数据。下面的示例显示了如何操作。

```csharp
string path = "c:\myFile.txt";
using (StreamReader sr = new StreamReader(path))
{
    while (sr.EndOfStream != true)
    {
        Console.WriteLine(sr.ReadLine());
    }
    sr.Close();
}
```

在第 1 行，我们首先声明一个字符串变量 `path` 并文件路径赋值给该变量。

```csharp
string path = "c:\\File.txt";
```

注意，在编写路径时我们必须使用双斜杠 `\\`。这是因为如果我们只使用单斜杠，编译器会认为单斜杠是转义序列的开头并将 `\m` 解释为转义序列。这将导致错误。

在第 2 行，我们创建一个 `StreamReader` 实例。`StreamReader` 构造函数接收一个参数——要读取的文件路径。

```csharp
StreamReader sr = new StreamReader(path);
```

注意到我们在第 2 行跟在 `using` 单词后面的括号内创建了这个 `StreamReader` 实例吗？

这里的 `using` 关键字与我们编写指令时使用的那个不同。

这里的关键字确保了 `dispose()` 方法始终被调用。`dispose()` 方法是 `System` 命名空间中的一个预写方法，一旦文件和流不再需要，就会释放这些未托管资源。当我们使用 `using` 关键字时，我们确保即使发生异常，`dispose()` 方法也会被调用。在第 9 行我们手动关闭文件。在处理文件时，始终使用 `using` 关键字是一种良好的习惯。从第 4 行到第 7 行，我们使用 `while` 循环来读取文件。

```csharp
while (sr.EndOfStream != true)
{
    Console.WriteLine(sr.ReadLine());
}
```

`EndOfStream` 是 `StreamReader` 类的一个属性，当到达文件末尾时返回 `true`。只要没有到达文件末尾，`while` 循环就会继续运行。在 `while` 循环内部，我们有语句：

```csharp
Console.WriteLine(sr.ReadLine());
```

`sr.ReadLine()` 从文件中读取一行并作为字符串返回。然后使用 `Console.WriteLine()` 方法打印到屏幕上。

最后，在我们完成读取后，关闭文件以便其他程序可以使用。当你不再需要它时，你应该关闭文件。

```csharp
sr.Close();
```

就这样。这就是在 C# 中读取文本文件的方法。非常简单吧？

然而，上面的代码有一个问题。如果找不到 "myFile.txt"，这段代码将产生错误。在这里有两个选项。

### 选项 1：try...catch

第一个选项是使用所示的 `try...catch` 语句：

```csharp
try
{
    using (StreamReader sr = new StreamReader(path))
    {
     while (sr.EndOfStream)
     {
         Console.WriteLine(sr.ReadLine());
     }
     sr.Close();
 }
catch (FileNotFoundException e)
{
    Console.WriteLine(e.Message);
}
```

从 1 行到 11 行，我们在 `try` 块中尝试打开、读取并关闭文件。

从 11 行到 14 行，我们使用 `catch` 块在文件不存在时捕捉 `FileNotFoundException` 异常。在 `catch` 块中，我们打印错误语句告知用户未找到文件。

### 选项 2：File.Exists()

处理“找不到文件”场景的第二种方法是使用 `File` 类中的 `Exists()` 方法。正如名字所示`Exists()` 方法检查文件是否存在。`File` 类是 `System.IO` 命名空间中的预写类，它为单个文件的创建、复制、删除、移动和打开提供了静态方法。

要使用 `Exists()` 方法，我们使用 `if` 语句在用 `StreamReader` 打开并读取文件之前检查文件是否存在。

```csharp
if (File.Exists(path))
{
    using (StreamReader sr = new StreamReader(path))
    {
        while (sr.EndOfOfStream)
        {
            Console.WriteLine(sr.ReadLine());
        }
        sr.Close();
    }
}else
{
    //Do something else
}
```

在这个代码块中，我们可以编写代码在未找到文件时创建它。

如你所见，处理文件缺失的两种方法非常相似。然而，`File.Exists()` 方法是优选，因为它比 `try..catch` 语句更快。

## 写入文本文件

接下来，让我们看看如何向文本文件写入。

要写入文本文件，我们使用 `StreamWriter` 类。

如果你想向现有文件追加数据，可以像这样创建一个 `StreamWriter` 实例：

```csharp
StreamWriter sw = new StreamWriter(path, true);
```

其中 `path` 是文件的路径，`true` 表示我们想要追加数据。

如果你想覆盖文件中的任何现有数据，可以像这样创建一个 `StreamWriter` 实例：

```csharp
StreamWriter sw = new StreamWriter(path);
```

当我们创建 `StreamWriter` 实例时，构造函数会在指定的路径处查找文件。如果没有找到文件，它将创建该文件。

在实例化我们的 `StreamWriter` 对象后，我们可以像下面一样使用 `WriteLine()` 方法向文件中写入：

```csharp
sw.WriteLine("It is easy to write to a file.");
```

在完成文件写入后，我们必须使用 `Close()` 关闭文件：

```csharp
sw.Close();
```

注意，在写入文本文件时，将代码封装在 `using` 语句中也是良好的做法。下面的代码展示了所有这些内容如何结合的完整示例。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
namespace FileDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            //declaring the path to the file
            string path = "file.txt";
            //Writing to the file
            using(StreamWriter sw=new StreamWriter(path,true))
            {
                sw.WriteLine("ABC");
                sw.WriteLine("DEF");
                sw.Close();
            }
        // Reading from the file
        if (File.Exists(path))
        {
            using (StreamReader sr=new StreamReader(path))
            {
                while (!sr.EndOfStream)
                {
                    Console.WriteLine(sr.ReadLine());
                }
            }
        }
    }
}
```

```csharp
sr.Close();
}
Console.Read();
}
}
```
