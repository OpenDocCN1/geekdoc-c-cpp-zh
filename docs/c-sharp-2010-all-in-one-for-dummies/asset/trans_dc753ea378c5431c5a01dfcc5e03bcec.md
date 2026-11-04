
## 使用流：示例

下面的 FileWrite 程序从控制台读取数据行并写入用户选择的文件中。这 是伪代码——它并非用于编译。我仅将其作为示例使用。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_464_0.png)

// FileWrite -- Write input from the Console into a text file.
using System;
using System.IO;

namespace FileWrite
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Get a filename from the user -- the while loop lets you
            // keep trying with different filenames until you succeed.
            StreamWriter sw = null;
            string fileName = "";
            while(true)
            {
                try
                {
                    // Enter output filename (simply hit Enter to quit).
                    Console.Write("Enter filename ");
                    Console.WriteLine("Enter blank filename to quit:");
                    fileName = Console.ReadLine();
                    if (fileName.Length == 0)
                    {
                        // No filename -- this jumps beyond the while
                        // loop for safety. You're done.
                        break;
                    }

                    // I factored out these tasks to simplify the loops a bit.
                    // Call a method (below) to set up the StreamWriter.
                    sw = GetWriterForFile(fileName);
                    // Read one string at a time, outputting each to the
                    // FileStream open for writing.
                    WriteFileFromConsole(sw);

                    // Done writing, so close the file you just created.
                    sw.Close(); // A very important step. Closes the file too.
                    sw = null; // Give it to the garbage collector.
                }
                catch (IOException ioErr)
                {
                    // Oops -- Error occurred during the processing of the
                    // file -- tell the user the full name of the file:
                    // Tack the name of the default directory to the filename.
                    string dir = Directory.GetCurrentDirectory(); // Directory class
                    string path = Path.Combine(dir, fileName); // System.IO.Path class
                    Console.WriteLine("Error on file {0}", path);

                    // Now output the error message in the exception.
                    Console.WriteLine(ioErr.Message);
                }
            }
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // GetWriterForFile -- Create a StreamWriter set up to write
        // to the specified file.
        private static StreamWriter GetWriterForFile(string fileName)
        {
            StreamWriter sw;
            // Open file for writing in one of these modes:
            // FileMode.CreateNew to create a file if it
            // doesn't already exist or throw an
            // exception if file exists.
            // FileMode.Append to append to an existing file
            // or create a new file if it doesn't exist.
            // FileMode.Create to create a new file or
            // truncate an existing file.

            // FileAccess possibilities are:
            // FileAccess.Read,
            // FileAccess.Write,
            // FileAccess.ReadWrite.
            FileStream fs = File.Open(fileName,
                FileMode.CreateNew,
                FileAccess.Write);
            // Generate a file stream with UTF8 characters.
            // Second parameter defaults to UTF8, so can be omitted.
            sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
            return sw;
        }

        // WriteFileFromConsole -- Read lines of text from the console
        // and spit them back out to the file.
        private static void WriteFileFromConsole(StreamWriter sw)
        {
            Console.WriteLine("Enter text; enter blank line to stop");
            while (true)
            {
                // Read next line from Console; quit if line is blank.
                string input = Console.ReadLine();
                if (input.Length == 0)
                {
                    break;
                }
                // Write the line just read to output file.
                sw.WriteLine(input);
                // Loop back up to get another line and write it.
            }
        }
    }
}

FileWrite 同时使用了 System.IO 命名空间和 System.Text。System.IO 包含文件 I/O 类。

## 启动新的 StreamWriter

FileWrite 程序在 Main() 中以包含 try 块的 while 循环开始。这对于文件操作程序来说很常见。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_466_0.png)

将所有文件 I/O 操作都放在 try 块中。文件 I/O 容易出现错误，例如缺少文件或目录、路径错误等。有关异常处理的更多信息，请参阅第一部分。

while 循环具有两个功能：

- 它允许程序在 I/O 失败时返回重试。例如，如果程序找不到用户想要读取的文件，程序可以在放弃用户之前再次询问文件名。
- 在程序内部执行 break 命令会让你直接跳过 try 块并到达循环末尾。这是退出方法或程序的便捷机制。请记住，break 只能让你退出它所在的循环。（第 4 章介绍循环和 break。）

FileWrite 程序从控制台读取要创建的文件名。如果用户输入空文件名，程序将通过跳出 while 循环而终止。程序的关键在于对 GetWriterForFile() 方法的调用；你可以在 Main() 下方找到该方法。GetWriterForFile() 中的关键行是

```
FileStream fs = File.Open(fileName, FileMode.CreateNew, FileAccess.Write);
...
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
```

在第一行中，程序创建了一个代表磁盘上输出文件的 FileStream 对象。此处使用的 FileStream 构造函数接受三个参数：

- 文件名：这显然是要打开的文件的名称。像 filename.txt 这样简单的名称被假定位于当前目录（对于 FileWrite，在 Visual Studio 中工作时，即项目目录下的 \bin\Debug 子目录；它是构建程序后包含 .EXE 文件的目录）。以反斜杠开头的 文件名，如 \some directory\filename.txt，被假定为本地机器上的完整路径。以两个斜杠开头的 文件名——例如 \\your machine\some directory\filename.txt——驻留在网络上的其他机器上。从这里开始，文件名的编码会变得迅速复杂，超出了本迷你书的范围。
- **文件模式：** 此参数指定要对文件执行的操作。基本写入模式有创建（CreateNew）、追加（Append）和覆盖（Create）。CreateNew 创建新文件，但如果文件已存在则抛出 IOException。Create 模式如果文件不存在则创建文件，但如果文件存在则覆盖（'截断'）文件。正如其名，Append 会在现有文件末尾添加内容，或在文件不存在时创建文件。
- **访问类型：** 文件可以以读取、写入或两者同时的方式打开。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_0.png)

FileStream 有许多构造函数，其中每个构造函数都会为模式和访问参数中的一个或两个设置默认值。然而，在我看来，你应该显式指定这些参数，因为它们对程序的清晰度有很大影响。这通常是很好的建议。默认值对程序员来说可能很方便，但对阅读代码的人来说却令人困惑。

在 GetWriterForFile() 方法的第二条非注释行中，程序将新打开的 FileStream 对象 '包装' 在 StreamWriter 对象 sw 中。StreamWriter 类围绕 FileStream 对象提供一组对文本友好的方法。该 StreamWriter 就是该方法返回的内容。

StreamWriter 构造函数的第一个参数是 FileStream 对象。这就是包装。第二个参数指定要使用的编码。默认编码是 UTF8。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_1.png)

读取文件时无需指定编码。StreamWriter 会在文件的前三个字节中写入编码类型。StreamReader 在打开文件时读取这三个字节以确定编码。隐藏此类细节是优秀软件库提供的优势。

## 最后，我们开始写入！

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_2.png)

在设置好 StreamWriter 后，FileWrite 程序开始从控制台读取字符串输入行（此代码位于从 Main() 调用的 WriteFileFromConsole() 方法中）。当用户输入空行时，程序停止读取；在那之前，它会吞下所有提供的内容并使用该类的 WriteLine() 方法将其吐入 StreamWriter sw。

StreamWriter.WriteLine() 与 Console.WriteLine() 之间的相似性不仅仅是巧合。

最后，流通过 sw.Close() 表达式关闭。这很重要，因为它也会关闭文件。（我在下一节中还有更多关于关闭事物的内容。）
