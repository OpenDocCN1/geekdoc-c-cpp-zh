

# 第 16 章 文件的操作

用户
stevekochan
-stevekochan/progs/../ch16/.path.m => /Users/stevekochan/ch16/path.m

> 注意
> 在你的系统中，输出将与所示内容不同。

函数 `NSTemporaryDirectory` 返回系统中一个目录的路径，你可以用它创建临时文件。如果你在该目录中创建了临时文件，请务必在完成后将其删除。此外，确保你的文件名是唯一的，特别是当可能同时运行多个应用程序实例时。（参见本章末尾的练习 5）。如果有多个用户登录到你的系统并运行同一个应用程序，这种情况很容易发生。请注意，临时文件只是临时的。如果你不删除它们，系统会在某个时候将它们删除。然而，你不应该依赖这一点，而应该自行删除。

`lastPathComponent` 方法提取路径中的最后一个文件。当你有一个绝对路径并只想从中获取基本文件名时，这个方法非常有用。

`stringByAppendingPathComponent` 用于在路径的末尾添加文件名。如果作为接收者的指定路径不以斜杠结尾，该方法会在路径中插入一个斜杠，以将其与附加的文件名隔开。通过将 `directory` 方法与 `stringByAppendingPathComponent:` 方法结合，你可以创建当前目录下文件的完整路径。该技术在程序 16.5 中显示。

`pathExtension` 方法提供提供路径的文件扩展名。在示例中，file.m 的扩展名是 m，由该方法返回的。如果文件没有扩展名，该方法将简单地返回一个空字符串。

`NSHomeDirectory` 函数返回当前用户的家目录。你可以使用 `NSHomeDirectoryForUser` 实例并将用户名作为函数的参数，来获取任何特定用户的家目录。

`pathComponents` 方法返回一个包含指定路径所有组件的数组。程序 16.5 遍历返回数组的每个元素，并在输出的每一行中显示每个路径组件。

最后，正如我们之前讨论过的，路径有时包含波浪号（~）字符。`FileManager` 方法接受 `~` 作为用户家目录的缩写，或接受 `~user` 作为指定用户家目录的缩写。如果你的路径可能包含波浪号字符，你可以使用 `stringByStandardizingPath` 方法解析它们。该方法返回一个消除了这些特殊字符（或已标准化）的路径。你也可以使用 `stringByExpandingTildeInPath` 方法在路径中出现波浪号时将其扩展。

## 操作路径的常用方法

表 16.3 总结了许多用于操作路径的常用方法。表中，`components` 是一个包含路径中每个组件的字符串对象的 `NSArray`；`path` 是一个指定文件路径的字符串对象；`ext` 是一个指示扩展名（例如“@mp4”）的字符串对象。

| 表 16.3 常用路径实用方法 |
| 方法 |  |
| --- | --- |
| + (NSObject *) pathWithComponents: components | 从 components 中的元素构建有效路径 |
| - (NSArray *) pathComponents | 将路径拆解为它的各个组成部分 |
| - (NSString *) lastPathComponent | 提取路径中的最后一个组件 |
| - (NSObject *) pathExtension | 从路径的最后一个组件中提取扩展名 |
| - (NSString *) stringByAppendingPathComponent: path | 在现有路径末尾添加路径 |
| - (NSString *) stringByAppendingPathExtension: ext | 在路径的最后一个组件后添加指定的扩展名 |
| - (NSString *) stringByDeletingLastPathComponent | 删除最后一个路径组件 |
| - (NSString *) stringByDeletingPathExtension | 删除最后一个路径组件的扩展名 |
| - (NSString *) stringByExpandingTildeInPath | 将路径中的波浪号扩展为用户家目录 (~) 或指定用户目录 (~user) |
| - (NSString *) stringByResolvingSymlinksInPath | 尝试解析路径中的符号链接 |
| - (NSString *) | 通过尝试解析 ~, . .. (父目录), . (当前目录) 和符号链接来标准化路径 |

表 16.4 给出了可用于获取用户信息、其家目录以及存储临时文件的目录信息的函数。

| 表 16.4 常用路径实用函数 |
| 函数 | 描述 |
| --- | --- |
| NSString *NSUsername (void) | 返回当前用户的登录名 |
| NSString *NSFullUsername (void) | 返回当前用户的全名 |
| NSString *NSHomeDirectory (void) | 返回当前用户家目录的路径 |
| NSString *NSHomeDirectoryFor(NSString *user) | 返回用户的家目录 |
| NSString *NSTemporaryDirectory(void) | 返回可创建临时文件的目录路径 |

你可能还想看看 Foundation 函数 `NSSearchForDirectoriesInDomains`，你可以用它定位系统或设备上的特殊目录，例如 `Application` 和 `Documents` 目录。例如，下面的代码定义了一个名为 `saveFilePath` 的方法，返回 `CachesDirectory` 中文件 `saveFile` 的路径。如果你想将应用程序中的某些数据保存到文件中，可以使用这样的方法。

```objc
(NSString *) saveFilePath{
Array *dirList = NSSearchForDirectoriesInDomains
(CachesDirectory, NSUserDomainMask, YES);
NSString *docDir = [dirList objectAtIndex: 0];

[docDir stringByAppendingPathComponent:@"saveFile"];
}
```

## 操作路径：NSPathUtilities.h

> 注意
> Caches 目录可以用于存储在程序多次运行之间持久的数据。每个 iOS 应用程序都有自己的 Caches 目录可以写入数据。`NSSearchPathInDomains` 函数的第一个参数指定要查找的目录。你应用程序中使用的另一个目录是 Documents。目录也可用于存储数据以及在 iOS 应用程序之间共享文件。常用 iOS 目录见表 16.5。

## 表 16.5 常用 iOS 目录

| 目录 | 目的 |
| --- | --- |
| Documents (NSDocumentDirectory) | 用于写入应用程序数据文件 |
| Library/Caches (NSCacheDirectory) | 用于写入在启动间持久的应用程序支持文件。在此创建的文件不会被 iTunes 备份 |
| tmp (使用 NSTemporaryDirectory()) | 用于写入运行后可以删除的临时文件。需要时应从该目录删除文件 |
| Library/Preferences | 此目录包含应用程序偏设置文件。使用 NSUserDefaults 创建、读取和修改偏设置文件 |

函数的第二个参数可以是多个值之一，指定要列出的目录，例如示例所示的用户目录、系统目录或所有目录。最后一个参数指定是否扩展路径中的 ~ 字符。
`NSSearchPathDirectoriesInDomains` 返回一个路径数组。如果你只是查找用户目录，数组将包含单个元素；根据第二个参数的值，它可能包含多个元素。

> 注意
> 编写 iOS 应用程序时，`NSSearchDirectoriesInDomains` 的第二个参数应该是 `NSUserDomainMask`，你应该预期得到一个包含单个路径的数组。

## 复制文件与使用 NSInfoPlistClass

程序 16.6 阐述了一个实现简单文件复制操作的命令行工具。
该命令的使用方式如下：
```from-file:to-file
```

与 `FileManager` 的 `copyPath:toPath:handler:` 方法不同，你的命令行工具允许 to-file 为一个目录。在这种情况下，文件将被复制到 to-目录中并命名为 from-file。同样与该方法不同，如果 to-file 存在，你允许覆盖其内容。这更符合标准的 UNIX 复制命令 `cp`。

