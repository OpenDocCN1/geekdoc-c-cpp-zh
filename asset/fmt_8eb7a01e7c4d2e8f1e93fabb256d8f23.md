
```csharp
static void Main()
{
    FileStream file = new FileStream("Names.txt",
    FileMode.Create, FileAccess.Write);
    StreamWriter writer = new StreamWriter(file);
```

- 3. 如下所示添加一个名称数组。每个名称都填充了空格使其长度达到 10 个字符，以便你在稍后的练习中轻松地演示 `Seek()` 方法。

```csharp
string[] names = {"Anthony ",
                  "Belle ",
                  "Carolyn ",
                  "David ",
                  "Edwin ",
                  "Frannie ",
                  "Gina ",
                  "Hannah ",
                  "Inez ",
                  "Juan"};
```

- 4. 声明一个变量作为数组下标，然后将每个名称写入输出文件。

```csharp
int x;
for(x = 0; x < names.Length; ++x)
    writer.WriteLine(names[x]);
```

- 5. 关闭 `StreamWriter` 和 `FileStream`。此外添加两个大括号——一个用于 `Main()` 方法，一个用于类。

```csharp
writer.Close();
file.Close();
}
```

- 6. 保存文件，然后编译并执行它。在文本编辑器中打开新创建的 `Names.txt` 文件。文件内容如图 14-16 所示。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_691_0.png)

图 14-16 `CreateFileName` 程序创建的文件

# 第 14 章 文件与流

（续）

# 从文件中读取

在接下来的步骤中，你从 `CreateNameFile` 程序创建的文件读取文本。

- 1. 如下启动一个名为 `ReadNameFile` 的新文件：

```csharp
using static System.Console;
using System.IO;
class ReadNameFile
{
```

- 2. 启动 `Main()` 方法并声明一个 `FileStream`，使用与 `CreateNameFile` 程序相同的文件名。将文件模式声明为 `Open`，访问权限声明为 `Read`。声明一个关联该文件的 `StreamReader`。此外声明一个用于计数读取名称的整数和一个存储名称的字符串。

```csharp
static void Main()
{
    FileStream file = new FileStream("Names.txt",
    FileMode.Open, FileAccess.Read);
    StreamReader reader = new StreamReader(file);
    int count = 1;
    string name;
```

- 3. 显示标题，并从文件中读取第一行。当名称为 `null` 时，显示计数和名称，并增加计数。

```csharp
WriteLine("Displaying names:");
name = reader.ReadLine();
while(name != null)
{
    WriteLine(count + " " + name);
    name = reader.ReadLine();
    count++;
}
```

- 4. 关闭 `StreamReader` 和 `FileStream`。此外为方法和类添加大括号。

```csharp
reader.Close();
file.Close();
}
```

# 保存文件

（续）

- 5. 保存文件，然后编译并执行它。输出如图 14-17 所示。

```
Displaying all names
1 Anthony
2 Belle
3 Carolyn
4 David
5 Edwin
6 Frannie
7 Gina
8 Hannah
9 Inez
10 Juan
```

图 14-17 输出

# 从顺序文件中读取

当我们从顺序文件中读取数据时，正如 `SequentialFile` 程序（图 14-14）所示，程序从文件开始，按顺序读取直到文件结束。如果文件中的每个记录是 32 字节，那么指针将持有字节数。为了重新读取文件，你可以将其关闭并重新打开，但这产生了不必要的开销。相反，你可以使用 `Seek()` 方法和 `SeekOrigin` 枚举重定位文件指针。

```csharp
file.Seek(0, SeekOrigin.Begin);
```

表 14-6 列出了你可以使用的 `SeekOrigin` 枚举值。

| Member | 描述 |
| --- | --- |
| Begin | 流的开头 |
| Current | 当前的位置 |
| End | 流的结尾 |

表 14-6 `SeekOrigin` 枚举

图 14-18 是一个反复搜索文件以产生符合最低金额员工列表的程序。程序中的阴影部分表示与 `SequentialFile` 程序（图 14-14）的区别。在这个程序中，每当用户输入最低金额，文件指针就会设置为文件的开头。

```csharp
using System;
using static System.Console;
using System.IO;

class FindEmployees
{
    const char DELIM = ',';
    class Employee
    {
        public int EmpNum;
        public string Name;
        public double Salary;
    }
    static void Main()
    {
        const int END = 999;
        const string FILENAME = "Employee.txt";
        FileStream inFile = new FileStream(FILENAME, FileMode.Open, FileAccess.Read);
        StreamReader reader = new StreamReader(inFile);
        string recordIn;
        double minSalary;

        Write("Enter minimum salary to find or " + END + " to quit: ");
        minSalary = double.Parse(ReadLine());
        inFile.Seek(0, SeekOrigin.Begin);

        WriteLine("Displaying names:");
        int count = 1;
        while ((recordIn = reader.ReadLine()) != null)
        {
            string[] fields = recordIn.Split(DELIM);
            Employee emp = new Employee();
            emp.EmpNum = int.Parse(fields[0]);
            emp.Name = fields[1];
            emp.Salary = double.Parse(fields[2]);

            if (emp.Salary >= minSalary)
            {
                WriteLine("{0,-5}{1,-12}{2,-8}", count, emp.Name, emp.Salary);
            }
            count++;
        }
        reader.Close();
        inFile.Close();
    }
}
```

```cs
using System;
using static System.Console;
using System.IO;
class AccessSomeNames
{
    static void Main()
    {
        FileStream file = new FileStream("Names.txt",
        FileMode.Open, FileAccess.Read);
        StreamReader reader = new StreamReader(file);
```

- 2. 声明一个命名的常量 `END`，它表示一个输入值，允许用户使用程序。然后声明程序将使用的其他变量。

const int END = 999;

int count = 0;

int num;

int size;

string name;

- 3. 从输入文件中读取一行。只要有可用名称，就继续读取并计数。通过将文件长度除以存储的字符串的数量来计算每个名称的大小。

name = reader.ReadLine();

while (name != null)

{

    ++count;

    name = reader.ReadLine();

}

size = (int)file.Length / count;

- 4. 提示用户输入要读取的第一条记录编号，并从控制台读取该值。

Write("\nWhich number do you want to start? >> ");

int num = Convert.ToInt32(ReadLine());

- 5. 启动一个循环，只要用户不输入哨兵值 `END`，循环就会继续。在循环内部，显示用户的数字，然后使用 `Seek` 方法将文件指针定位于文件的正确位置。由于用户输入的数字从 1 开始，而文件位置从 0 开始，因此你通过

# 第 14 章 文件与流

（续上）

首先从用户的输入值中减去 1 来计算文件位置。然后，将计算出的记录数乘以文件中每个名称的大小。例如，如果每个名称长度为 10 字节，那么计算出的起始位置应该是 0、10、20、30 或其他基于名称大小的倍数方法。

```cs
while(num != END)
{
    WriteLine("Starting " + num + ":\n");
    file.Seek((num - 1) * size, SeekOrigin.Begin);
}
```

- 2. 在计算出的位置读取并写入名称。然后，在嵌套循环中，读取并写入所有剩余名称，直到文件末尾。

```cs
name = reader.ReadLine();
WriteLine(" " + name);
while(name != null)
{
    name = reader.ReadLine();
    WriteLine(" " + name);
}
```

- 3. 最后，提示用户新列表的下一个起始值，告知用户如何退出应用程序，并接受下一个输入值。为外部循环添加右括号。

- 4. 关闭 `StreamReader` 和 `File` 对象，并为方法和类添加右括号。

```cs
reader.Close();
file.Close();
}
```

- 5. 保存文件，然后进行编译并执行。图 14-20 显示了一个典型的执行过程，在此期间用户在不同的时间点显示了三组名称。

（继续）

## 理解序列化与反序列化

```
With which number do you want to start? >> 7
Starting with name 7:
Gina
Hannah
inez
Juan

With which number do you want to start?
(Enter 999 to quit) >> 2
Starting with name 2:
Belle
Carolyn
David
Edwin
Frannie
GGina
Hannah
inez
Juan

With which number do you want to start?
(Enter 999 to quit) >> 9
Starting with name 9:
inez
Juan

With which number do you want to start?
(Enter 999 to quit) >> 999
```

**图 14-20** `AccessSomeNames` 过程的典型执行

## 理解序列化与反序列化

写入文本文件允许你存储数据以供以后使用。然而，写入文本文件有两个缺点：

- 文本文件中的数据在记事本等文本编辑器中易读。虽然这个功能对开发人员测试程序很有有用，但它不是一种非常安全的数据存储方式。

- 当数据文件中的记录包含许多字段时，在将记录存储到磁盘之前，将每个字段转换为文本并用分隔符组合字段是非常繁琐的。同样，当你读取文本文件时，消除分隔符、将文本拆分为标记并将每个标记转换为正确的数据类型也有些不方便。一次性将对象写入文件会更方便。

C# 提供了一种名为序列化（serialization）的技术，可用于将对象写入文件或从数据文件中读取对象。序列化是将对象转换为字节流的过程。反序列化是相反的过程；它将字节流转换回对象。

要创建一个可以序列化的类，你需要用 `[Serializable]` 属性标记它，如图 14-21 中阴影语句所示。图中的 `Employee` 类与图 14-10 中的类相同，仅多了 `[Serializable]` 属性。

```cs
[Serializable]
class Employee
{
    public int EmpNum {get; set;}
    public string Name {get; set;}
    public double Salary {get; set;}
}
```

**图 14-21** 可序列化的 `Employee` 类

属性提供了一种信息与 C# 代码关联的方法。它们始终包含在方括号中。可以在 http://msdn.microsoft.com 搜索 C# 属性获取更多详情。

![](img/7516c1fecf7bbbe7af10cf209b17ae3700)

在标记为 `[Serializable]` 的类中，每个实例变量必须是可序列化的。默认情况下，C# 的简单类型是可以序列化的。但是，如果你的类引用其他对象，它们也必须是可序列化的。

如果你创建一个类并想将其对象写入文件，可以实现 `ISerializable` 接口，而不是用 `[Serializable]` 属性标记类。当你使用这种方法时，必须编写一个名为 `GetObjectData()` 的方法。用属性标记类更为简单。

使用序列化的程序包含两个命名空间：

* `System.Serialization.Formatters.Binary;`

* `System.Runtime.Serialization;`

当你创建一个将对象写入文件的程序时，你使用如下语句声明一个 `BinaryFormatter` 类的实例：

BinaryFormatter bf = new BinaryFormatter();

然后，如果你有一个带有对象数据的类，可以使用如下的语句将其写入输出文件流：

bf.Serialize(outFile, objectFilledData);

## Serialize 方法

`Serialize()` 方法接收两个参数——输出文件的引用以及一个可能包含任意数量数据字段的可序列化对象的引用。整个对象通过此单一语句写入数据文件。

同样，当你从数据文件读取内容时，使用如下的语句：

objectInstance = (Employee)formatter.Deserialize(inFile);

该语句使用 `BinaryFormatter` 的 `Deserialize()` 方法从文件中读取一个对象。该对象被强制类型并赋值给对象实例。然后你可以访问各个字段。无论对象包含多少字段，都通过此单一语句读取整个对象。

图 14-22 显示了一个将 `Employee` 类写入输出文件并将其读入程序的程序。在第一个语句处声明了 `FileStream`。用户输入 `Employee` 的 ID、姓名和薪资，完整的对象在第二个阴影语句中写入文件。当用户输入 999 时，完整的对象被关闭。
