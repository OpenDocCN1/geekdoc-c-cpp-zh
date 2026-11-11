
最后，要删除文件，只需调用

```java
Files.delete(path);
```

如果文件不存在，此方法会抛出异常，因此你可能想改用

```java
boolean deleted = Files.deleteIfExists(path);
```

删除方法也可用于删除空目录。

有关文件操作可用选项的汇总，请参见表 2.3。

**表 2.3 文件操作的标准选项**

| 选项 | 描述 |
|---|---|
| **StandardOpenOption；与 newBufferedWriter、newInputStream、newOutputStream、write 一起使用** | |
| READ | 以读取方式打开 |
| WRITE | 以写入方式打开 |
| APPEND | 如果以写入方式打开，则追加到文件末尾 |
| TRUNCATE_EXISTING | 如果以写入方式打开，则删除现有内容 |
| CREATE_NEW | 创建新文件，如果文件已存在则失败 |
| CREATE | 如果文件不存在，则自动创建新文件 |
| DELETE_ON_CLOSE | 在关闭文件时“尽最大努力”删除该文件 |
| SPARSE | 向文件系统提示该文件将是稀疏文件 |
| DSYNC\|SYNC | 要求每次对文件数据 \| 数据和元数据的更新都同步写入存储设备 |
| **StandardCopyOption；与 copy、move 一起使用** | |
| ATOMIC_MOVE | 原子地移动文件 |
| COPY_ATTRIBUTES | 复制文件属性 |
| REPLACE_EXISTING | 如果目标存在则替换目标 |
| **LinkOption；与上述所有方法以及 exists、isDirectory、isRegularFile 一起使用** | |
| NOFOLLOW_LINKS | 不跟随符号链接 |
| **FileVisitOption；与 find、walk、walkFileTree 一起使用** | |
| FOLLOW_LINKS | 跟随符号链接 |

- `java.nio.file.Files`^7
  - `static Path copy(Path from, Path to, CopyOption... options)`
  - `static Path move(Path from, Path to, CopyOption... options)`  
    从给定源位置复制或移动到给定目标位置，并返回目标。
  - `static long copy(InputStream from, Path to, CopyOption... options)`
  - `static long copy(Path from, OutputStream to, CopyOption... options)`  
    从输入流复制到文件，或从文件复制到输出流，并返回复制的字节数。
  - `static void delete(Path path)`
  - `static boolean deleteIfExists(Path path)`  
    删除给定文件或空目录。如果文件或目录不存在，第一个方法会抛出异常。第二个方法在这种情况下返回 false。

### 2.5.5 获取文件信息

以下静态方法返回 `boolean` 值，用于检查路径的某个属性：

- `exists`
- `isHidden`
- `isReadable`、`isWritable`、`isExecutable`
- `isRegularFile`、`isDirectory`、`isSymbolicLink`

`size` 方法返回文件中的字节数。

```java
long fileSize = Files.size(path);
```

`getOwner` 方法返回文件所有者，作为 `java.nio.file.attribute.UserPrincipal` 的实例。

所有文件系统都报告一组基本属性，由 `BasicFileAttributes` 接口封装，这些信息与上述信息部分重叠。基本文件属性包括：

- 文件的创建时间、最后访问时间和最后修改时间，作为 `java.nio.file.attribute.FileTime` 类的实例
- 文件是常规文件、目录、符号链接，还是都不是
- 文件大小
- *文件键*——某个类的对象，特定于文件系统，可能唯一标识一个文件，也可能不唯一

要获取这些属性，请调用

```java
BasicFileAttributes attributes = Files.readAttributes(path, BasicFileAttributes.class);
```

如果你知道用户的文件系统符合 POSIX，则可以改为获取 PosixFileAttributes 的实例：

```java
PosixFileAttributes attributes = Files.readAttributes(path, PosixFileAttributes.class);
```

然后你可以查明文件的组所有者以及所有者、组和其他用户的访问权限。我们不会详述细节，因为其中大量信息无法跨操作系统移植。

| java.nio.file.Files 7 |
|---|
| • `static boolean exists(Path path)` |
| • `static boolean isHidden(Path path)` |
| • `static boolean isReadable(Path path)` |
| • `static boolean isWritable(Path path)` |
| • `static boolean isExecutable(Path path)` |
| • `static boolean isRegularFile(Path path)` |
| • `static boolean isDirectory(Path path)` |
| • `static boolean isSymbolicLink(Path path)`<br>检查路径所指定文件的给定属性。 |
| • `static long size(Path path)`<br>获取文件大小（以字节为单位）。 |
| • `A readAttributes(Path path, Class<A> type, LinkOption... options)`<br>读取类型为 A 的文件属性。 |

| java.nio.file.attribute.BasicFileAttributes 7 |
|---|
| • `FileTime creationTime()` |
| • `FileTime lastAccessTime()` |
| • `FileTime lastModifiedTime()` |
| • `boolean isRegularFile()` |
| • `boolean isDirectory()` |
| • `boolean isSymbolicLink()` |
| • `long size()` |
| • `Object fileKey()`<br>获取请求的属性。 |

`walk` 方法接受一个 `FileVisitOption...`，但只能提供一个选项：`FOLLOW_LINKS`，用于跟随符号链接。

> **注意：** 如果你筛选 `walk` 返回的路径，并且筛选条件涉及与目录一起存储的文件属性，例如大小、创建时间或类型（文件、目录、符号链接），则应使用 `find` 方法而不是 `walk`。调用该方法时，传入一个接受路径和 `BasicFileAttributes` 对象的谓词函数。唯一的优势是效率。由于无论如何都要读取目录，这些属性很容易获得。

以下代码片段使用 `Files.walk` 方法将一个目录复制到另一个目录：

```java
Files.walk(source).forEach(p ->
{
    try
    {
        Path q = target.resolve(source.relativize(p));
        if (Files.isDirectory(p))
            Files.createDirectory(q);
        else
            Files.copy(p, q);
    }
    catch (IOException ex)
    {
        throw new UncheckedIOException(ex);
    }
});
```

遗憾的是，你无法轻松地使用 `Files.walk` 方法来删除目录树，因为需要先删除子项，再删除父项。下一节将展示如何解决该问题。

### 2.5.7 使用目录流

正如你在上一节中所看到的，`Files.walk` 方法会生成一个 `Stream<Path>`，用于遍历目录的后代。有时，你需要对遍历过程进行更细粒度的控制。在这种情况下，请改用 `Files.newDirectoryStream` 对象。它会生成一个 `DirectoryStream`。请注意，这不是 `java.util.stream.Stream` 的子接口，而是专门用于目录遍历的接口。它是 `Iterable` 的子接口，因此可以在增强 for 循环中使用目录流。以下是使用模式：

```java
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir))
{
    for (Path entry : entries)
        Process entries
}
```

try-with-resources 块确保目录流被正确关闭。

目录条目的访问顺序不固定。

可以使用 glob 模式筛选文件：

```java
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir, "*.java"))
```

**表 2.4 Glob 模式**

| 模式 | 描述 | 示例 |
|---|---|---|
| `*` | 匹配路径组件中的零个或多个字符 | `*.java` 匹配当前目录中的所有 Java 文件 |
| `**` | 匹配零个或多个字符，可跨越目录边界 | `**.java` 匹配任意子目录中的所有 Java 文件 |
| `?` | 匹配一个字符 | `????.java` 匹配所有四字符的 Java 文件（不计扩展名） |
| `[...]` | 匹配一组字符。可以使用连字符 `[0-9]` 和否定 `[!0-9]`。 | `Test[0-9A-F].java` 匹配 `Testx.java`，其中 x 是一个十六进制数字 |
| `{...}` | 匹配由逗号分隔的备选项 | `*.{java,class}` 匹配所有 Java 和 class 文件 |
| `\\` | 转义上述任意字符以及 `\\` | `*\\*` 匹配名称中包含 `*` 的所有文件 |

> **警告：** 如果在 Windows 上使用 glob 语法，必须对反斜杠转义两次：一次用于 glob 语法，一次用于 Java 字符串语法：
> `Files.newDirectoryStream(dir, "C:\\\\")`。

如果要访问目录的所有后代，请改为调用 `walkFileTree` 方法，并提供一个 `FileVisitor` 类型的对象。该对象会在以下情况下收到通知

- 当遇到文件时：`FileVisitResult visitFile(T path, BasicFileAttributes attrs)`
- 在处理目录之前：`FileVisitResult preVisitDirectory(T dir, BasicFileAttributes attrs)`
- 在处理目录之后：`FileVisitResult postVisitDirectory(T dir, IOException ex)`

