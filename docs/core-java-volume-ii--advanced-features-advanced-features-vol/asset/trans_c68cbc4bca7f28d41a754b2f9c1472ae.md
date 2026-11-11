

| `java.nio.file.attribute.BasicFileAttributes` | 7 |
|---|---|
| • `FileTime creationTime()` | |
| • `FileTime lastAccessTime()` | |
| • `FileTime lastModifiedTime()` | |
| • `boolean isRegularFile()` | |
| • `boolean isDirectory()` | |
| • `boolean isSymbolicLink()` | |
| • `long size()` | |
| • `Object fileKey()` | |
| 获取所请求的属性。 | |

### 2.4.6 遍历目录条目

静态的 `Files.list` 方法返回一个 `Stream<Path>`，用于读取目录中的条目。目录是惰性读取的，因此可以高效处理包含大量条目的目录。

由于读取目录涉及需要关闭的系统资源，因此应使用 try 块：

```
try (Stream<Path> entries = Files.list(pathToDirectory))
{
    ...
}
```

`list` 方法不会进入子目录。若要处理目录的所有后代，请改用 `Files.walk` 方法。

```
try (Stream<Path> entries = Files.walk(pathToRoot))
{
    // 包含所有后代，按深度优先顺序访问
}
```

以下是对解压后的 src.zip 目录树进行遍历的示例：

```
java
java/nio
java/nio/DirectoryBuffer.java
java/nio/ByteBufferAsShortBufferRL.java
java/nio/MappedByteBuffer.java
...
java/nio/ByteBufferAsDoubleBufferFB.java
java/nio/charset
java/nio/charset/CoderMalfunctionError.java
java/nio/charset/CharsetDecoder.java
java/nio/charset/UnsupportedCharsetException.java
java/nio/charset/spi
java/nio/charset/spi/CharsetProvider.java
java/nio/charset/StandardCharsets.java
java/nio/charset/Charset.java
. . .
java/nio/charset/CoderResult.java
java/nio/HeapFloatBuffer.java
. . . .
```

如你所见，每当遍历遇到一个目录时，会先进入该目录，然后再继续处理其兄弟节点。

你可以通过调用 `Files.walk(pathToRoot, depth)` 来限制要访问的树的深度。两个 walk 方法都有一个 `FileVisitOption` 类型的可变参数……但你只能提供一个选项：`FOLLOW_LINKS`，用于跟随符号链接。

> **注意：** 如果你要过滤 walk 返回的路径，并且过滤条件涉及与目录一起存储的文件属性（例如大小、创建时间或类型（文件、目录、符号链接）），那么应使用 `find` 方法而不是 `walk`。调用该方法时，需要传入一个谓词函数，该函数接受一个路径和一个 `BasicFileAttributes` 对象。这样做的好处只是效率更高。由于无论如何都要读取目录，因此这些属性已经可用。

以下代码片段使用 `Files.walk` 方法将一个目录复制到另一个目录：

```
Files.walk(source).forEach(p ->
{
    try
    {
        Path q = target.resolve(source.relative(p));
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

遗憾的是，你不能轻松地使用 `Files.walk` 方法删除目录树，因为你需要先删除子项，然后再删除父项。下一节将向你展示如何解决该问题。

### 2.4.7 使用目录流

如前一节所述，`Files.walk` 方法会生成一个 `Stream<Path>`，用于遍历目录的后代。有时，你需要对遍历过程进行更细粒度的控制。在这种情况下，请改用 `Files.newDirectoryStream` 对象。它会生成一个 `DirectoryStream`。请注意，这不是 `java.util.stream.Stream` 的子接口，而是专门用于目录遍历的接口。它是 `Iterable` 的子接口，因此你可以在增强的 for 循环中使用目录流。用法模式如下：

```
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir))
{
    for (Path entry : entries)
        Process entries
}
```

try-with-resources 块确保目录流被正确关闭。

目录条目的访问顺序没有特定规定。

你可以使用 glob 模式过滤文件：

```
try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir, "*.java"))
```

表 2.4 显示了所有 glob 模式。

**表 2.4 Glob 模式**

| 模式 | 描述 | 示例 |
|---|---|---|
| `*` | 匹配路径组件中的零个或多个字符。 | `*.java` 匹配当前目录中的所有 Java 文件。 |
| `**` | 匹配零个或多个字符，可跨越目录边界。 | `**.java` 匹配任何子目录中的所有 Java 文件。 |
| `?` | 匹配一个字符。 | `????.java` 匹配所有四个字符（不包括扩展名）的 Java 文件。 |
| `[...]` | 匹配一组字符。可以使用连字符（`[0-9]`）和取反（`[!0-9]`）。 | `Test[0-9].java` 匹配 Test0.java，其中 x 是一个十六进制数字。 |
| `{...}` | 匹配以逗号分隔的替代项。 | `*.{java,class}` 匹配所有 Java 和 class 文件。 |
| `\` | 转义上述任何字符以及 `\` 本身。 | `**\*` 匹配所有名称中包含 `*` 的文件。 |

> **警告：** 如果你在 Windows 上使用 glob 语法，则必须对反斜杠进行*两次*转义：一次是针对 glob 语法，一次是针对 Java 字符串语法：`Files.newDirectoryStream(dir, "C:\\\*")`。

如果要访问目录的所有后代，请调用 `walkFileTree` 方法，并提供一个 `FileVisitor` 类型的对象。该对象会在以下情况得到通知：

- 遇到文件时：`FileVisitResult visitFile(T path, BasicFileAttributes attrs)`
- 处理目录之前：`FileVisitResult preVisitDirectory(T dir, IOException ex)`
- 处理目录之后：`FileVisitResult postVisitDirectory(T dir, IOException ex)`
- 尝试访问文件或目录时发生错误（例如尝试打开没有必要权限的目录）：`FileVisitResult visitFileFailed(T path, IOException ex)`

在每种情况下，你都可以指定是否：

- 继续访问下一个文件：`FileVisitResult.CONTINUE`
- 继续遍历，但不访问此目录中的条目：`FileVisitResult.SKIP_SUBTREE`
- 继续遍历，但不访问此文件的兄弟节点：`FileVisitResult.SKIP_SIBLINGS`
- 终止遍历：`FileVisitResult.TERMINATE`

如果任何方法抛出异常，遍历也会终止，并且该异常会从 `walkFileTree` 方法中抛出。

> **注意：** `FileVisitor` 接口是一个泛型类型，但你不太可能需要除 `FileVisitor<Path>` 之外的任何类型。`walkFileTree` 方法愿意接受 `FileVisitor<? super Path>`，但 `Path` 并没有很多超类型。

便捷类 `SimpleFileVisitor` 实现了 `FileVisitor` 接口。除 `visitFileFailed` 之外的所有方法都不执行任何操作并继续。`visitFileFailed` 方法会抛出导致失败的异常，从而终止访问。

例如，以下代码展示如何打印出给定目录的所有子目录：

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

    public FileVisitResult visitFileFailed(Path path, IOException exc)
        throws IOException
    {
        return FileVisitResult.SKIP_SUBTREE;
    }
});
```

请注意，我们需要重写 `postVisitDirectory` 和 `visitFileFailed`。否则，一旦遇到不允许打开的目录或不允许访问的文件，访问就会失败。

还要注意，路径的属性会作为参数传递给 `preVisitDirectory` 和 `visitFile` 方法。访问器已经进行了 OS 调用来获取属性，因为它需要区分文件和目录。这样，你就不需要再进行一次调用。

`FileVisitor` 接口的其他方法在进入或离开目录时需要执行某些工作时非常有用。例如，当你删除目录树时，需要在删除目录中的所有文件后，再删除当前目录。这是删除目录树的完整代码：

```java
// Delete the directory tree starting at root
Files.walkFileTree(root, new SimpleFileVisitor<Path>()
{
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
        throws IOException
    {
        Files.delete(file);
        return FileVisitResult.CONTINUE;
    }
});
```

