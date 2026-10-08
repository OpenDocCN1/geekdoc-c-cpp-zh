
260 第 13 章：访问目录和文件

**注意：** 这是一个盲目的软件设计示例。更好的解决方案是将代理（delegate）存储在*线程字典（thread dictionary）*中（参见第 14 章）。如果你需要对单例类进行类似的更改，请考虑这种方法，或者简单地为回调保留额外的参数。不要为了支持你的新接口而对现有代码进行侵入性的修改。

...文件管理器，它在单例模式下是线程安全的。如果你没有调用任何发送代理消息的方法，使用该单例也是安全的。这很遗憾，因为这意味着当你拷贝文件时，你可能需要创建一个新的 `NSFileManager` 实例，即使你已经有一个指向该单例实例的指针。

## 获取文件属性

```
NSFileManager *fm = [NSFileManager defaultManager];
Dictionary *attributes = [fm attributesOfAtPath:@"fileAttributes.m" error:NULL];
NSString *fileType = [attributes objectForKey:fileFileType];
NSNumber *creator = [attributes objectForKey:NSFileManagerHFSCreatorCode];
```
来自：fileAttributes.m

`NSFileManager` 类封装了大多数标准的 POSIX 文件系统操作函数。在 C 中，你通常使用 `stat()` 函数来查找文件信息。该函数接受一个结构体指针作为参数，并用文件信息填充它。

这种方法的局限性是显而易见的：你无法在不破坏使用该结构的所有现有代码的情况下添加新字段。`NSFileManager` 的版本要灵活得多。`-attributesOfItemAtPath:error` 方法返回一个 `NSDictionary`，向字典中添加额外的条目而不破坏二进制兼容性是非常轻而易举的。

从这个示例中你可以注意到，我们可以向字典发送 `-fileType` 消息来获取值。该方法是 `NSDictionary` 条目中对应 `NSFileType` 键的一部分，并返回字典条目键。还有几个类似的字典方法。

在 OS X 上，你比其他 POSIX 平台拥有更多的文件元数据位。HFS+ 为每个文件存储了创建者代码（creator code）和类型代码（type code）。这些现在不再被频繁使用，但在经典的 MacOS 上，它们被用来代替文件扩展名来确定打开文件的正确应用程序。

## 操作路径

```
NSString *home = @"-";
NSString *full =
[home stringByExpandingTildeInPath];
NSString *users =
[full stringByDeletingLastPathComponent];
NSString *file =
[users stringByAppendingPathComponent: @"users"];
NSString *fileWithExtension =
[file stringByAppendingPathExtension: @"db"];
```
*来自：path.m*

许多 UNIX 代码通过使用 `sscanf()` 和 `sprintf()` 函数来操作路径。当你将代码移植到 Windows 或 Symbian 时，会导致很多问题，因为它们的文件系统布局和路径分隔符是不同的。

OpenStep 从一开始就被设计为可以跨不同的操作系统家族。`NSString` 类提供了几个设计用于操作路径的方法。虽然这些方法操作的是字符串，但它们暴露了一个更抽象的接口。你可以添加或删除路径组件（路径中的单个项目，文件或目录）。你还可以修改文件扩展名。

在 OS X 上，像任何 UNIX 系统一样，有一个根目录，由单个斜杠表示。子目录由斜杠分隔，文件扩展名由点分隔。在 Windows 上，有多个根目录，路径组件由反斜杠分隔，但文件扩展名仍然由点分隔。

如果你在 `NSString` 上使用路径操作方法，无论文件系统的约定如何，你的代码都能正常工作。遗憾的是，`NSMutableString` 没有相应的操作集。你可以通过使用 `+pathWithComponents:` 和 `-pathComponents` 方法来避免创建大量临时对象带来的开销，这些方法分别从路径组件数组构造字符串，并创建一个路径组件数组。

在处理路径的代码中，没必要过度担心效率。文件系统上的几乎任何操作开销都比创建几个临时对象大得多。

264 第 13 章：访问目录和文件

## 判断文件或目录是否存在

```
NSFileManager *fm =
[NSFileManager defaultManager];
BOOL isDir;
if ([fm fileExistsAtPath:path isDirectory:&isDir]) {
    if (isDir)
        printf("Folder exists\n");
    else
        printf("File exists\n");
}else
    printf("File does not exist\n");
```
来自：fileExists.m

判断文件是否存在的最简单方法是尝试访问它，然后检查错误。这并不优雅，尽管这通常是安全的工作方法。如果你想在尝试操作之前向用户提供有关操作是否可以成功的反馈，你需要一个显式的测试。

`-fileExistsAtPath:isDirectory` 方法正是此用。该方法的名称有点误导。它测试指定路径上是否存在文件或目录，并告诉你它是否是一个目录。

第二个参数是一个指向 `BOOL` 的指针。如果你来自 C 或 C++，这看起来会非常熟悉，但对于来自 Java 等语言的人来说，这可能看起来有点奇怪。C（以及扩展的 Objective-C）只支持返回单个值，但此方法需要返回两个结果：对象是否存在以及它是否为目录。实现这一点几种方法。一种是定义一个枚举类型，包含 `nothing exists`、`file exists` 和 `directory exists` 元素。

**注意：** 不要使用这种机制来创建临时文件。如果这样做，在测试文件是否存在和创建文件之间存在潜在的竞态条件。请改用 C 库的 `mkstemp()` 函数。Foundation 框架有一个封装了这种功能，如果你想留在对象世界中可以使用。

这会让使用该方法的代码更简单，当你意识到可以传递 `NULL` 作为第二个参数时，答案变得明显。这是一个很小的节省，并不清楚这是否是一个明智的选择。

266 第 13 章：访问目录和文件

## 使用 Bundle（程序包）

```
NSBundle *mainBundle =
[NSBundle mainBundle];
NSLog("@@ links against %@", [mainBundle executablePath], [mainBundle allFrameworks]);
```
来自：bundles.m

在 Apple System 7 及更早版本中，文件系统支持两个分支：代码分支和数据分支。数据分支用于存储任意资源。随着 Mac OS 8.1，Apple 引入了 HFS+，它支持任意数量的分支，使得文件在能力上类似于目录。

OS X 仍然支持资源分支并在不支持的文件系统（如 UFS 和 FAT）上将其存储在隐藏文件中，但不建议使用。将包含分支的文件拷贝到其他文件系统有问题。如果你用 OS X 将文件拷贝到 FAT 磁盘，然后在 Windows 上拷贝，将不会拷贝隐藏文件，因此分支数据将会丢失。

与此同时，NeXT 采取了另一个方向。如果分支像目录，为什么不直接使用目录呢？NeXT 在标准的 UNIX 文件系统之上提供了分支的功能，只需使用目录来代替文件。

被预期视为文件的目录被称为 Bundle。对于原始的低级文件系统操作和其他操作系统，它们看起来像目录。例如，如果你将一个 OS X 应用程序 Bundle 拷贝到 USB 驱动器并在 Windows 上查看，它看起来就像任何其他目录。然而，当你在 Finder 中查看它时，它看起来像单个文件。

你在几乎任何 Objective-C 程序和应用程序中都会使用的两种 Bundle。它们都包含一些可执行代码（程序或共享库）和一组资源。

具体的布局取决于系统。GNUstep 使用旧的 NEXT 样式 Bundle 布局，而 OS X 使用的是稍微简单的一种。你完全可以产生同时具有 GNUstep 和 Cocoa 布局的 Bundle，允许同一个 .app 无需重新编译即可在系统间迁移。

你可以通过向 NSBundle 发送 `+mainBundle` 消息来获取应用程序的主 Bundle。这是一个用于封装 Bundle 的类。它跟踪所有动态加载的 Bundle。

Bundle 天生是可本地化的。资源存储在每个语言的子目录中，并按需加载。`-pathForResource:ofType` 方法将返回

