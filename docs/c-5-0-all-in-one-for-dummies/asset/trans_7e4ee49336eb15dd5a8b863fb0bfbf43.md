

```
ArrayList ints = new ArrayList(); // An old-fashioned list of Objects
int myInt = (int)ints[0]; // Extract the first int in the list.
```

就好像你的整数被藏在复活节彩蛋里。如果不进行强制转换，就会产生错误，因为例如Object不支持你期望整数具有的+操作或其他方法、属性和运算符。你可以忍受这些限制，但这种代码容易出错，而且进行所有这些强制转换确实很繁琐。（此外，正如我在第1册第8章中讨论的，处理复活节彩蛋会因“装箱”现象而增加一些处理开销。过多的装箱会降低程序速度。）

而且，如果集合中碰巧包含多种类型的对象——比如石榴和篮球——问题就变得更棘手了。不知何故，你必须检测出取出的对象是石榴还是篮球，以便正确地进行强制转换。

由于旧的非泛型集合存在这些限制，较新的泛型集合就像一股清新的空气。你永远不必进行强制转换，而且你总是知道会得到什么，因为任何给定集合中只能放入一种类型。但你仍然会偶尔在别人编写的代码中看到较旧的集合——有时你甚至可能有正当理由将苹果和橙子放在同一个集合中。

![](img/80ff26f06fc9ab951e1cd4257b867366_157_0.png)

非泛型集合位于System.Collections和System.Collections.Specialized命名空间中。Specialized集合是有趣、有时有用、古怪的集合，而且主要是非泛型的。现代的泛型集合位于System.Collections.Generic中。（我在第2册中讨论面向对象编程时解释了命名空间和泛型。）

## 第7章：遍历集合

### 本章内容

- 将目录作为文件集合、将文件作为字节集合来处理
- “枚举”或迭代集合
- 实现索引器以方便访问集合对象
- 使用C#迭代器块轻松循环访问集合

本分册第6章探讨了.NET Framework类库提供的、可供C#及其他.NET语言使用的集合类。集合类是.NET中的构造，可以实例化以保存一组项（见第6章）。

本章第一部分稍微扩展了集合的概念。例如，考虑以下集合：将文件视为数据行或数据记录的集合，将目录视为文件的集合。因此，本章既基于本分册第6章的集合内容，也基于第3册的文件内容。

然而，本章的重点是遍历或迭代各类集合的几种方法，从文件目录到各种数组和列表。

### 遍历文件目录

读写是你在这一领域立足的基本技能。这正是第3册中FileRead和FileWrite程序的重要之处。然而，在某些情况下，你只是想快速浏览一个文件目录，寻找某些内容。

下面的LoopThroughFiles程序会查看指定目录中的所有文件，读取每个文件并将其内容以十六进制格式转储到控制台。（这听起来可能有点傻，但这个程序也演示了如何以不仅仅是字符串的格式写出文件。我将在下面的侧边栏“认识十六进制”中介绍十六进制格式。）

![](img/80ff26f06fc9ab951e1cd4257b867366_159_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_159_1.png)

如果你在一个包含大量文件的目录中运行此程序，十六进制转储可能需要一段时间。此外，长文件也需要一段时间来循环处理。要么选择一个文件较少的目录，要么按Ctrl+C终止耗时较长的程序运行。该命令会中断在任何控制台窗口中运行的程序。

```
// LoopThroughFiles -- Loop through all files contained in a directory;
// this time perform a hex dump, though it could have been anything.
using System;
using System.IO;

namespace LoopThroughFiles
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // If no directory name provided...
            string directoryName;
            if (args.Length == 0)
            {
                // ...get the name of the current directory...
                directoryName = Directory.GetCurrentDirectory();
            }
            else
            {
                // ...otherwise, assume that the first argument
                // is the name of the directory to use.
                directoryName = args[0];
            }
            Console.WriteLine(directoryName);

            // Get a list of all files in that directory.
            FileInfo[] files = GetFileList(directoryName);

            // Now iterate through the files in that list,
            // performing a hex dump of each file.
            foreach(FileInfo file in files)
            {
                // Write out the name of the file.
                Console.WriteLine("\n\nhex dump of file {0}:", file.FullName);

                // Now "dump" the file to the console.
                DumpHex(file);

                // Wait before outputting next file.
                Console.WriteLine("\nenter return to continue to next file");
                Console.ReadLine();
            }

            // That's it!
            Console.WriteLine("\no files left!");
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // GetFileList -- Get a list of all files in a specified directory.
        public static FileInfo[] GetFileList(string directoryName)
        {
            // Start with an empty list.
            FileInfo[] files = new FileInfo[0];
            try
            {
                // Get directory information.
                DirectoryInfo di = new DirectoryInfo(directoryName);

                // That information object has a list of the contents.
                files = di.GetFiles();
            }
            catch(Exception e)
            {
                Console.WriteLine("Directory \"{0}\" invalid", directoryName);
                Console.WriteLine(e.Message);
            }
            return files;
        }

        // DumpHex -- Given a file, dump out the contents of the file to the console.
        public static void DumpHex(FileInfo file)
        {
            // Open the file.
            FileStream fs;
            BinaryReader reader;
            try
            {
                fs = file.OpenRead();
                // Wrap the file stream in a BinaryReader.
                reader = new BinaryReader(fs);
            }
            catch(Exception e)
            {
                Console.WriteLine("can't read from \"{0}\"", file.FullName);
                Console.WriteLine(e.Message);
                return;
            }

            // Iterate through the contents of the file one line at a time.
            for(int line = 1; true; line++)
            {
                // Read another 10 bytes across (all that will fit on a single
                // line) -- return when no data remains.
                byte[] buffer = new byte[10];
                // Use the BinaryReader to read bytes.
                // Note: Using the bare FileStream
                // would have been just as easy in this case.
                int numBytes = reader.Read(buffer, 0, buffer.Length);
                if (numBytes == 0)
                {
                    return;
                }

                // Write out the data just read,
                // in a single line preceded by line number.
                Console.Write("{0:D3} - ", line);
                DumpBuffer(buffer, numBytes);

                // Stop every 20 lines so that the data doesn't scroll
                // off the top of the Console screen.
                if ((line % 20) == 0)
                {
                    Console.WriteLine("Enter return to continue another 20 lines");
                    Console.ReadLine();
                }
            }
        }

        // DumpBuffer -- Write a buffer of characters as a single line in hex format.
        public static void DumpBuffer(byte[] buffer, int numBytes)
        {
            for(int index = 0; index < numBytes; index++)
            {
                byte b = buffer[index];
                Console.Write("{0:X2}, ", b);
            }
            Console.WriteLine();
        }
    }
}
```

在命令行中，用户指定要使用的目录作为程序的参数。下面的命令将对temp目录中的每个文件（包括二进制文件和文本文件）进行十六进制转储：

```
loopthroughfiles c:\randy\temp
```

如果不输入目录名，程序默认使用当前目录。（十六进制转储将输出显示为十六进制（基数为16）数字系统的数字。参见旁边的侧边栏“认识十六进制”。）

![](img/80ff26f06fc9ab951e1cd4257b867366_161_0.png)

FileRead和FileWrite都从控制台读取输入文件名，而这个程序从命令行读取输入。我真的不是在故意迷惑你——我只是想展示解决同一问题的不同方法。

LoopThroughFiles中的第一行查找程序参数。如果参数列表为空（args.Length为零），程序将调用Directory.GetCurrentDirectory()。如果你在Visual Studio中运行（而不是在命令行中运行），该值默认为LoopThroughFiles项目目录下的bin\Debug子目录。

![](img/80ff26f06fc9ab951e1cd4257b867366_161_1.png)

Directory类为用户提供了一组操作目录的方法。FileInfo类提供了移动、复制和删除文件等方法，以及其他任务。

然后，程序通过调用本地的GetFileList()创建指定目录中所有文件的列表。该方法返回一个FileInfo对象数组。每个FileInfo对象包含有关文件的信息——例如文件名（带完整路径的FullName或不带路径的Name）、创建日期和最后修改日期。Main()使用你的老朋友foreach语句迭代文件列表。它显示每个文件的名称，然后将文件传递给DumpHex()方法以显示到控制台。

