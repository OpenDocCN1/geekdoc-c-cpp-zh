

- 当尝试访问文件或目录发生错误时，例如尝试打开没有必要权限的目录：`FileVisitResult visitFileFailed(T path, IOException ex)`

在每种情况下，你可以指定是否想要：

- 继续访问下一个文件：`FileVisitResult.CONTINUE`
- 继续遍历，但不访问此目录中的条目：`FileVisitResult.SKIP_SUBTREE`
- 继续遍历，但不访问此文件的兄弟条目：`FileVisitResult.SKIP_SIBLINGS`
- 终止遍历：`FileVisitResult.TERMINATE`

如果任何一个方法抛出异常，遍历也会终止，并且该异常会从`walkFileTree`方法中抛出。

> **注意：** `FileVisitor`接口是一个泛型类型，但你不太可能需要`FileVisitor<Path>`以外的其他类型。`walkFileTree`方法愿意接受`FileVisitor<? super Path>`，但`Path`并没有太多的超类型。

一个便捷类`SimpleFileVisitor`实现了`FileVisitor`接口。除了`visitFileFailed`之外的所有方法都不执行任何操作并继续。`visitFileFailed`方法会抛出导致失败的异常，从而终止访问。

例如，下面是如何打印出给定目录的所有子目录：

```java
Files.walkFileTree(Paths.get("/"), new SimpleFileVisitor<Path>()
{
    public FileVisitResult preVisitDirectory(Path path, BasicFileAttributes attrs)
        throws IOException
    {
        System.out.println(path);
        return FileVisitResult.CONTINUE;
    }

    public FileVisitResult postVisitDirectory(Path dir, IOException exc)
    {
        return FileVisitResult.CONTINUE;
    }

    public FileVisitResult visitFileFailed(Path path, IOException exc) throws IOException
    {
        return FileVisitResult.SKIP_SUBTREE;
    }
});
```

注意，我们需要重写`postVisitDirectory`和`visitFileFailed`。否则，一旦遇到不允许打开的目录或不允许访问的文件，访问就会失败。

还要注意，路径的属性作为参数传递给`preVisitDirectory`和`visitFile`方法。访问器已经不得不进行操作系统调用来获取属性，因为它需要区分文件和目录。这样，你就不需要再进行另一次调用。

`FileVisitor`接口的其他方法在你进入或离开目录时需要执行某些工作时非常有用。例如，当你删除一个目录树时，你需要先删除当前目录中的所有文件，然后再删除当前目录本身。以下是删除目录树的完整代码：

```java
// 删除从 root 开始的目录树
Files.walkFileTree(root, new SimpleFileVisitor<Path>()
{
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException
    {
        Files.delete(file);
        return FileVisitResult.CONTINUE;
    }

    public FileVisitResult postVisitDirectory(Path dir, IOException e) throws IOException
    {
        if (e != null) throw e;
        Files.delete(dir);
        return FileVisitResult.CONTINUE;
    }
});
```

**java.nio.file.Files 7**

- `static DirectoryStream<Path> newDirectoryStream(Path path)`
- `static DirectoryStream<Path> newDirectoryStream(Path path, String glob)`  
  获取给定目录中文件和目录的迭代器。第二个方法只接受与给定 glob 模式匹配的条目。
- `static Path walkFileTree(Path start, FileVisitor<? super Path> visitor)`  
  遍历给定路径的所有后代，将访问器应用于所有后代。

**java.nio.file.SimpleFileVisitor<T>**

- `FileVisitResult visitFile(T path, BasicFileAttributes attrs)`  
  在访问文件或目录时被调用，返回`CONTINUE`、`SKIP_SUBTREE`、`SKIP_SIBLINGS`或`TERMINATE`之一。默认实现不执行任何操作并继续。
- `FileVisitResult preVisitDirectory(T dir, BasicFileAttributes attrs)`
- `FileVisitResult postVisitDirectory(T dir, IOException exc)`  
  在访问目录之前和之后被调用。默认实现不执行任何操作并继续。
- `FileVisitResult visitFileFailed(T path, IOException exc)`  
  如果在尝试获取给定文件的信息时抛出异常，则调用此方法。默认实现会重新抛出该异常，从而导致访问以该异常终止。如果你想继续，请重写此方法。

## 2.5.8 ZIP 文件系统

`Paths`类在默认文件系统——用户本地磁盘上的文件中查找路径。你也可以有其他文件系统。其中比较有用的一种是 ZIP 文件系统。如果 zipname 是 ZIP 文件的名称，那么调用

```java
FileSystem fs = FileSystems.newFileSystem(Paths.get(zipname), null);
```

这将建立一个包含 ZIP 存档中所有文件的文件系统。如果你知道文件名，那么从该存档中复制文件是件容易的事：

```java
Files.copy(fs.getPath(sourceName), targetPath);
```

这里，`fs.getPath`等同于`Paths.get`，适用于任意文件系统。

要列出 ZIP 存档中的所有文件，可以遍历文件树：

```java
FileSystem fs = FileSystems.newFileSystem(Paths.get(zipname), null);
Files.walkFileTree(fs.getPath("/"), new SimpleFileVisitor<Path>()
{
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) throws IOException
    {
        System.out.println(file);
        return FileVisitResult.CONTINUE;
    }
});
```

这比第 77 页 2.3.3 节“ZIP 存档”中描述的 API 更好，该 API 需要一组新类来处理 ZIP 存档。

**java.nio.file.FileSystems 7**

- `static FileSystem newFileSystem(Path path, ClassLoader loader)`  
  遍历已安装的文件系统提供程序，并且如果 loader 不为 null，还会遍历给定类加载器可以加载的文件系统。返回第一个接受给定路径的文件系统提供程序创建的文件系统。默认情况下，有一个 ZIP 文件系统提供程序，它接受 name 以`.zip`或`.jar`结尾的文件。

**java.nio.file.FileSystem 7**

- `Path getPath(String first, String... more)`  
  通过连接给定的字符串来创建路径。

## 2.6 内存映射文件

大多数操作系统可以利用虚拟内存实现来将文件或文件区域“映射”到内存中。然后，该文件可以像内存数组一样被访问，这比传统的文件操作快得多。

### 2.6.1 内存映射文件性能

在本节末尾，你可以找到一个程序，它使用传统文件输入和内存映射文件计算文件的 CRC32 校验和。在一台机器上，我们计算 JDK 的`jre/lib`目录中 37MB 的`rt.jar`文件的校验和时，得到了表 2.5 所示的计时数据。

**表 2.5** 文件操作的计时数据

| 方法 | 时间 |
|---|---:|
| 普通输入流 | 110 秒 |
| 缓冲输入流 | 9.9 秒 |
| 随机访问文件 | 162 秒 |
| 内存映射文件 | 7.2 秒 |

如你所见，在这台特定的机器上，内存映射比使用缓冲的顺序输入稍快，并且比使用`RandomAccessFile`快得多。

当然，具体的数值会因机器不同而有很大差异，但很明显，与随机访问相比，性能提升可能是巨大的。另一方面，对于中等大小的文件的顺序读取，则没有理由使用内存映射。

`java.nio`包使内存映射变得非常简单。下面是你需要做的。

首先，获取文件的`channel`。channel 是磁盘文件的一种抽象，它让你能够访问操作系统功能，如内存映射、文件锁定以及文件之间的快速数据传输。

```java
FileChannel channel = FileChannel.open(path, options);
```

然后，通过调用`FileChannel`类的`map`方法从 channel 获取`ByteBuffer`。指定要映射的文件区域和映射模式。支持三种模式：

- `FileChannel.MapMode.READ_ONLY`：生成的缓冲区是只读的。任何对缓冲区的写入尝试都会导致`ReadOnlyBufferException`。
- `FileChannel.MapMode.READ_WRITE`：生成的缓冲区是可写的，并且更改将在某个时候写回文件。请注意，映射了同一文件的其他程序可能不会立即看到这些更改。多个程序同时映射文件的确切行为取决于操作系统。
- `FileChannel.MapMode.PRIVATE`：生成的缓冲区是可写的，但任何更改都仅对该缓冲区私有，不会传播到文件。

一旦你有了缓冲区，就可以使用`ByteBuffer`类及其超类`Buffer`的方法来读写数据。

缓冲区支持顺序和随机数据访问。缓冲区有一个位置，通过`get`和`put`操作来推进。例如，你可以按顺序遍历缓冲区中的所有字节：

```java
while (buffer.hasRemaining())
{
    byte b = buffer.get();
    . . .
}
```

或者，你可以使用随机访问：

```java
for (int i = 0; i < buffer.limit(); i++)
{
    byte b = buffer.get(i);
    . . .
}
```

你还可以使用这些方法读写字节数组：

