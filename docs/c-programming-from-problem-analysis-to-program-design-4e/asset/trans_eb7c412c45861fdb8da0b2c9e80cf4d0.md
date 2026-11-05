
```csharp
else
{
    Console.WriteLine("{0} not found – using current " +
                       "directory", fileName);
}
Console.ReadKey( );
}
}
}
```

来自 DirectoryStructure 应用程序的输出显示在图 13-3 中。

![](img/36e48639a06772bcb0fa1ea2525b33a3_882_0.png)

**图 13-3** DirectoryStructure 应用程序的输出

Archive 显示为文件的 Attributes 的值。根据您运行的操作系统版本，您可能会看到 Normal 而不是 Archive。Normal 属性表示文件是标准文件，没有特殊属性，例如 ReadOnly。Archive 表示文件是备份或删除的候选对象。方法 GetAttributes() 返回一个 FileAttributes 枚举。枚举是一种特殊的值类型形式，为底层基本类型的值提供替代名称。枚举类型具有名称、底层类型和一组字段。

程序员定义枚举的一个示例可能是名为 DayOfWeek 的类型。可能的字段可以是 Sunday, Monday, Tuesday, Wednesday, Thursday, Friday 和 Saturday。Sunday 可以与整数 0 相关联，Monday 与 1 相关联，每个连续的日子为 2、3、4、5 和 6。枚举可以定义如下：

```csharp
public enum DayOfWeek
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}
```

枚举在类外部定义，使用 `enum` 关键字，并且通常提供 `public` 访问。在定义枚举之后，您可以使用这些值作为数据类型字段。例如，要打印字符串 "Tuesday"，您可以编写：

```csharp
Console.WriteLine("Today is {0}!", DayOfWeek.Tuesday);
```

输出如下：

```
Today is Tuesday!
```

您还可以使用显式类型转换来访问分配给该值的关联整数。例如，要显示与 Wednesday 关联的数字，您可以编写：

```csharp
Console.WriteLine("{0} = {1}", DayOfWeek.Wednesday,
                 (int)DayOfWeek.Wednesday );
```

输出如下：

```
Wednesday = 3
```

现在回顾示例 13-1。方法 `GetAttributes(fileName)` 返回文件的 `FileAttributes`。`FileAttributes` 是一个枚举。如图 13-3 所示，它返回的字段为 `Archive`。其他枚举的 `FileAttributes` 值包括 `Compressed`、`Device`、`Directory`、`Encrypted`、`Hidden`、`Normal`、`ReadOnly` 和 `System`。使用此类枚举使编码更简单，输出更易读。

## 目录类

与 File 类的成员类似，Directory 类中的所有成员都是 `public static` 方法。Directory 类提供用于创建目录和在目录及子目录之间移动的静态方法。表 13-3 列出了 Directory 类的一些更有趣的方法。

**表 13-3** Directory 类成员

| 公共静态成员 | 描述 |
|---|---|
| `CreateDirectory()` | 创建指定路径中的所有目录 |
| `Delete()` | 删除指定的目录 |
| `Exists()` | 确定给定路径是否引用现有目录 |
| `GetCreationTime()` | 获取目录的创建日期和时间 |
| `GetCurrentDirectory()` | 获取应用程序的当前工作目录 |
| `GetDirectories()` | 获取指定目录中的子目录名称 |
| `GetFiles()` | 返回指定目录中的文件名称 |
| `GetParent()` | 检索指定路径的父目录，包括绝对路径和相对路径 |
| `GetLastWriteTime()` | 返回指定文件或目录上次写入的日期和时间 |
| `Move()` | 将文件或目录及其内容移动到新位置 |
| `SetCurrentDirectory()` | 将应用程序的当前工作目录设置为指定目录 |

.NET 还包括 DirectoryInfo 和 FileInfo 类。这些类与它们的名称对应类 Directory 和 File 非常相似。它们的区别在于 DirectoryInfo 和 FileInfo 类都具有实例方法而不是静态成员。它们是 FileSystemInfo 类的直接后代。

可以从 DirectoryInfo 和 FileInfo 类实例化对象。不能从 File 和 Directory 类实例化对象。

## FileInfo 和 DirectoryInfo 类

FileInfo 和 DirectoryInfo 类提供了超出 File 和 Directory 类方法成员的功能。它们都有一系列公共属性，当然两者都提供公共构造函数。这两个类都不能被继承。如果您计划多次引用和使用文件或目录，您需要考虑实例化其中一个或两个类的对象并使用其实例方法。表 13-4 显示了 FileInfo 类的一些关键属性。

**表 13-4** FileInfo 属性

| 公共成员 | 描述 |
|---|---|
| `Attributes` | 获取或设置当前 FileSystemInfo 的 FileAttributes |
| `Directory` | 获取父目录的实例 |
| `DirectoryName` | 获取表示目录完整路径的字符串 |
| `Exists` | 获取指示文件是否存在的的值 |
| `Extension` | 获取表示文件扩展名部分的字符串 |
| `FullName` | 获取目录或文件的完整路径 |
| `LastAccessTime` | 获取或设置当前文件或目录上次访问的时间 |
| `LastWriteTime` | 获取或设置当前文件或目录上次写入的时间 |
| `Length` | 获取当前文件的大小 |
| `Name` | 获取文件的名称 |

表中未显示 FileInfo 或 DirectoryInfo 类的公共方法。但是请注意，File 和 Directory 类的大多数公共静态方法在 FileInfo 和 DirectoryInfo 类中作为实例方法可用。

DirectoryInfo 类添加了另外两个关键属性：Parent 和 Root。Parent 获取指定子目录的父目录。Root 获取路径的根部分。在处理与文件和/或目录相关的路径时，您应非常小心。路径必须准确，否则会引发异常。

示例 13-2 为示例 13-1 中说明的 DirectoryStructure 示例添加了额外功能。实例化了一个 DirectoryInfo 对象，并且 foreach 循环结构使用 FileInfo 类。

### 示例 13.2

```csharp
DirectoryInfo dir = new DirectoryInfo(".");
Console.WriteLine("Current Directory: \n{0}\n",
                  Directory.GetCurrentDirectory());
Console.WriteLine("File Name".PadRight(52) +
                  "Size".PadRight(10) + "Creation Time");
foreach (FileInfo fil in dir.GetFiles("*.*"))
{
    string name = fil.Name;
    long size = fil.Length;
    DateTime creationTime = fil.CreationTime;
    Console.WriteLine("{0} {1,12:N0} {2,20:g}", name.PadRight(45),
                      size, creationTime);
}
```

在示例 13-2 中实例化 DirectoryInfo 对象后，将调用 GetCurrentDirectory() 方法以显示当前目录。调用 DirectoryInfo 类的 GetFiles() 方法以检索当前目录中的文件集合。用于显示时访问 FileInfo 类的 Name、Size 或 Length 和 CreationTime 属性。修订后示例的输出显示在图 13-4 中。

![](img/36e48639a06772bcb0fa1ea2525b33a3_886_0.png)

**图 13-4** 来自修订的 DirectoryStructure 应用程序的输出

在审查代码时，您会注意到 string 类的 PadRight() 方法被用来格式化 FileInfo Name 属性返回的文件名。

> **注意**
>
> 示例 13-2 中的 PadRight() 将文件名左对齐，并在右侧添加空格，使其填充 45 个字符位置。size 或 Length 和 CreationTime 值使用格式说明符右对齐。格式说明符中的正整数（12 和 20）表示值应右对齐。

