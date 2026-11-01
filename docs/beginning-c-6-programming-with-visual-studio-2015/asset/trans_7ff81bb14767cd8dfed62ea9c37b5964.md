
examined. 此目录包含调用此代码的应用程序。你将在稍后，‘路径名称和相对路径’部分中更详细地了解这一点。

大多数 FileInfo 方法以这种方式镜像 File 方法。在大多数情况下，使用哪种技术并不重要，尽管以下标准可以帮助你决定哪种更合适：

- 如果只进行一次方法调用，使用静态 File 类上的方法是有意义的——单次调用会更快，因为 .NET Framework 不必经历实例化新对象然后调用方法的过程。
- 如果你的应用程序对文件执行多个操作，那么实例化 FileInfo 对象并使用其方法更有意义——这可以节省时间，因为对象已经引用文件系统上的正确文件，而静态类每次都必须找到它。

FileInfo 类还公开与底层文件相关的属性，其中一些可以被操作以更新文件。其中许多属性继承自 FileSystemInfo，因此适用于 FileInfo 和 DirectoryInfo 类。FileSystemInfo 的属性如表 18-4 所示。

### 表 18-4：FileSystemInfo 属性

| 属性 | 描述 |
|---|---|
| Attributes | 获取或设置当前文件或目录的属性，使用 FileAttributes 枚举。 |
| CreationTime, CreationTimeUtc | 获取或设置当前文件的创建日期和时间，以协调世界时（UTC）和非 UTC 版本提供。 |
| Extension | 检索文件的扩展名。此属性为只读。 |
| Exists | 确定文件是否存在。这是一个只读抽象属性，在 FileInfo 和 DirectoryInfo 中被重写。 |
| FullName | 检索文件的完整路径。此属性为只读。 |
| LastAccessTime, LastAccessTimeUtc | 获取或设置当前文件上次被访问的日期和时间，以 UTC 和非 UTC 版本提供。 |
| LastWriteTime, LastWriteTimeUtc | 获取或设置当前文件上次被写入的日期和时间，以 UTC 和非 UTC 版本提供。 |
| Name | 检索文件的完整路径。这是一个只读抽象属性，在 FileInfo 和 DirectoryInfo 中被重写。 |

特定于 FileInfo 的属性如表 18-5 所示。

### 表 18-5：FileInfo 属性

| 属性 | 描述 |
|---|---|
| Directory | 检索表示包含当前文件的目录的 DirectoryInfo 对象。此属性为只读。 |
| DirectoryName | 返回文件目录的路径。此属性为只读。 |
| IsReadOnly | 文件只读属性的快捷方式。此属性也可通过 Attributes 访问。 |
| Length | 获取文件的大小（以字节为单位），返回为 long 值。此属性为只读。 |

## DirectoryInfo 类

DirectoryInfo 类的工作方式与 FileInfo 类完全相同。它是一个实例化对象，表示机器上的单个目录。与 FileInfo 类类似，许多方法调用在 Directory 和 DirectoryInfo 之间重复。选择使用 File 或 FileInfo 的方法的准则也适用于 DirectoryInfo 方法：

- 如果只进行一次调用，请使用静态 Directory 类。
- 如果进行一系列调用，请使用实例化的 DirectoryInfo 对象。

DirectoryInfo 类继承了大部分属性自 FileSystemInfo，FileInfo 也是如此，尽管这些属性操作的是目录而不是文件。还有两个特定于 DirectoryInfo 的属性，如表 18-6 所示。

### 表 18-6：DirectoryInfo 类独有的属性

| 属性 | 描述 |
|---|---|
| Parent | 检索表示包含当前目录的目录的 DirectoryInfo 对象。此属性为只读。 |
| Root | 检索表示当前卷根目录的 DirectoryInfo 对象——例如 C:\ 目录。此属性为只读。 |

## 路径名称和相对路径

在 .NET 代码中指定路径名时，可以使用绝对或相对路径名。绝对路径名明确指定来自已知位置的文件或目录——例如 C: 驱动器。

### 表 18-7：流类

| 类 | 描述 |
|---|---|
| FileStream | 表示可以写入、读取或同时进行的文件。此文件可以异步或同步地写入和读取。 |
| StreamReader | 从流中读取字符数据，可以使用 FileStream 作为基类创建。 |
| StreamWriter | 向流写入字符数据，可以使用 FileStream 作为基类创建。 |

现在让我们看看如何使用这些类。

## FileStream 对象

FileStream 对象表示指向磁盘或网络路径上文件的一个流。尽管该类确实公开了从文件读取和写入字节的方法，但最常见的是你会使用 StreamReader 或 StreamWriter 来执行这些功能。这是因为 FileStream 类操作字节和字节数组，而 Stream 类操作字符数据。字符数据更容易处理，但某些操作，例如随机文件访问（访问文件中间某点的数据），只能由 FileStream 对象执行。你将在本章后面了解更多关于此的内容。

创建 FileStream 对象有几种方法。构造函数有许多不同的重载，但最简单的一个只需要两个参数：文件名和 FileMode 枚举值：

```
FileStream aFile = new FileStream(filename, FileMode.<Member>);
```

FileMode 枚举有多个成员，指定文件如何打开或创建。你很快就会看到这些可能性。另一个常用的构造函数如下：

```
FileStream aFile =
new FileStream(filename, FileMode.<Member>, FileAccess.<Member>);
```

第三个参数是 FileAccess 枚举的成员，是指定流用途的一种方式。FileAccess 枚举的成员如表 18-8 所示。

### 表 18-8：FileAccess 枚举成员

| 成员 | 描述 |
|---|---|
| Read | 仅以只读方式打开文件 |
| Write | 仅以只写方式打开文件 |
| ReadWrite | 以读写方式打开文件 |

尝试执行 FileAccess 枚举成员未指定的操作将导致抛出异常。此属性通常用作根据用户授权级别调整用户对文件的访问权限的一种方式。

在不使用 FileAccess 枚举参数的 FileStream 构造函数版本中，使用默认值，即 FileAccess.ReadWrite。

FileMode 枚举成员如表 18-9 所示。使用每个值时实际发生的情况取决于指定的文件名是否引用现有文件。请注意，本表中条目指的是流在创建时指向文件中的位置，这将在下一节中详细介绍。除非另有说明，否则流指向文件的开头。

### 表 18-9：FileMode 枚举成员

| 成员 | 文件存在时的行为 | 文件不存在时的行为 |
|---|---|---|
| Append | 文件被打开，流定位在文件末尾。只能与 FileAccess.Write 结合使用。 | 创建一个新文件。只能与 FileAccess.Write 结合使用。 |
| Create | 文件被销毁，并在其位置创建新文件。 | 创建一个新文件。 |
| CreateNew | 抛出异常。 | 创建一个新文件。 |
| Open | 文件被打开，流定位在文件开头。 | 抛出异常。 |
| OpenOrCreate | 文件被打开，流定位在文件开头。 | 创建一个新文件。 |
| Truncate | 文件被打开并擦除。流定位在文件开头。原始文件创建日期被保留。 | 抛出异常。 |

File 和 FileInfo 类都公开 OpenRead() 和 OpenWrite() 方法，使创建 FileStream 对象变得更容易。第一个以只读访问打开文件，第二个允许只写访问。这些方法提供快捷方式，因此你不必以参数形式向 FileStream 构造函数提供所有所需信息。例如，以下代码行以只读访问打开 Data.txt 文件：

```
FileStream aFile = File.OpenRead("Data.txt");
```
