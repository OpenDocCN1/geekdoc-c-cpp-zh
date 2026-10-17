
```bash
$ see what files we have
total 96
-rwxr-xr-x 1 steovec staff 19956 Jul 24 14:33
copy
-rw-r--r-- 1 steovec staff 1484 Jul 24 14:32
copy.m
-rw-r--r-- 1 steovec staff 1403 Jul 24 14:00
file.m
drwxr-xr-x 2 stevekoc staff 68 Jul 24 14:40
newdir
-rw-r----1 stevekoc staff 1567 Jul 24 14:12
path1.m
-rw-r----1 stevekoc staff 84 Jul 24 13:22
testfile
$ copy try with no args
Usage: copy src dest
$ copy foo copy2
Can't read foo
$ copy.m backup.m
Copy of copy.m to backup.m succeeded!
$ diff copy.m backup.m compare the files
$ copy copy.m newdir try copy into directory
Copy of copy.m to newdir/copy.m succeeded!
$ ls -l newdir
total 8
-rw-r-r- 1 stevekoc staff 1484 Jul 24 14:44
copy.m
$
```

注意

所显示的输出将根据你运行此程序时在当前目录中存储的文件而有所不同。

`ProcessInfo` 的 `arguments` 方法返回一个字符串对象数组。数组的第一个元素是进程名称，其余元素包含在命令行上输入的参数。

你首先检查命令行上是否输入了两个参数。这是通过测试 `arguments` 方法返回的数组 `args` 的大小来实现的。如果测试成功，程序将从数组中提取源文件名和目标文件名。接下来，你检查源文件是否可以读取。这是通过使用 `isReadableAtPath:` 完成的。

# 基本操作：NSFileHandle

`NSFileHandle` 提供的方法允许你更紧密地处理文件。在本章开始，我们列出了使用这些方法可以做的一些事情。通常处理文件时遵循以下三个步骤：

1. 打开文件并获取引用该文件的 `NSFileHandle` 对象。
2. 对打开的文件进行 I/O 操作。
3. 关闭文件。

## 表 16.7 常用 NSFileHandle 方法

| 方法 | 说明 |
| :--- | :--- |
| `+(NSFileHandle *) fileHandleForReadingAtPath: path` | 打开文件读取 |
| `+(NSFileHandle *) fileHandleForWritingAtPath: path` | 打开文件写入 |
| `+(NSFileHandle *) fileHandleForUpdatingAtPath: path` | 打开文件更新（读写） |
| `-(NSData *) availableData` | 返回设备或通道的可用数据 |
| `-(NSData *) readToEndFile` | 读取到文件末尾的 `UINT_MAX` 字节 |
| `-(NSData *) readDataOfLength: bytes` | 从文件中读取指定数量的字节 |
| `-(void) writeData: data` | 将数据写入文件 |
| `-(unsigned long long) offsetInFile` | 返回当前文件偏移 |
| `-(void) seekToFileOffset: offset` | 设置当前文件偏移 |
| `-(unsigned long long) seekToEndFile` | 将当前文件偏移置于文件末尾 |
| `-(void) truncateToFileOffset: offset` | 将文件大小设置为 `offset` 字节（如果需要） |
| `-(void) closeFile` | 关闭文件 |

你应该注意，`NSFileHandle` 类并不提供创建文件的功能。这必须通过 `NSFileManager` 方法完成，正如我们已经描述的那样。因此，`fileHandleForWritingAtPath:` 和 `fileHandleForUpdatingAtPath:` 都假设文件存在，如果不存在则返回 `nil`。在在这两种情况下，文件偏移量被设置为文件的开头，因此写入（或更新模式）从文件开始开始。未展示的还有在后台（即异步）读取和写入数据的方法。

在 UNIX 中，你应该注意打开文件进行写入并不会截断文件。如果这是你的意图，你必须手动完成。

[程序 16.7](https://objc.apple.com/library/documentation/archive/Objective-C-Programming-Guide/beginning/reading-a-file.html#program-1677) 打开了在本章开头创建的原始 `testfile` 文件，读取其内容并将其复制到名为 `testout` 的文件中。

# 程序 16.7

```
// 一基础文件句柄操作
// 假设当前工作目录下存在一个名为 "testfile" 的文件

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSFileHandle *inFile, *outFile;
        NSData *buffer;

        // 打开 testfile 进行读取
        inFile = [NSFileHandle fileHandleForReadingAtPath:@"testfile"];

        if (inFile == nil) {
            NSLog (@@"Open of testfile for reading failed");
            return 1;
        }

        // 如果必要，先创建输出文件
```

```
 [NSFileManager defaultManager
createFileAtPath: @"testout"
contents: nil attributes: nil];
```

```
// 现在打开 outfile 进行写入
outFile = [NSFileHandle
fileHandleForWritingAtPath: @"testout"];
```

```
if (outFile == nil) {
NSLog (@"Open of testout for writing
failed");
return 2;
}
```

```
// 截断输出文件，因为它可能包含数据
```

```
[outFile truncateFileAtOffset: 0];
```

```
// 从 inFile 读取数据并写入 toFile
```

```
buffer = [inFile readDataToEndFile];
[outFile writeData: buffer];
```

```
// 关闭两个文件
[inFile closeFile];
[outFile closeFile];
```

```
// 验证文件内容
```

```
NSLog(@"%@", [NSString
```

```
stringWithContentsFile: @"testout" encoding:
NSUTF8StringEncoding error:
NULL]);
}
  return 0;
}
```

# 程序 16.7 输出

这是一个包含一些数据的测试文件。

这是另一行数据。

这是第三行。

`readDataToEndFile:` 方法每次读取最多 `UINT_MAX` 字节的数据，该值定义在 `<limits.h>` 中并等于 `0xFFFFFFFF`：这对于你将编写的任何应用程序都足够大。你也可以将该操作拆分以执行较小的读写。你甚至可以设置一个循环，使用 `readDataLength:` 方法每次在文件之间传输字节缓冲区。例如，你的缓冲区大小可能是 8192 `8kb` 或 131072 `128kb` 字节。通常使用 2 的幂，是因为底层操作系统通常以这种大小的块来执行 I/O 操作。你可能想在你的系统上尝试不同的值，看看效果最好。

如果读取到达文件末而没有读取到数据，它将返回一个空的 `NSData` 对象（即一个没有任何字节的缓冲区）。你可以对缓冲区应用 `length` 方法并测试是否等于零，以检查文件中是否有剩余数据待读取。

如果你打开文件进行更新，文件偏移量将设置为文件开头。你可以通过在文件中寻址（seek）来更改偏移量，然后在文件上执行读取或写入操作。因此，要将在句柄为 `databaseHandle` 的文件中寻道第 10 个字节，你可以写下以下消息表达式：

```
[databaseHandle seekToFileOffset: 10];
```

相对文件定位是通过获取当前文件偏移量然后对其进行加或减来实现的。因此，要跳到文件中下一个 128 字节，请写道：

```
[databaseHandle seekToFileOffset: [databaseHandle offsetInFile] + 128];
```

要向文件中回回等于五个整数的距离，写道：

```
[databaseHandle seekToFileOffset: [databaseHandle offsetInFile] - 5 * sizeof(int)];
```

程序 16.8 将一个文件的内容追加到另一个文件中。它通过打开第二个文件进行写入、寻道到文件末尾并将第一个文件的内容写入第二个文件来实现这一点。

# 程序 16.8

```
// 将 "fileA" 文件追加到 "fileB" 的末尾

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSFileHandle *inFile, *outFile;
        NSData *buffer;

        // 打开 fileA 进行读取
        inFile = [NSFileHandle
fileHandleForReadingAtPath: @"fileA"];

        if (inFile == nil) {
            NSLog (@"Open of fileA for reading
failed);\n
            return 1;
        }

        // 打开 fileB 进行更新
        outFile = [NSFileHandle
fileHandleForWritingAtPath: @"fileB"];

        if (outFile == nil) {
            NSLog (@"Open of fileB for writing
failed);\n
            return 2;
        }

        // 寻道到 outFile 的末尾
        [outFile seekToEndOfFile];

        // 读取 inFile 并将其内容写入 outFile
        buffer = [inFile readDataToEndFile];
        [outFile writeData: buffer];

        // 关闭两个文件
        [inFile closeFile];
        [outFile closeFile];

        // 验证其内容

        NSLog("%@", [NSString
stringWithContentsOfFile: @"fileB"
    encoding:NSUTF8StringEncoding error:
]);
        return 0;
    }
}
```

运行 [程序 16.8] 之前 fileA 的内容

```
这是第一个文件的第 1 行。
这是第一个文件的第 2 行。
```

运行 [程序 16.8] 之前 fileB 的内容

```
这是第二个文件的第 1 行。
这是第二个文件的第 2 行。
```

# 程序 16.8 输出

```
fileB 的内容
这是第二个文件的第 1 行。
这是第二个文件的第 2 行。
这是第一个文件的第 1 行。
这是第一个文件的第 2 行。
```

你可以看到第一个文件的内容是如何追加到第二个文件中的。你可能想在你的系统上尝试不同的值，看看效果最好。

# NSURL 类

`NSURL` 类提供了一种简单的方法来处理地址。例如，给定一个字符串，你可以使用 `URLWithString:` 创建。如果你有一个存储在网络地址的字典，可以使用 `dictionaryWithContentsURL:` 方法读取它。或者如果是一个数组，请使用 `arrayWithURL:` 方法。你可能还会通过 `dataWithURL:` 方法读取网络地址的任何类型的数据。

# 程序 16.9

```
// 读取文件的内容
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSURL *myURL = [NSURL URLWithString:@"testout"];

        NSString *myHomePage = [NSString stringWithContentsOfURL:myURL encoding:NSUTF8StringEncoding error:NULL];

        NSLog("%%@", myHomePage);
    }
}
```

# 程序 16.9 输出

```
<!DOCTYPE html PUBLIC "-W3C//DTD HTML1.0 Transitional//EN"
"http://www.w3.org/TR/html1/transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<meta http-equiv="Style-Type" content="text/css" />
<meta name="google-site-verification" content=""/>
<title>iPhone 在线课程与 iPhone 编程</title>
```

inDirectory: @"birdImages";

该方法返回一个路径名称数组。如果你的 JPEG 文件没有存储在应用程序的子目录下，你可以将 `""` 设置为 `inDirectory` 参数的值。

`NSBundle` 类中还有更多你想要学习的方法。请查看你的文档以获取详情。

# 练习题

- 1. 修改在程序 16.6 中开发的复制程序，使其能够接受多个源文件并复制到目录中，类似于标准的 UNIX `cp` 命令。这样，命令：

```
$ copy1.m file1.m file2.m progs
```

应该将 `copy1.m`、`file1.m` 和 `file2.m` 这三个文件复制到 `progs` 目录。请确保当指定了多个源文件时，最后一个参数实际上是一个存在的目录。

- 2. 编写一个名为 `find` 的命令行工具，它接受两个参数。第一个是开始搜索的起始目录，第二个是要查找的文件名。这样，命令：

```
$ myfind /Users proposal.doc
/Users/stevekochan/MyDocuments/proposals/proposals/al.doc
$
```

将从 `/Users` 开始搜索文件系统以定位 `proposal.doc` 文件。如果找到，则打印文件的完整路径（如所示）；如果没有找到，则打印适当的消息。

- 3. 编写你自己的版本的标准 UNIX 工具 `basename` 和 `dirname`。

- 4. 使用 `NSProcessInfo` 编写一个程序，显示其每个 getter 方法返回的所有信息。

- 5. 给本章描述的 `NSPathUtilities.h` 函数 `NSTemporaryDirectory` 和 `NSProcessInfo` 方法 `globallyString`，为 `NSString` 添加一个名为 `TempFiles` 的分类，并在其中定义一个名为 `temporaryFileName` 的方法，该方法每次被调用时返回一个不同的唯一文件名。

- 6. 修改程序 16.7，使文件每次读写 `kBufSize` 字节，其中 `kBufSize` 定义在程序的程序开头。请确保在大文件上测试该程序（即大于 `kBufSize` 字节的文件）。

- 7. 打开一个文件，每次读取 128 字节内容，并将其写入终端。使用 `NSFileHandle` 的 `fileHandleWithStandardOutput` 方法获取终端输出的句柄。

- 8. 一个字典以属性列表的形式存储在此 URL：http://bit.ly/aycNwd。编写一个程序读取该字典的内容并显示其内容。该字典包含什么数据？

# 17. 内存管理与自动引用计数

回想 `NSMutableArray` 类，它允许你创建一个可以添加对象和移除对象的数组。假设在你的程序执行开始时，你需要将一个文件的内容读取到数组中。假设你可以调用 `new array myData`，并且你想从一个以属性列表形式存储的文件（在第 19 章“归档”中有更详细的介绍）初始化它的内容。你可以使用 `NSArrayWithContentsOfFile:` 方法来实现，方法如下：

```
NSArray *myData = [NSArray arrayWithContentsOfFile:"database"];
```
