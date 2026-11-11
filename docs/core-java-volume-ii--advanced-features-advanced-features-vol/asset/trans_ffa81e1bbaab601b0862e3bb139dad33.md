

**java.nio.file.Files 7**

- `static byte[] readAllBytes(Path path)`
- `static String readString(Path path, Charset charset)`
- `static List<String> readAllLines(Path path, Charset charset)`
  读取文件的内容。
- `static Path write(Path path, byte[] contents, OpenOption... options)`
- `static Path write(Path path, String contents, Charset charset, OpenOption... options)`
- `static Path write(Path path, Iterable<? extends CharSequence> contents, OpenOption... options)`
  将给定内容写入文件并返回该路径。
- `static InputStream newInputStream(Path path, OpenOption... options)`
- `static OutputStream newOutputStream(Path path, OpenOption... options)`
- `static BufferedReader newBufferedReader(Path path, Charset charset)`
- `static BufferedWriter newBufferedWriter(Path path, Charset charset, OpenOption... options)`
  打开文件以进行读取或写入。

### 2.4.3 创建文件和目录

要创建新目录，请调用

```java
Files.createDirectory(path);
```

路径中除最后一个组件外，其余部分必须已经存在。若要同时创建中间目录，请使用

```java
Files.createDirectories(path);
```

你可以使用以下方法创建空文件：

```java
Files.createFile(path);
```

如果文件已存在，该调用将抛出异常。存在性检查和创建是原子的。如果文件不存在，它会在其他人有机会执行相同操作之前被创建。

有一些便捷方法可在指定位置或系统特定位置创建临时文件或目录。

```java
Path newPath = Files.createTempFile(dir, prefix, suffix);
Path newPath = Files.createTempFile(prefix, suffix);
Path newPath = Files.createTempDirectory(dir, prefix);
Path newPath = Files.createTempDirectory(prefix);
```

此处，`dir` 是一个 `Path`，`prefix`/`suffix` 是可为 `null` 的字符串。例如，调用 `Files.createTempFile(null, ".txt")` 可能返回诸如 `/tmp/1234405522364837194.txt` 的路径。

创建文件或目录时，你可以指定属性，例如所有者或权限。然而，具体细节取决于文件系统，我们在此不作讨论。

**java.nio.file.Files 7**

- `static Path createFile(Path path, FileAttribute<?>... attrs)`
- `static Path createDirectory(Path path, FileAttribute<?>... attrs)`
- `static Path createDirectories(Path path, FileAttribute<?>... attrs)`
  创建文件或目录。`createDirectories` 方法也会创建所有中间目录。
- `static Path createTempFile(String prefix, String suffix, FileAttribute<?>... attrs)`
- `static Path createTempFile(Path parentDir, String prefix, String suffix, FileAttribute<?>... attrs)`
- `static Path createTempDirectory(String prefix, FileAttribute<?>... attrs)`
- `static Path createTempDirectory(Path parentDir, String prefix, FileAttribute<?>... attrs)`
  在适合存放临时文件的位置或给定父目录中创建临时文件或目录。返回所创建文件或目录的路径。

### 2.4.4 复制、移动和删除文件

要将文件从一个位置复制到另一个位置，只需调用

```java
Files.copy(fromPath, toPath);
```

要移动文件（即复制并删除原文件），请调用

```java
Files.move(fromPath, toPath);
```

如果目标已存在，复制或移动将失败。如果要覆盖现有目标，请使用 `REPLACE_EXISTING` 选项。如果要复制所有文件属性，请使用 `COPY_ATTRIBUTES` 选项。你可以同时提供两者，如下所示：

```java
Files.copy(fromPath, toPath, StandardCopyOption.REPLACE_EXISTING,
    StandardCopyOption.COPY_ATTRIBUTES);
```

你可以指定移动操作应是原子的。这样即可确保要么移动成功完成，要么源文件仍然存在。请使用 `ATOMIC_MOVE` 选项：

```java
Files.move(fromPath, toPath, StandardCopyOption.ATOMIC_MOVE);
```

你也可以将输入流复制到 Path，这仅意味着将输入流保存到磁盘。类似地，你可以将 Path 复制到输出流。请使用以下调用：

```java
Files.copy(inputStream, toPath);
Files.copy(fromPath, outputStream);
```

与其他复制调用一样，你可以根据需要提供复制选项。

最后，要删除文件，只需调用

```java
Files.delete(path);
```

如果文件不存在，此方法将抛出异常，因此你可能希望改用

```java
boolean deleted = Files.deleteIfExists(path);
```

删除方法也可以用于移除空目录。

有关可用于文件操作的选项的汇总，请参见表 2.3。

| `java.nio.file.Files` |
|---|
| • `static Path copy(Path from, Path to, CopyOption... options)`<br>• `static Path move(Path from, Path to, CopyOption... options)`<br>&nbsp;&nbsp;将 `from` 复制或移动到给定的目标位置，并返回 `to`。<br>• `static long copy(InputStream from, Path to, CopyOption... options)`<br>• `static long copy(Path from, OutputStream to, CopyOption... options)`<br>&nbsp;&nbsp;将输入流复制到文件，或将文件复制到输出流，返回复制的字节数。<br>• `static void delete(Path path)`<br>• `static boolean deleteIfExists(Path path)`<br>&nbsp;&nbsp;删除给定的文件或空目录。如果文件或目录不存在，第一个方法会抛出异常；第二个方法在这种情况下返回 `false`。 |

**表 2.3 文件操作的标准选项**

| 选项 | 描述 |
|---|---|
| `StandardOpenOption`；与 `newBufferedWriter`、`newInputStream`、`newOutputStream`、`write` 一起使用 | |
| `READ` | 打开以进行读取 |
| `WRITE` | 打开以进行写入 |
| `APPEND` | 如果为写入而打开，则追加到文件末尾 |
| `TRUNCATE_EXISTING` | 如果为写入而打开，则移除现有内容 |
| `CREATE_NEW` | 创建新文件，如果文件已存在则失败 |
| `CREATE` | 如果文件不存在，则原子地创建新文件 |
| `DELETE_ON_CLOSE` | 在文件关闭时“尽力”删除该文件 |
| `SPARSE` | 向文件系统提示此文件将是稀疏文件 |
| `DSYNC` 或 `SYNC` | 要求将每次对文件数据或数据及元数据的更新同步写入存储设备 |
| `StandardCopyOption`；与 `copy`、`move` 一起使用 | |
| `ATOMIC_MOVE` | 原子地移动文件 |
| `COPY_ATTRIBUTES` | 复制文件属性 |
| `REPLACE_EXISTING` | 如果目标存在则替换目标 |
| `LinkOption`；与上述所有方法以及 exists、`isDirectory`、`isRegularFile` 一起使用 | |
| `NOFOLLOW_LINKS` | 不跟随符号链接 |
| `FileVisitOption`；与 `find`、`walk`、`walkFileTree` 一起使用 | |
| `FOLLOW_LINKS` | 跟随符号链接 |

### 2.4.5 获取文件信息

以下静态方法返回一个布尔值，用于检查路径的某个属性：

- `exists`
- `isHidden`
- `isReadable`、`isWritable`、`isExecutable`
- `isRegularFile`、`isDirectory`、`isSymbolicLink`

size 方法返回文件中的字节数。

```java
long fileSize = Files.size(path);
```

getOwner 方法返回文件的所有者，作为 java.nio.file.attribute.UserPrincipal 的一个实例。

所有文件系统都会报告一组基本属性，这些属性由 BasicFileAttributes 接口封装，与上述信息部分重叠。基本文件属性如下：

- 文件的创建时间、最后访问时间和最后修改时间，作为类 java.nio.file.attribute.FileTime 的实例
- 该文件是常规文件、目录、符号链接，还是三者皆非
- 文件大小
- 文件键——某个类的对象，特定于文件系统，可能唯一标识文件，也可能不唯一标识

要获取这些属性，请调用

```java
BasicFileAttributes attributes = Files.readAttributes(path, BasicFileAttributes.class);
```

如果你知道用户的文件系统符合 POSIX，则可以改为获取 PosixFileAttributes 的实例：

```java
PosixFileAttributes attributes = Files.readAttributes(path, PosixFileAttributes.class);
```

然后你可以查明文件的组所有者以及所有者、组和其他用户的访问权限。我们不会深入讨论这些细节，因为其中大部分信息在操作系统之间并不具有可移植性。

**java.nio.file.Files 7**

- `static boolean exists(Path path)`
- `static boolean isHidden(Path path)`
- `static boolean isReadable(Path path)`
- `static boolean isWritable(Path path)`
- `static boolean isExecutable(Path path)`
- `static boolean isRegularFile(Path path)`
- `static boolean isDirectory(Path path)`
- `static boolean isSymbolicLink(Path path)`
  检查路径所指定文件的给定属性。
- `static long size(Path path)`
  以字节为单位获取文件大小。
- `static <A> A readAttributes(Path path, Class<A> type, LinkOption... options)`
  读取类型为 A 的文件属性。

