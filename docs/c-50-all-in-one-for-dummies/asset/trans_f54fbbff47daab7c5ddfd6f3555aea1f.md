

# 450 从流中提取：使用 StreamReader

你可以在网页上的 FileWriteUsing 示例查看 FileWrite 的重写版本。请注意，在重写过程中，我必须对两个 Main() 调用进行取消重构，将代码提取回到 Main() 中——即进行内联——然后才能引入代码块。

![](img/6df7bb88e9302e98442acc219cfbd7fc_475_0.png)

# 将它们从流中提取：使用 StreamReader

写入文件很酷，但如果你以后无法读回文件，那么它就毫无意义。下面的 FileRead 程序将输入放回短语 I/O。此程序读取类似于 FileWrite 或记事本创建的文本文件——它是 FileWrite 的反向操作（注意我没有使用这一个）：![](img/6df7bb88e9302e98442acc219cfbd7fc_475_1.png)

```csharp
// FileRead -- 读取文本文件并输出到控制台
using System;
using System.IO;

namespace FileRead
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // 你需要一个读取对象。
            StreamReader sr = null;
            string fileName = "";

            try
            {
                // 从用户获取文件名。
                sr = GetReaderFile(fileName);
            }
            catch (IOException err)
            {
                // TODO: 发布之前，将此替换为友好的消息。
                Console.WriteLine("{0}\n", err.Message);
            }
            finally
            {
                // 清理。
                if (sr != null) // 防止尝试关闭空对象
                {
                    sr.Close(); // 也会处理刷新操作
                    sr = null;
                }
            }

            // 等待用户确认结果。
            Console.WriteLine("按回车键终止...");
            Console.Read();
        }
    }
}
```

# 从流中提取：使用 StreamReader

```csharp
// GetReaderFile -- 打开文件并返回其对应的 StreamReader。
private static GetReaderFile(string fileName)
{
    StreamReader sr;
    // 输入：
    Console.Write("要读取的文件名是: ");
    fileName = Console.ReadLine();

    // 用户没有输入任何内容，抛出异常以表示这是不可接受的。
    if (fileName.Length == 0)
    {
        throw new IOException("你需要输入文件名.");
    }

    // 获取了名称 —— 打开一个用于读取的流；如果不存在则不创建。
    FileStream fs = File.Open(fileName, FileMode.Open, FileAccess.Read);

    // 在流上封装 StreamReader —— 这使用文件的前几个字节来指示编码（但语言）。
    sr = new StreamReader(fs);
    return sr;
}

// ReadToFileConsole -- 从 sr 代表的文件读取行并将其写入控制台。
private static void ReadToFileConsole(StreamReader sr)
{
    Console.WriteLine("\n文件内容：");
    // 一次读取一行。
    while (true)
    {
        // 读取一行。
        string input = sr.ReadLine();

        // 当再也读不到内容时退出。
        if (input == null)
        {
            break;
        }

        // 将你读取的任何内容写入控制台。
        Console.WriteLine(input);
    }
}
```

记得 FileRead 使用的当前目录是 FileWrite 项目下的 \bin\Debug 目录，我们在上一节中在该目录中创建了一些测试。在运行 FileRead 进行尝试之前，将任何文本文件 (.txt) 放在 \bin\Debug 目录并命名以便打开它。在 FileWrite 示例中创建的 TestFile.txt 副本会很好。![](img/6df7bb88e9302e98442acc219cfbd7fc_476_0.png)

在 FileReader 中，用户读取且仅读取一个文件。用户必须输入有效的文件名程序才能输出。没有更改。在程序读取文件后，它就会退出。如果用户想额外查看第二个文件，她必须再次运行程序。这是一个你可能会有不同设计的选择。

程序启动时，所有的源代码都封装在一个异常处理程序中。在 try 块中，该处理程序尝试调用两个方法：首先获取文件的 StreamReader，然后读取文件并将其行转储到控制台。如果发生异常，catch 块将写入异常消息。最后，finally 块确保流和文件已关闭，并且变量 sr 为 null，以便垃圾收集器回收它（见第二卷）。从 try 块中调用的任何方法都可能发生 I/O 异常。这些异常传播到 Main() 寻找处理程序（因为方法内部没有异常处理程序）。![](img/6df7bb88e9302e98442acc219cfbd7fc_477_0.png)

注意 catch 块中的 //TODO: 注释。这是为了在发布程序之前将消息设为用户友好的提醒。标记此类注释出现在 Visual Studio 的任务列表窗口中。在此窗口中，从左角的下拉列表中选择“注释（Comments）”。双击某一项可以在代码中打开或编辑该注释。

由于变量 sr 在异常块中使用，你必须在最初将其设置为 null —— 否则编译器会报错在异常块中使用了未初始化的变量。同样，在尝试调用其 Close() 方法之前，检查 sr 是否（或仍然）为 null。更好的方法是将程序转换为使用 using。

