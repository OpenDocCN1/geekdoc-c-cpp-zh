
在前面的代码片段中，创建了一个`ReadLine`活动。此`ReadLine`活动创建`Bookmark`类的实例并等待书签被恢复。当`Bookmark`被恢复时，`ReadLine`活动将数据分配给结果参数。

- 5. 在键盘上按 CTRL+F5 键组合运行`BookmarkResume`应用程序。运行应用程序时，它会提示输入你的姓名，如图 28.15 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1417_0.png)

输入姓名后，例如 Kabir，它会显示输出，如图 28.16 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1417_1.png)

现在，让我们总结本章讨论的主要主题。

## 摘要

在本章中，你学习了 WF 的新特性和其组件。接下来，你学习了活动和工作流类型。进一步，你学习了内置和书签活动。你还学习了如何使用`Try`和`Throw`活动处理运行时错误。最后，你学习了如何通过使用不同的类来托管工作流。

在下一章，你将学习文件处理。

## 29 C# 2010 中的文件处理

| 如果您需要立即解决以下问题： | 请参阅页码： |
|---|---|
| 使用驱动器 | 1390 |
| 使用目录 | 1393 |
| 使用文件 | 1403 |
| 在 .NET Framework 中压缩文件 | 1411 |

![](img/e073a4882197be4ab61103cbe0bcb394_1418_0.png)

## 深入探讨

文件是存储信息的一种介质，具有适当的格式和设计。在 C# 中，所有文件都应得到妥善处理，以防止其中存储的信息丢失。文件处理包括从文件中读取数据、向其中写入数据、复制和移动文件、重命名和删除文件。要处理文件，您可以在应用程序中使用`System.IO`命名空间。该命名空间提供了各种类，例如`FileStream`、`StreamReader`、`StreamWriter`、`BinaryReader`、`BinaryWriter`、`FileInfo`、`DriveInfo`、`Directory`和`DirectoryInfo`，用于处理文件。例如，您可以使用`FileStream`类以同步或异步方式读写文件数据。`StreamReader`和`StreamWriter`类允许您在流中读写文本数据，流是指文件中字符的流动。此外，除了读写文本数据外，您还可以使用`BinaryReader`和`BinaryWriter`类读写二进制数据。`FileInfo`类允许您创建、打开、移动、复制和删除文件。在处理文件时，您通常需要处理目录和驱动器，因为文件以分层格式存储在目录中。您可以使用`Directory`和`DirectoryInfo`类对目录执行操作，例如创建、移动、复制、重命名和删除目录。

在本章中，您将了解`System.IO`命名空间，包括其提供的类。您还将学习如何检索驱动器的信息。此外，您将学习如何在 .NET 中处理目录和文件。最后，您将学习文件压缩。在“立即解决方案”部分，您将学习如何在应用程序中实现这些概念。

现在，让我们开始学习`System.IO`命名空间。

## `System.IO` 命名空间

在 C# 2010 中，文件处理很大程度上基于`System.IO`命名空间，该命名空间包含一个支持字符串、字符和文件操作的类库。此命名空间中最常用的类是`FileStream`、`BinaryReader`、`BinaryWriter`、`StreamReader`和`StreamWriter`。这些类包含创建、复制、移动和删除文件的属性、方法和事件。`System.IO`命名空间中最重要的类在表 29.1 中给出：

### 表 29.1：显示 `System.IO` 命名空间的类

| Class | Description |
|---|---|
| `BinaryReader` | 有助于使用特定编码（如通用时间格式（UTF），包括 UTF-8 或 UTF-16）以二进制值形式读取原始数据类型。 |
| `BinaryWriter` | 有助于以二进制形式向流写入原始数据类型，并支持使用特定编码写入字符串。 |
| `Directory` | 暴露静态方法，有助于创建、移动和枚举目录和子目录。您不能继承此类。 |
| `DirectoryInfo` | 暴露实例方法以创建、移动和枚举目录和子目录。您不能继承此类。 |
| `DirectoryNotFoundException` | 通知用户文件或目录的一部分丢失。 |
| `DriveInfo` | 提供有关驱动器数据的相关信息。 |
| `File` | 提供用于创建、打开、移动、删除和复制文件的静态方法。此外，它有助于创建`FileStream`对象。 |
| `FileInfo` | 提供用于创建、打开、移动、删除和复制文件的实例方法。此外，它有助于创建`FileStream`对象。您不能继承此类。 |
| `FileFormatException` | 当输入数据的格式与文件的指定格式不匹配时引发异常，例如文件分配表（FAT）或新技术文件系统（NTFS）。 |

### 表 29.1：显示 `System.IO` 命名空间的类

| Class | Description |
|---|---|
| `FileNotFoundException` | 当您尝试访问硬盘上不存在的文件时引发异常。 |
| `FileStream` | 暴露围绕文件的流，支持同步和异步读写操作。 |
| `FileSystemInfo` | 为`FileInfo`和`DirectoryInfo`对象提供基类信息。 |
| `StreamReader` | 实现`TextReader`对象，有助于使用特定编码（如 UTF-8 和 UTF-16）从字节流读取字符。 |
| `StreamWriter` | 实现`TextWriter`对象，有助于使用特定编码（如 UTF-8 和 UTF-16）向流写入字符。 |

在探索了`System.IO`命名空间的重要类之后，让我们现在学习如何使用驱动器。

## 使用驱动器

在开始在 C# 中探索驱动器之前，让我们先检查在使用驱动器时经常使用的一些术语。以下是其中一些术语的列表：

- 驱动器号 — 表示用户为系统中的不同逻辑驱动器提供的名称。要为驱动器提供名称，您可以使用`Name`属性。此属性可帮助您为驱动器提供字母标识符，例如`C:\`、`D:\`和`E:\`。
- 驱动器状态 — 指定驱动器的状态，例如驱动器是否处于就绪状态。您可以使用`IsReady`属性来确定驱动器的状态。如果您查询未处于就绪状态的驱动器，则会发生异常。
- 驱动器类型 — 指连接到系统的驱动器的类型。您可以使用`DriveType`属性来确定驱动器的类型。驱动器可以是`CD-ROM`、`FIXED`、`UNKNOWN`、`NETWORK`、`NOROOTDIRECTORY`、随机存取存储器（`RAM`）或`REMOVABLE`类型。所有这些类型的取值均在`DriveType`枚举中指定。该枚举定义了驱动器类型的常量。`DriveType`枚举的不同成员如下：
  - `Unknown` — 表示未知驱动器类型
  - `NoRootDirectory` — 表示没有根目录的驱动器
  - `Removable` — 表示可移动性质的驱动器，例如软盘驱动器或通用串行总线（USB）闪存驱动器
  - `Fixed` — 表示固定磁盘驱动器，不能移除
  - `Network` — 表示通过网络访问的驱动器
  - `CD-ROM` — 表示光学性质的驱动器，例如 CD 或 DVD ROM
  - `RAM` — 表示随机存取存储器（RAM）磁盘驱动器
- 卷标 — 有助于设置或检索驱动器的名称。标签的长度基于操作系统的类型。例如，新技术文件系统（NTFS）允许卷标最长为 32 个字符。您可以使用`DriveInfo`类的`VolumeLabel`属性设置驱动器的卷标。请注意，如果您将`Null`作为驱动器的卷标输入，不会发生异常，因为`VolumeLabel`属性允许`Null`值。
- 文件系统格式 — 指定为驱动器提供的文件系统名称，例如 NTFS 或 FAT。NTFS 是 Windows NT 的最标准文件系统。它被所有后来的 Windows 版本支持，例如 Windows 2000、Windows XP、Windows Server 2003 和 Windows Vista。另一方面，FAT 文件系统几乎被所有现有操作系统支持，主要是个人使用的计算机。
- 驱动器上的可用空间 — 表示驱动器上可用的可用空间。您可以使用`AvailableFreeSpace`属性来计算当前用户可用的可用空间量，单位为字节。

C# 提供了`DriveInfo`类来检索驱动器中包含的信息。`DriveInfo`类对驱动器进行建模，并提供方法和属性来获取有关可用驱动器、它们包含的数据类型、其总容量以及可用空间的信息。`DriveInfo`类的继承层次结构如下：

```
System.Object

System.IO.DriveInfo
```

`DriveInfo`类涉及许多成员，例如属性、方法和事件。`DriveInfo`类的公共属性在表 29.2 中列出：

### 表 29.2：显示 `DriveInfo` 类的属性

| Property | Description |
|---|---|
| `AvailableFreeSpace` | 指定驱动器上可用的可用空间量 |
| `DriveFormat` | 检索文件系统的名称，无论是 NTFS 还是 FAT32 |
| `DriveType` | 检索指定驱动器的类型 |
| `IsReady` | 检索显示驱动器状态的值 |
| `Name` | 获取指定驱动器的名称 |
| `RootDirectory` | 检索驱动器的根目录 |
| `TotalFreeSpace` | 获取硬盘上可用的总可用空间量 |
| `TotalSize` | 检索硬盘的总容量 |
| `VolumeLabel` | 获取或设置驱动器的卷标 |

表 29.3 列出了`DriveInfo`类值得注意的公共方法：

### 表 29.3：显示 `DriveInfo` 类的方法

| Method | Description |
|---|---|
| `GetDrives()` | 获取系统上所有可用逻辑驱动器的名称 |
| `ToString()` | 以字符串形式返回驱动器的名称 |

让我们现在学习有关目录的知识。

## 使用目录

目录是作为文件存储库的实体。C# 提供了两个类`Directory`和`DirectoryInfo`来处理目录。`Directory`类是处理目录最重要的类之一。此类公开静态方法，有助于创建、移动和枚举目录和子目录。`Directory`类还用于设置目录的创建和访问日期和时间信息。需要注意的是，您不能继承`Directory`类。

`Directory`类的继承层次结构如下：

```
System.Object

System.IO.Directory
```

`Directory`类的所有方法都是静态的。表 29.4 列出了`Directory`类的方法：

### 表 29.4：显示 `Directory` 类的方法

| Methods | Description |
|---|---|
| `CreateDirectory()` | 在指定路径中创建所有目录 |

### 表 29.4：显示 `Directory` 类的方法

| Methods | Description |
|---|---|
| `Delete()` | 删除指定的目录 |
| `Exists()` | 确定给定的路径是否引用磁盘上存在的目录 |
| `GetAccessControl()` | 返回 Windows 访问控制列表 (ACL) |
| `GetCreationTime()` | 检索目录的创建日期和时间 |
| `GetCreationTimeUtc()` | 以协调世界时 (UTC) 格式检索目录的创建日期和时间 |
| `GetCurrentDirectory()` | 检索应用程序的当前工作目录 |
| `GetDirectories()` | 检索特定目录中的子目录名称 |
| `GetDirectoryRoot()` | 检索与指定路径相关的根、卷或卷和根的信息 |
| `GetFiles()` | 检索指定目录中的文件名称 |
| `GetFileSystemEntries()` | 检索指定目录中所有文件和子目录的名称 |
| `GetLastAccessTime()` | 检索指定文件或目录的最后访问日期和时间 |
| `GetLastAccessTimeUtc()` | 以 UTC 格式检索指定文件或目录的最后访问日期和时间 |
| `GetLastWriteTime()` | 检索指定文件或目录上次写入的日期和时间 |
| `GetLastWriteTimeUtc()` | 以 UTC 格式检索指定文件或目录上次写入的日期和时间 |
| `GetLogicalDrives()` | 检索计算机上的驱动器名称 |
| `GetParent()` | 检索指定路径的父目录，该路径包括绝对路径和相对路径 |
| `Move()` | 将文件或目录及其内容移动到新位置 |
| `SetAccessControl()` | 实现由`DirectorySecurity`对象描述的 ACL 条目，应用于指定目录 |
| `SetCreationTime()` | 设置指定文件或目录的创建日期和时间 |
| `SetCreationTimeUtc()` | 以 UTC 格式设置指定文件或目录的创建日期和时间 |
| `SetCurrentDirectory()` | 为应用程序指定当前工作目录 |
| `SetLastAccessTime()` | 设置指定文件或目录的最后访问日期和时间 |
| `SetLastAccessTimeUtc()` | 以 UTC 格式设置指定文件或目录的最后访问日期和时间 |
| `SetLastWriteTime()` | 指定目录的最后写入日期和时间 |
| `SetLastWriteTimeUtc()` | 以 UTC 格式指定目录的最后写入日期和时间 |

`DirectoryInfo`类公开了实例方法，有助于创建、移动和枚举目录。

`DirectoryInfo`类的继承层次结构如下：

```
System.Object

System.MarshalByRefObject

System.IO.FileSystemInfo

System.IO.DirectoryInfo
```
