

```objc
stringByAppendingPathComponent:fName;
NSLog(@"fullpath to %@ is %@", fName, fullpath);
```

```objc
// Get the file name extension
extension = [fullpath pathExtension];
NSLog(@"extension for %@ is %@", fullpath, extension);
```

```objc
// Get user's home directory
homedir = NSHomeDirectory();
NSLog(@"Your directory is %@", homedir);
```

# 程序 16.5 输出

| 临时目录是 | |
| :--- | :--- |
| /var/folders/HT/HTyGLVsNHTuNb6NrMuo7QE+++TI/ | |
| 目录是 examples | |
| path.m 的全路径是 | /Users/stevekochan/progs/examples/path.m |
| /Users/stevekochan/progs/examples/path.m 的扩展名为 | m |
| 你的主目录是 | /Users/stevekochan/Users/stevekochan |

# 注意

在你的系统中，输出将与所示的不同。

函数 `NSTemporaryDirectory` 返回系统上可用于创建临时文件的目录路径。如果你在此目录中创建了临时文件，请务必在完成后将其删除。此外，确保你的文件名是唯一的，特别是当你的应用程序可能有多个实例同时运行时。（参见本章末尾的练习 5.）如果登录到你系统的多个用户正在运行同一个应用程序，这种情况很容易发生。请注意，临时文件仅仅是临时文件。如果你在使用后没有删除它们，系统会在某个时间自动为你删掉它们。然而，你不应该依赖这一点，而应该自己进行删除。

`lastPathComponent` 方法提取路径中的最后一个文件。当你有一个绝对路径并只想从中获取基本文件名时，这个方法非常有用。

`stringByAppendingPathComponent` 方法用于将文件名标记在路径末尾。如果作为接收者的指定路径不以斜杠结尾，该方法会在路径中插入一个斜杠，以与添加的文件隔离开。通过结合 `currentDirectoryPath` 方法与 `stringByAppendingComponent:` 方法，你可以创建一个指向当前目录下文件的完整路径。该技术在程序 16.5 中所示。

`pathExtension` 方法提供提供路径的文件扩展名。在示例中，`path.m` 文件的扩展名为 `m`，这是该方法返回的结果。如果文件没有扩展名，该方法仅返回一个空字符串。

`NSHomeDirectory` 函数返回当前用户的主目录。你可以通过使用 `NSHomeDirectoryForUser` 函数来获取任何特定用户的主目录，并将用户名作为函数的参数传递。

`pathComponents` 方法返回一个包含指定路径每个组件的数组。程序 16.5 顺序遍历返回数组的每个元素，并在输出的单独行中显示每个组件。

# 处理路径的常用方法

表 16.3 总结了许多用于处理路径的常用方法。在该表中：

# 表 16.3. 常用路径工具方法

| 方法 | 说明 |
| :--- | :--- |
| - (NSString *) pathWithComponents:components | 从组件中的元素构建有效路径 |
| - (NSArray *) pathComponents | 将路径拆解为它的组成组件 |
| - (NSString *) lastPathComponent | 提取路径中的最后一个组件 |
| - (NSString *) pathExtension | 从路径的最后一个组件中提取扩展名 |
| - (NSString *) stringByAppendingPathComponent:path | 在现有路径末尾添加路径 |
| - (NSString *) stringByAppendingPathExtension:ext | 在路径的最后一个组件上添加指定的扩展名 |
| - (NSString *) stringByDeletingLastPathComponent | 删除最后一个路径组件 |
| - (NSString *) stringByDeletingPathExtension | 删除最后一个路径组件的扩展名 |
| - (NSString *) stringByExpandingTildeInPath | 将路径中的任何波浪号 (~)扩展为用户的主目录或指定用户的主目录 |
| (NSString *) stringByResolvingSymlinksInPath | 尝试解析路径中的符号链接 |
| (NSString *) stringByStandardizingPath | 通过尝试解析...（父目录）和符号链接来标准化路径 |

表 16.4 展示了用于获取用户信息、其主目录以及存储临时文件的目录的函数。

## 16.4. 常用路径工具函数

| NSString *Username(void) | 返回当前用户的登录名 |
| :--- | :--- |
| NSString *NSFullUsername(void) | 返回当前用户的全名 |
| NSString *NSHomeDirectory(void) | 返回当前用户主目录的路径 |
| NSString *NSHomeDirectoryForUser(NSString *) | 返回用户的主目录 |
| NSString *NSTemporaryDirectory(void) | 返回可用于创建临时文件的目录路径 |

你可能还想查看 Foundation 函数 `NSSearchPathDirectoriesInDomains`，你可以用它定位系统或设备上的特殊目录，例如应用程序（Application）和文档（Documents）目录。例如，下面定义了一个名为 `saveFilePath` 的方法，它返回 Documents 目录中名为 `saveFile` 的文件的路径。如果你想将应用程序中的某些数据保存到文件中，可以使用像这样的方法。

```objc
- (NSString *) saveFilePath
{
    NSArray *dirList = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *docDir = [dirList objectAtIndex:0];

    return [docDir stringPathComponent:@"saveFile"];
}
```

# 注意

编写 iOS 应用程序时，`NSSearchPathInDomains` 函数的第二个参数应该是 `NSUserDomainMask`，你应该预期返回一个包含单个路径的数组。

# 复制文件和使用 NSProcessInfo 类

程序 16.6 演示了一个实现简单复制操作的命令行工具。该命令用法如下：

```
copy from-file to-file
```

与 `FileManager` 的 `copyPath:toPath:handler:` 不同，你的命令行工具允许 `to-file` 作为一个目录名称。在这种情况下，文件将被复制到 `to-file` 目录下并命名 `from-file`。与该方法不同，如果 `to-file` 已存在，你允许覆盖其内容。这更符合标准的 UNIX 复制命令 `cp`。

你可以通过使用 main 函数的 `argc` 和 `argv` 参数从命令行获取文件名。这两个参数分别由命令行上参数的数量（包括命令名）和一个指向 C 风格字符串数组的指针填充。

与其处理 C 字符串（当你处理 `argv` 时必须这样做），不如使用一个名为 `NSProcessInfo` 的 Foundation 类。`NSProcessInfo` 包含了允许你设置和检索有关正在运行的应用程序（即你的进程）的各种类型的方法。这些方法在表 16.6 中总结。

# 表 16.5. 常用目录

| 目录 | 用途 |
| :--- | :--- |
| Documents (NSDocumentDirectory) | 应用程序特定数据的目录。在 iOS 上写入的文件可以从 iTunes 共享和访问。存储在这里的文件会自动备份。 |
| Library/Caches (NSCacheDirectory) | 写入在启动之间间持久化的应用程序支持文件的目录。在此创建的文件不会持久化。 |
| tmp (NSTemporaryDirectory()) | 写入可以在终止后删除的临时文件的目录。不再需要时，你应该从此目录删除文件。 |
| Library/Preferences | 此目录包含应用程序特定的偏好文件。使用 `NSDefaultClasses` 创建、读取和修改偏好文件。 |

# 表 16.6. NSProcessInfo 方法

