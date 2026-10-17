
虽然 `Lambda` 表达式是 `LINQ` 的一个组成部分，但你可以将其用于任何可以使用委托的地方。因此，`.NET Framework` 提供了许多预定义委托，可用于表示作为参数传递的方法，无需你先声明显式的委托类型。

由于返回布尔值的委托很常见，`.NET Framework` 定义了一个 `Predicate<T>` 委托，它被 `Array` 和 `List<>` 类中的许多方法使用。

尽管 `Predicate<T>` 定义了一个总是返回布尔值的委托，但 `Func` 委托系列封装了一个具有指定返回类型和 0 到 16 个输入参数的方法。

由于 `Predicate<T>` 和 `Func` 委托都有返回类型，`Action` 委托系列表示具有 `void` 返回类型的方法。与 `Func` 委托一样，`Action` 委托也接受 0 到 16 个输入参数。

## 延迟执行

与许多传统的数据查询技术不同，直到你实际遍历 `LINQ` 查询时，该查询才会被评估。这种称为**惰性求值**的方法的一个优点是，它允许原始集合中的数据在查询执行之后、查询识别的数据检索之前发生变化。最终，这意味着你始终拥有最新的数据。

尽管 `LINQ` 倾向于使用惰性求值，但使用任何聚合函数的查询都必须首先遍历所有元素。这些函数（如 `Count`、`Max`、`Average` 和 `First`）返回单个值，并且在不使用显式 `foreach` 语句的情况下执行。

## 延迟执行与链接查询

延迟执行的另一个优点是它允许高效地链接查询。因为查询对象表示的是查询本身，而不是查询的结果，所以它们可以轻松地进行链接或重用，而不会导致潜在的高成本数据获取操作。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_303_0.png)

你还可以通过将 `foreach` 语句紧接在查询表达式之后，或调用 `ToList` 或 `ToArray` 方法来强制立即评估，有时这被称为**贪婪求值**。你还可以使用 `ToList` 或 `ToArray` 将数据缓存到单个集合对象中。

## 总结

`LINQ` 采用了诸如 Haskell 等功能语言以及其他研究语言的最佳理念，并将它们结合在一起，引入了一种一致的方式来自定义查询数据，无论原始数据源是什么，都使用简单的声明式或基于方法的语法。通过允许以与源无关的方式编写查询，`LINQ` 使得可以访问多种数据源，包括数据库、XML 文件和内存集合。

使用类似于 SQL 查询的语法，`LINQ` 的声明式语法使得查询成为与算术运算和控制流语句一样的一等语言构造。`LINQ` 实际上实现为 `IEnumerable<T>` 接口上的一组扩展方法，这些方法接受 `Lambda` 表达式作为参数。`Lambda` 表达式以表达式 `Lambda` 或语句 `Lambda` 的形式存在，是编写匿名委托的一种紧凑方式。

当你刚开始使用 `LINQ` 时，你不需要大量使用 `Lambda` 表达式，但随着你对它们越来越熟悉，你会发现它们极其强大。

## 问答

- **问. 什么是 LINQ？**

  - **答.** `LINQ` 是一组技术，它将查询功能直接集成到 C# 语言中，并通过为每个受支持的数据源提供相同的查询语言，消除了处理数据和处理对象之间常见的语言不匹配。

- **问. 什么是 Lambda 表达式？**

  - **答.** `Lambda` 表达式代表了一种紧凑和简洁的方式来编写匿名委托，并且可以在任何传统委托可以使用的地方使用。

## 练习

### 测验

- 1. `LINQ` 的声明式语法和方法语法之间有区别吗？

- 2. `LINQ` 查询何时执行？

- 3. `Lambda` 表达式的底层委托类型是什么？

### 答案

- 1. 选择使用声明式语法还是方法语法完全是个人的选择，取决于你认为哪种更容易阅读。无论选择哪种，执行查询的结果都将相同。

- 2. 默认情况下，`LINQ` 利用查询的延迟执行。这意味着查询实际上不会执行，直到使用 `foreach` 语句遍历结果时。

- 3. `Lambda` 表达式本质上是无类型的，因此它们没有底层类型；然而，它们可以隐式转换为任何兼容的委托类型。

### 习题

- 1. 修改 `AddressBook` 项目中 `MainWindow` 类的 `Search_Click` 方法，使其将 `this.DataContext` 设置为对 `contacts` 集合查询的结果。此查询应选择集合中 `FirstName` 或 `LastName` 属性包含 `this.searchCriterias.Text` 中值的任何元素。

- 2. 修改 `Search_Click` 方法，使得如果搜索类别复选框被选中，也使用选定的类别进行查询。

# 第三部分

# 数据处理

- 第 13 小时：使用文件和流 289

- 第 14 小时：处理 XML 311

- 第 15 小时：处理数据库 329

## 第 13 小时

# 使用文件和流

**本小时您将学习：**

- 文件和目录

- 读取和写入数据

- 二进制文件

- 缓冲流

- 文本文件

在第 9 小时“处理数组和集合”和第 12 小时“理解查询表达式”中，您学习了应用程序如何与存储在集合中的数据一起工作，以及如何查询和操作这些数据。虽然这些是常见的活动，但许多应用程序需要从磁盘上的文件或存储中读取或获取数据。

`.NET Framework` 将文件视为数据流。**流**是数据包（表示为字节）的顺序流。数据流有一个底层存储介质，通常称为**后备存储**，它为流提供源。幸运的是，`.NET Framework` 通过提供的 `File`、`Directory` 和 `Path` 类使文件和目录的处理变得更加容易。

`System.IO` 命名空间包含您需要处理有缓冲和无缓冲流的所有类。缓冲流允许操作系统创建自己的内部缓冲区，用于以最高效的增量读取和写入数据。

在本小时中，您将学习如何使用 `File`、`Directory` 和 `Path` 类探索和文件管理系统，以及读写文件。您还将学习如何使用 `Stream` 类或其任何派生类执行更复杂的读写操作。

## 文件和目录

你可以将文件看作是具有明确名称和持久后备存储的字节序列。文件通过目录路径、磁盘存储以及文件和目录名称进行操作。`.NET Framework` 在 `System.IO` 命名空间中提供了多个类，使处理文件变得容易。

## 处理路径

路径是一个字符串，提供文件或目录的位置，可以包含绝对或相对位置信息。**绝对路径**完全指定了一个位置，而**相对路径**指定了部分位置。使用相对路径时，当前位置是定位指定文件的起点。

> **当前位置**
>
> 每个进程都有一个进程范围的“当前位置”，通常是（但不总是）进程可执行文件加载的位置。

`Path` 类提供静态方法，以跨平台方式对路径字符串执行操作。虽然大多数 `Path` 类成员不与文件系统交互，但它们会验证指定的路径字符串是否包含有效字符。表 13.1 显示了常用方法。

**表 13.1** `Path` 类的常用方法

| 方法 | 描述 |
| :--- | :--- |
| `ChangeExtension` | 更改扩展名 |
| `Combine` | 将字符串组合为路径 |
| `GetDirectoryName` | 获取指定路径的目录名 |
| `GetExtension` | 获取指定路径的扩展名 |
| `GetFileName` | 获取指定路径的文件名和扩展名 |
| `GetFileNameWithoutExtension` | 获取指定路径的文件名（不含扩展名） |
| `GetPathRoot` | 获取指定路径的根目录 |
| `GetRandomFileName` | 获取随机名称 |

## 表 13.1 `Path` 类中常用的方法

| 方法 | 描述 |
| :--- | :--- |
| `GetTempFileName` | 创建一个具有唯一随机名称的临时文件，并返回该文件的完整路径 |
| `GetTempPath` | 获取临时文件夹的路径 |

## 特殊目录

Windows 操作系统包含许多应用程序常用的“特殊”文件夹。通常，这些文件夹由操作系统设置；然而，用户在安装某个版本的 Windows 时也可以显式地设置它们。因此，在许多机器上，这些文件夹的位置或名称可能并不相同。

查找这些“特殊”目录（例如 Windows 目录）的最合适方法是使用 `Environment.GetFolderPath` 方法。该方法接受 `Environment.SpecialFolder` 枚举值中的一个，用于指示要获取其路径的特殊文件夹。

表 13.2 展示了一些常用的 `Environment.SpecialFolder` 值。

### 表 13.2 常见的 `Environment.SpecialFolder` 值

| 成员 | 描述 |
| :--- | :--- |
| `ApplicationData` | 作为当前漫游用户的应用程序专用数据通用存储位置的目录。 |
| `CommonApplicationData` | 作为所有用户使用的应用程序专用数据通用存储位置的目录。 |
| `LocalApplicationData` | 作为当前非漫游用户使用的应用程序专用数据通用存储位置的目录。 |
| `CommonDocuments` | 包含所有用户通用文档的文件系统目录。此特殊文件夹适用于 Windows NT 系统、Windows 95 以及安装了 shfolder.dll 的 Windows 98 系统。 |
| `Desktop` | 逻辑桌面，而非物理文件系统位置。 |
| `DesktopDirectory` | 用于在桌面上物理存储文件对象的目录。请勿将此目录与桌面文件夹本身混淆，后者是一个虚拟文件夹。 |
| `MyDocuments` | “我的文档”文件夹。此成员等效于 `Personal`。 |
| `Personal` | 作为文档通用存储位置的目录。 |
| `System` | 系统目录。 |
| `Windows` | Windows 目录或 SYSROOT。这对应于 `%windir%` 或 `%SYSTEMROOT%` 环境变量。 |

## `DirectoryInfo` 和 `FileInfo` 类

`DirectoryInfo` 和 `FileInfo` 类都继承自 `FileSystemInfo` 类，该类包含文件和目录操作共有的方法，并且可以表示文件或目录。当实例化 `FileSystemInfo` 时，目录或文件信息会被缓存，因此必须使用 `Refresh` 方法对其进行刷新，以确保信息的实时性。

`DirectoryInfo` 类包含提供众多属性和方法的实例成员，用于执行常见的操作，如复制、移动、创建和枚举目录。`DirectoryInfo` 类中常用的方法和属性列于表 13.3 中。

### 表 13.3 常见的 `DirectoryInfo` 成员

| 成员 | 描述 |
| :--- | :--- |
| `Create` | 创建一个目录 |
| `CreateSubdirectory` | 在指定路径上创建一个子目录 |
| `Delete` | 删除当前目录，可选择性删除所有文件和子目录 |
| `EnumerateDirectories` | 获取当前目录中目录信息的一个可枚举集合 |
| `EnumerateFiles` | 获取当前目录中文件信息的一个可枚举集合 |
| `EnumerateFileSystemInfos` | 获取当前目录中文件和目录信息的一个可枚举集合 |
| `FullName` | 获取当前目录的完整路径 |
| `MoveTo` | 将当前目录及其所有文件和子目录移动到新位置 |
| `Name` | 获取当前目录的名称 |
| `Parent` | 获取当前目录的父目录 |
| `Refresh` | 刷新缓存的目录信息 |
| `Root` | 获取路径的根部分 |

示例 13.1 展示了 `DirectoryInfo` 类如何执行一些常见操作。

### 示例 13.1 使用 `DirectoryInfo` 类

```csharp
public class DirectoryInfoExample
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();

        DirectoryInfo directoryInfo = new DirectoryInfo(tempPath);
        try
        {
            if (directoryInfo.Exists)
            {
                Console.WriteLine("The directory already exists.");
            }
            else
            {
                directoryInfo.Create();
                Console.WriteLine("The directory was successfully created.");
                directoryInfo.Delete();
                Console.WriteLine("The directory was deleted.");
            }
        }
        catch (IOException e)
        {
            Console.WriteLine("An error occurred: {0}", e.Message);
        }
    }
}
```

`FileInfo` 类包含提供众多属性和方法的实例成员，用于执行常见的文件操作，如复制、移动、创建和打开文件。常用的方法和属性列于表 13.4 中。

### 表 13.4 常见的 `FileInfo` 成员

| 成员 | 描述 |
| :--- | :--- |
| `AppendText` | 创建 `StreamWriter` 以将文本追加到当前文件 |
| `CopyTo` | 将当前文件复制到新文件 |
| `Create` | 创建一个文件 |
| `CreateText` | 创建或打开文件以写入文本 |
| `Delete` | 删除当前文件 |
| `Directory` | 获取父目录 |
| `DirectoryName` | 获取父目录的名称 |
| `Exists` | 确定当前文件是否存在于磁盘上 |
| `Extension` | 当前文件的扩展名 |
| `FullName` | 获取当前文件的完整路径 |
| `IsReadOnly` | 获取或设置一个值，以确定当前文件是否为只读 |
| `Length` | 当前文件的大小 |
| `MoveTo` | 将当前文件移动到新位置 |
| `Name` | 获取当前文件的名称 |
| `Open` | 打开一个文件 |
| `OpenRead` | 打开现有文件以进行读取 |
| `OpenText` | 打开现有文本文件以进行读取 |
| `OpenWrite` | 打开现有文件以进行写入 |
| `Refresh` | 刷新缓存的文件信息 |
| `Replace` | 用当前文件的内容替换指定文件的内容 |

示例 13.2 展示了 **FileInfo** 类如何执行一些常见操作。

### 示例 13.2 使用 `FileInfo` 类

```csharp
public class FileInfoExample
{
    public static void Main()
    {
        string tempFile = Path.GetTempFileName();

        FileInfo fileInfo = new FileInfo(tempFile);
        try
        {
            if (!fileInfo.Exists)
            {
                using (StreamWriter writer = fileInfo.CreateText())
                {
                    writer.WriteLine("Line 1");
                    writer.WriteLine("Line 2");
                }
            }

            fileInfo.CopyTo(Path.GetTempFileName());
            fileInfo.Delete();
        }
        catch (IOException e)
        {
            Console.WriteLine("An error occurred: {0}", e.Message);
        }
    }
}
```

> **流是可释放的**
>
> 在使用完流后，请确保通过调用 **Close** 方法来释放该流。你也可以将流包裹在 **using** 语句中，这是确保流正确关闭的首选方式。
>
> *顺便提一下*

## 动手试一试

### 使用 `DirectoryInfo` 和 `FileInfo` 类

要了解如何使用 **DirectoryInfo** 和 **FileInfo** 类，请按照以下步骤操作。请在本练习结束时保持 Visual Studio 打开，因为稍后你会用到此应用程序。

- 1. 创建一个新的控制台应用程序。

- 2. 在 `Program.cs` 文件的 **Main** 方法中，在 `C:\Windows\Web\Wallpaper` 目录上创建一个新的 **DirectoryInfo** 实例。使用以下代码获取此文件夹的路径：

## 目录和文件类

如果你不想创建 `DirectoryInfo` 或 `FileInfo` 类的实例，可以使用 `Directory` 或 `File` 类。这些类仅提供静态方法，用于执行 `DirectoryInfo` 和 `FileInfo` 类提供的相同的目录和文件操作。

`Directory` 类的常用方法如表 13.5 所示。

### 表 13.5 `Directory` 类的常用方法

| 方法 | 描述 |
| :--- | :--- |
| `CreateDirectory` | 创建指定路径中的所有目录 |
| `Delete` | 删除指定目录 |
