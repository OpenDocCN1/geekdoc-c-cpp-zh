
## 4. 使用正则表达式替换字符串中的特殊字符

如果字符串包含特殊字符并且需要删除/替换这些字符，则可以使用正则表达式：

```csharp
Regex.Replace(Stringwithchars, @"[^0-9a-zA-Z]+", "")
```

这段代码会删除所有特殊字符，但如果不需要删除“-”和“.”等某些字符，则可以使用下面的正则表达式：

```csharp
Regex.Replace(Stringwithchars, @"[^0-9a-zA-Z.\-]+", "")
```

## 两分题及答案

### Q.1 什么是事件和委托？

答：事件是由控件发送的消息，用于通知某个操作的发生。然而，无法预知哪个对象接收该事件。因此，.NET 提供了一种称为委托（Delegate）的特殊类型，它充当发送方对象和接收方对象之间的中介。

### Q.2 什么是委托？请解释。

答：委托是保存对方法引用的变量。因此，它是函数指针或引用类型。所有委托都派生自 System.Delegate 命名空间。委托及其引用的方法可以具有相同的签名。

声明委托：

```csharp
public delegate void AddNumbers(int n);
```

声明委托后，必须使用 new 关键字通过委托创建对象。

```csharp
AddNumbers an1 = new AddNumbers(number);
```

委托为引用方法提供了一种封装，当调用委托时，该方法会在内部被调用。

### Q.3 什么是正则表达式？如何使用正则表达式搜索字符串？

答：正则表达式是用于匹配一组输入的模板。模式可以由运算符、构造或字符字面量组成。Regex 用于字符串解析和替换字符串。

例如：

```csharp
{
    if (System.Text.RegularExpressions.Regex.IsMatch(s, "Python"))
    {
        Console.WriteLine("Match found");
    }
}
```

上面的示例在 languages 数组的一组输入中搜索“Python”。它使用 Regex.IsMatch，如果输入中找到该模式，则返回 true。模式可以是表示我们想要匹配的输入的任何正则表达式。

### Q.4 什么是事件？

答：事件是用户操作，会向应用程序生成通知，应用程序必须对此作出响应。用户操作可以是鼠标移动、按键等。

在编程中，引发事件的类称为发布者，响应/接收事件的类称为订阅者。一个事件应至少有一个订阅者；否则，该事件永远不会被引发。

委托用于声明事件。

```csharp
public delegate void PrintNumbers();
event PrintNumbers myEvent;
```

### Q.5 委托有哪些不同类型？

答：委托的不同类型包括：

- **单播委托：** 只能调用单个方法的委托。
- **多播委托：** 可以调用多个方法的委托。`+` 和 `-` 运算符分别用于订阅和取消订阅。
- **泛型委托：** 它不需要定义委托实例。它有三种类型：Action、Func 和 Predicate。
  - **Action：** 在上面的委托和事件示例中，我们可以使用 Action 关键字替换委托和事件的定义。Action 委托定义的方法可以带参数调用，但不返回结果。
    ```csharp
    public delegate void deathInfo();
    public event deathInfo deathDate;
    // Replacing with Action
    public event Action deathDate;
    ```
  - **Predicate：** 定义可带参数调用并始终返回 bool 的方法。`Predicate<string> myDel` 与 `delegate bool myDel(string s);` 相同。

## 长问答题

- Q.1 讨论 C# 中的委托。（参考第 10.1 节）
- Q.2 C# 中的 lambda 表达式是什么？（参考第 10.2 节）
- Q.3 讨论 C# 中 lambda 表达式的用途和应用。（参考第 10.2 节）
- Q.4 讨论 C# 中事件的发布者-订阅者模型。（参考第 10.3 节）
- Q.5 C# 中如何处理事件？（参考第 10.3 节）

### Q.6 编写一个使用委托将英尺转换为英寸的 C# 程序。

AU：2018 年 5 月，7 分

答：

```csharp
/*
 * C# Program to Convert Feet to Inches using Delegates
 */
using System;

public delegate double Conversion(double from);

class DelegateDemo
{
    public static double FeetToInches(double feet)
    {
        return feet * 12;
    }

    static void Main()
    {
        Conversion doConversion = new Conversion(FeetToInches);
        Console.Write("Enter Feet: ");
        double feet = Double.Parse(Console.ReadLine());
        double inches = doConversion(feet);
        Console.WriteLine("\n{0} Feet = {1} Inches.\n", feet, inches);
        Console.ReadLine();
    }
}
```

## 第二单元

## 第 11 章

## C# 高级特性 II——文件和 I/O

**教学大纲：** 核心 C#。

| 节号 | 主题名称 | 页码 |
| :---: | :---: | :---: |
| 11.1 | 文件 | 11 - 2 |
| 11.2 | C# I/O 类 | 11 - 2 |
| | 两分题及答案 | 11 - 13 |
| | 长问答题 | 11 - 14 |

### 11.1 文件

**概念**

文件用于持久化数据。文件是存储在磁盘上的数据集合，具有特定的名称和目录路径。

可以对文件执行多种操作，即创建文件、写入文件、读取文件、保存文件、关闭文件和打开文件。

**说明**

此外，还有一些操作可获取文件信息，例如文件名、文件大小、文件属性（只读等）、文件路径、创建日期和时间等。

当打开文件进行读取或写入时，它便成为流。流基本上是通过通信路径的字节序列。主要有两种流：输入流和输出流。

输入流用于从文件读取数据（读操作），输出流用于向文件写入数据（写操作）。

在 C# 中，System.IO 命名空间包含各种用于对文件执行操作的类。

### 11.2 C# I/O 类

| 序号 | I/O 类 | 描述 |
|---|---|---|
| 1. | FileStream | 用于从文件中的任意位置读取和向任意位置写入。 |
| 2. | BinaryReader | 从二进制流读取基元数据。 |
| 3. | BinaryWriter | 以二进制格式写入基元数据。 |
| 4. | File | 用于操作文件。 |
| 5. | StreamReader | 用于从字节流读取字符。 |
| 6. | StreamWriter | 用于将字符写入流。 |
| 7. | StringReader | 用于从字符串缓冲区读取。 |
| 8. | StringWriter | 用于写入字符串缓冲区。 |
| 9. | Directory | 帮助操作目录结构。 |
| 10. | DirectoryInfo | 用于对目录执行操作。 |
| 11. | BufferedStream | 字节流的临时存储。 |
| 12. | DriveInfo | 提供有关驱动器的信息。 |
| 13. | FileInfo | 用于对文件执行操作。 |
| 14. | MemoryStream | 用于随机访问存储在内存中的流式数据。 |
| 15. | Path | 对路径信息执行操作。 |

### 11.2.1 FileStream 类

- FileStream 类用于读取文件、写入文件和关闭文件。
- 此类派生自抽象类 Stream。
- 使用 FileStream 类：
  - 创建 FileStream 对象（用于创建新文件或打开现有文件）。
  - 语法：

    ```csharp
    FileStream <object_name> = new FileStream(<file_name>, <FileMode Enumerator>, <FileAccess Enumerator>, <FileShare Enumerator>);
    ```

例如，创建一个 FileStream 对象 `F`，用于读取名为 `Example.txt` 的文件，如下所示：

```csharp
FileStream My_File = new FileStream("Example.xlsx", FileMode.Open, FileAccess.ReadWrite, FileShare.ReadWrite);
```

其中，

**1. FileMode**

FileMode 枚举器定义了用于打开文件的各种成员。

FileMode 枚举器的成员包括：

| 模式 | 描述 |
|---|---|
| Append | 打开现有文件并将光标置于文件末尾；如果文件不存在，则创建该文件。 |
| Create | 创建新文件。如果文件已存在，则会覆盖该文件。 |
| CreateNew | 也用于创建新文件。如果文件已存在，则会引发异常。 |
| Open | 打开现有文件。 |
| OpenOrCreate | 向操作系统指定：如果文件存在，则应打开文件；否则应创建新文件。 |
| Truncate | 打开现有文件并将其大小截断为零字节。 |

