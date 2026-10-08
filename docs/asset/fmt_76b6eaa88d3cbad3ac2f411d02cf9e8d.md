
```cs
// FileAccessWithUsing.cs
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.IO;      //添加用于文件访问
namespace FileAccessApp
{
    public partial class FrmFileGUI : Form
    {
        public FrmFileGUI()
        {
            InitializeComponent();
            private void FrmFileGUI_Load(object sender
```

```csharp
catch (FileNotFound exc)
{
    lbl1Msg.Text = "File Not Found !\n" + exc.Message;
}
catch (Exception exc)
{
    lbl1Msg.Text = exc.Message;
}
}
```

> 注意 与之前的示例一样，未显示 `FileAccessDesigner.cs` 和 `Program.cs` 文件。这些文件包含 Visual Studio 自动生成的 Windows 代码。

注意示例 13-6，`StreamReader` 对象是在 `using` 块内部定义并实例化的。这发生在 `try` 子句内部。通过在此 `using` 块中实例化 `inFile` 对象，可以保证在退出块时文件已关闭。此时，`inFile` 对象被释放回内存。此外注意在 `using` 语句中声明并实例化对象，不再需要调用 `Close()` 方法。

将示例 13-6 与示例 13-5 比较，你还会注意到一个 `if` 语句，用于检查文件是否存在，并且为 `FileNotFoundException` 添加了额外的 `catch` 子句，位于 `Exception` 之前，因为 `Exception` 类比 `FileNotFoundException` 类更通用。

`using` 语句可以与 `try...catch` 块分开。它对于处理文件非常有用，因为它在退出时会自动释放资源并关闭文件。然而，在示例 13-7 中，`Font` 和 `c` 对象仅存在于括号内部。在块外部引用对象会导致编译器错误。

# 示例 13-7

## 添加 using 语句

```cs
using (Font aFont = new Font("Arial", 12.0f),
    Customer c = new Customer())
{
    // 引用 aFont 和 c
```

如示例 13-7 所示，如果你想声明并实例化多个对象，使用逗号。

# BinaryReader 和 BinaryWriter 类

## 随机访问

`StreamReader` 类也支持随机访问数据。可以按任何顺序处理。可以检索记录。`StreamReader` 的成员之一是 `Seek()` 方法。起点的枚举值为 `SeekOrigin.Begin`、`SeekOrigin.End` 和 `SeekOrigin.Current`。使用 `Seek()` 方法设置流中的位置。第一个参数是字节数，第二个参数是起点。

`BinaryReader` 和 `BinaryWriter` 类用于写入和读取二进制数据。`BinaryReader` 和 `BinaryWriter` 类提供了面向特定数据类型的流式功能。当你查看表 13-8 所示的 `BinaryReader` 方法时，你会注意到几个 `Read()` 方法。每个方法都专注于可能出现的数据类型。

### 表 13-7 BinaryWriter 成员

| 方法 | 说明 |
| --- | --- |
| `Close()` | 关闭当前 `BinaryWriter` 和底层流 |
| `Flush()` | 清除当前写入器的所有缓冲区，并将任何缓冲数据写入底层流 |
| `Seek()` | 设置当前流中的位置 |
| `Write()` | 将值写入当前流 |
| `WriteEncodedInt()` | 以压缩格式写入 32 位整数 |

### 表 13-8 BinaryReader 方法

| 方法 | 说明 |
|---|---|
| `Close()` | 关闭当前 `BinaryReader` 和底层流 |
| `PeekChar()` | 返回下一个可用字符，但不推进字节或字符位置 |
| `Read()` | 从底层流读取字符并推进当前流的位置 |
| `ReadBoolean()` | 从当前流读取一个布尔值，并将流位置推进 1 字节 |
| `ReadByte()` | 从当前流读取下一个字节，并将流位置推进 1 字节 |
| `ReadBytes()` | 从当前流读取指定数量的字节到字节数组，并推进指定字节数 |
| `ReadChar()` | 从当前流读取下一个字符并推进流的位置 |
| `ReadChars()` | 从当前流读取指定数量的字符并以字符数组返回，同时推进位置 |
| `ReadDecimal()` | 从当前流读取一个小数值，并将流位置推进 16 字节 |
| `ReadDouble()` | 从当前流读取一个 8 字节浮点值，并将流位置推进 8 字节 |
| `ReadInt32()` | 从当前流读取一个 4 字节有符号整数，并将流位置推进 4 字节 |
| `ReadString()` | 从当前流读取字符串；字符串前带有长度信息 |

示例 13-8 说明了如何使用 `BinaryWriter` 类创建一个存储整数、小数和字符串数据类型的二进制文件。

# 示例 13-8

```c
// BinaryFiles.cs
// 说明创建二进制文件
using System;
using System.Collections.Generic;
using System.Text;
using System.IO;

namespace BinaryFiles
{
    class BinaryExample
    {
        public static void Main( )
        {
            FileStream filStream;
            BinaryWriter binWriter;

            Console.Write("Enter name of the file: ");
            string fileName = Console.ReadLine();
            if (File.Exists(fileName))
            {
                Console.WriteLine("File - {0} already exists!", fileName);
            } else
            {
                filStream = new FileStream(fileName, FileMode.CreateNew);
                binWriter = new BinaryWriter(filStream);
                decimal aValue = 2.16M;

                binWriter.Write("Sample Run");
                for (int i = 0; i < 11; i++)
                {
                    binWriter.Write(i);
                }
                binWriter.Write(aValue);

                binWriter.Close( );
                filStream.Close();
                Console.WriteLine("File Created successfully");
            }
            Console.ReadLine();
        }
    }
}
```

# 第 13 章 处理文件

示例 13-8 首先检查用户输入的文件名是否存在。这是通过使用 `File` 类的静态方法 `Exists()` 实现的。当输入的名称是一个新文件时，会实例化 `FileStream` 和 `BinaryWriter` 类对象。注意 `FileStream` 构造函数的第二个参数是一个枚举。`FileMode` 类型指定了操作系统应该如何打开文件。如图 13-10 所示，字段值成员 `CreateNew` 表示操作系统创建一个新文件。IntelliSense 提示，如果文件已存在，将抛出 `SystemIO.IOException`。

```csharp
fstream = new FileStream(filename, FileMode);
binarywriter = new BinaryWriter(fream);
decimal aValue = 2.16M;
```

| FileMode |
| :--- |
| Append |
| Create |
| CreateNew |
| Open |
| OpenOrCreate |
| Truncate |

`FileMode.CreateNew` 指定操作系统应该创建一个新文件。这需要 `System.Security.Permissions.FilePermissionsAccess.Write`。如果文件已存在，将抛出 `SystemIO.IOException`。

图 13-10 可枚举 FileMode

`BinaryWriter` 对象基于 `FileStream` 对象或封装在 `FileStream` 对象之上。`FileStream` 对象作为参数传递给 `BinaryWriter` 构造函数。

在示例 13-8 中，首先向文件写入了一个字符串参数。接着是几个整数和一个十进制值。最后，为了正确创建文件，必须关闭两个文件。13-11 显示了生成的控制台输出。在图前景，你可以看到新创建的文件。

# BinaryReader 和 BinaryWriter 类 803

![](img/45e6f245af31396d967c3186f196d331_836_0.png)

图 13-11 创建的 TestBinaryCreation.txt 文件

如图 13-11 所示，由于没有指定路径，文件存储在项目的 `bin\debug` 目录中。

创建二进制文件后，你不能简单地用记事本打开文件并查看其内容。你会发现许多不可打印字符。你可以使用 `BinaryReader` 类编写程序语句来检索结果。这在示例 13-9 中所示。

# 示例 13-9

```csharp
// BinaryFileAccess.cs
// 说明从二进制文件中检索数据。

using System;
using System.Collections.Generic;
using System.Text;
using System.IO;

namespace BinaryFileAccess
{}
```

```csharp
class BinaryInput {
    public static void Main( ) {
        FileStream filStream;
        BinaryReader binReader;
        Console.Write("Enter name of the file: ");
        string fileName = Console.ReadLine();
        try {
            filStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
            binReader = new BinaryReader(filStream);
            RetrieveAndDisplayData(binReader);
            binReader.Close( );
            filStream.Close( );
        } catch (FileNotFoundException exc) {
            Console.WriteLine(exc.Message);
        } catch (InvalidDataException exc) {
            Console.WriteLine(exc.Message);
        } catch (EndOfStreamException exc) {
            Console.WriteLine(exc.Message);
        } catch (IOException exc) {
            Console.WriteLine(exc.Message);
        }
        Console.ReadLine();
    }

    public static void RetrieveAndDisplayData(BinaryReader binReader) {
        // 从文件中读取字符串数据。
        Console.WriteLine(binReader.ReadString( ));
        // 从文件中读取整数数据。
        for (int i = 0; i < 11; i++) {
            Console.WriteLine(binReader.ReadInt32( ));
        }
        // 从文件中读取十进制数据。
        Console.WriteLine(binReader.ReadDecimal());
    }
}
```

示例 13-9 所示的代码用于检索上一个应用程序 `BinaryFiles` 存储在二进制文件中的。`BinaryFiles` 的代码在示例 13-8 中显示。

## BinaryReader 和 BinaryWriter 类 807

这是通过使用 `OpenFileDialog` 和 `SaveFileDialog` 类实现的。这两个类都派自 `FileDialog` 类。`FileDialog` 是一个抽象类，不能实例化，但为 `OpenFileDialog` 和 `SaveFileDialog` 类提供了许多功能。这些类属于 `System.Windows.Forms` 命名空间。`FileDialog` 类有一个名为 `FileName` 的属性，`OpenFileDialog` 和 `SaveFileDialog` 类都使用该属性从对话框设置或获取文件名。

要在应用程序中添加对话框行为，请从工具箱将 `OpenFileDialog` 和/或 `SaveFileDialog` 控件拖到表单上。释放鼠标时，控件将放置在表单下方的组件区域，如图 13-13 所示。

![](img/45e6f245af31396d967c3186f196d331_840_0.png)

图 13-13 放置 OpenFileDialog 和 SaveFileDialog 控件

当 `OpenFileDialog` 放置在表单上时，`FileName` 属性的初始默认值为对象 `openFileDialog1` 的名称。你可以为 `FileName` 属性输入一个新值，或者如果你不想输入名称，可以删除 `FileName` 属性的值。这将导致文件名的文本框为空。

将对话框控件放置在表单后，使用 `ShowDialog()` 方法来打开对话框。`ShowDialog()` 方法也是抽象类 `FileDialog` 的成员。它在这两个派生类中均可用。如果你不更改对象的名称，而是使用默认名称，则你需要在程序中想要显示对话框的位置包含以下语句：

```
openFileDialog1.ShowDialog( );
```

或者

```
saveFileDialog1.ShowDialog( );
```

当使用 `openFileDialog1` 对象执行 `ShowDialog( )` 方法时，将显示如图 13-14 所示的打开文件对话框。
