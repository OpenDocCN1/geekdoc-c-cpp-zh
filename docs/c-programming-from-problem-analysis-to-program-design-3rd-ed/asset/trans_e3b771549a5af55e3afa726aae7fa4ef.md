

![](img/e33ae760e23d89eac66541252ad65de8_831_0.png)

该文件使用记事本显示。不过，它是在 Visual Studio 中使用通过 **“文件”>“新建”>“文件”>“常规”** 菜单选项找到的 **“文本文件”** 模板创建的。它实际位于 bin\Debug 文件夹下的项目子目录中。如果你尝试在文字处理应用程序（例如 Microsoft Word）中创建它，请务必小心。必须将其保存为不带任何特殊格式的纯文本文件。

应用程序的一次示例运行如图 13–9 所示。

![](img/e33ae760e23d89eac66541252ad65de8_831_1.png)

**图 13–9** FileAccessApp 应用程序的输出

![](img/e33ae760e23d89eac66541252ad65de8_831_2.png)

ListBox 对象的属性之一是 Sorted。默认情况下，它被设置为 `false`；不过，你可以更改该设置，让列表框中的条目按排序顺序排列——即使它们在文件中并未排序。对于此应用程序，由于这些值是按名字输入的，排序并不合适。

在示例 13–5 中，`try…catch` 块被包含在一个选择语句中。`if` 语句用于检查文件是否存在。当指定了无效路径时，不会引发异常，并且会跳过 `try…catch` 块。请查看示例 13–5 中出现的 `while` 语句。

```
while ((inValue = inFile.ReadLine()) != null)
```

ReadLine( ) 方法用于与文件对象配合，从文件中检索一行文本。该行存储在 inValue 变量中。while 语句测试每次对文件的访问，并持续循环，直到 inValue == null，这表示所有行都已读取。

## 添加 using 语句

`using` 关键字有两个主要用途。此前，你在程序语句中添加 `using` 子句，以导入命名空间中定义的类型。这样做可以避免对类型引用进行完全限定。例如，通过添加 `using System`，你可以编写 `Console.WriteLine( )`，而不必编写 `System.Console.WriteLine( )`。在 Visual Studio 中工作时，你还会注意到，一旦使用 `using` 语句添加了对特定命名空间的引用，IntelliSense 就能列出该命名空间中引用的该类型的有效成员。

`using` 关键字的第二个主要用途是为对象定义作用域，并让公共语言运行时（CLR）在对象超出作用域时自动处置或释放资源。这在处理文件或数据库时非常有用。例如，如果你正在将数据写入文件，那么在文件关闭之前，数据不会正确存储在文件中。如果未能关闭文件，你会发现一个空文件。`using` 块与文件一起使用时，可确保文件正确关闭。你不必调用 `Close( )` 方法。当对象超出作用域时，CLR 会自动为你调用该方法。示例 13-6 演示了如何添加 `using` 语句来定义 `StreamReader` 对象。

### 示例 13-6

```csharp
// FileAccessAppWithUsing.cs
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.IO;    //Added for file access

namespace FileAccessApp
{
    public partial class FrmFileGUI : Form
    {
        public FrmFileGUI( )
        {
            InitializeComponent( );
        }

        private void FrmFileGUI_Load(object sender,
                                     System.EventArgs e)
        {
            string inValue;
            try
            {
                using (StreamReader inFile =
                       new StreamReader("name.txt"))
                {
                    while ((inValue =
                           inFile.ReadLine()) != null)
                    {
                        this.lstBoxNames.Items.Add(inValue);
                    }
                }
            }
            catch (FileNotFoundException exc)
            {
                lblMsg.Text = "File Not Found !\n" + exc.Message;
            }
            catch (Exception exc)
            {
                lblMsg.Text = exc.Message;
            }
        }
    }
}
```

与前面的示例一样，FileAccessApp.Designer.cs 和 Program.cs 文件未显示。这些文件包含在 Visual Studio 中自动创建的 Windows 生成代码。

请注意，在示例 13-6 中，StreamReader 对象是在 using 块内定义并实例化的。这发生在 try 子句内。通过在此处实例化 inFile 对象，该对象仅存在于这个块中，并且可以保证在退出该块时文件已关闭。此时，inFile 对象的资源被释放回内存。另请注意，通过将对象的声明和实例化放在 using 语句中，你不再需要调用 Close( ) 方法。

如果将示例 13-6 与示例 13-5 进行比较，你还会注意到 if 语句，它用于检查文件是否存在或已被移除。为 FileNotFoundException 添加了一个额外的 catch 子句。它被放在带有 Exception 类的 catch 之前，因为 Exception 是所有异常类的基类，并且比 FileNotFoundException 类更通用。

using 语句可用于与 try...catch 子句分离。它在处理文件时非常有用，因为它在退出时会自动释放资源并关闭文件。但是，如示例 13-7 所示使用时，aFont 和 c 对象仅存在于由花括号指定的块内。尝试在该块外部引用这些对象将生成编译器错误。

### 示例 13-7

```csharp
// Adding a using statement
using (Font aFont = new Font("Arial", 12.0f),
    Customer c = new Customer())
{
    // Statements referencing aFont and c
}
```

如示例 13-7 所示，如果要声明并实例化多个对象，请在实例化之间使用逗号。

## 随机访问

FileStream 类还支持随机访问数据。值可以按任意顺序处理。使用随机访问时，可以在处理第一条记录之前检索并处理第五条数据记录。这是通过一种称为“查找”的概念实现的，它会修改当前位置。因此，你不需要从文件或内存流的开头按顺序读写数据，而是指定要处理的位置或记录。

FileStream 类的成员之一是 Seek( ) 方法。Seek( ) 允许你使用偏移引用参数将读取或写入位置移动到流中的任意位置。偏移可以相对于开头、当前位置或末尾来指定。Seek( ) 方法接受两个参数。第一个参数指定距原点的字节数，第二个参数指定原点。原点的枚举值为 SeekOrigin.Begin、SeekOrigin.End 和 SeekOrigin.Current。

还支持查找到超出流长度的位置。当你查找到超出文件长度的位置时，文件大小会增长。随机访问和查找既可用于文本文件，也可用于二进制文件，这是下一节的主题。

## BinaryReader 和 BinaryWriter 类

BinaryWriter 和 BinaryReader 类用于写入和读取二进制数据，而不是字符串。创建的文件可由计算机读取，但与 StreamWriter 类创建的文件不同，你不能简单地使用记事本打开并读取二进制文件的内容。需要程序来解释文件内容。写入或读取二进制文件很容易。除了构造函数之外，BinaryWriter 和 BinaryReader 类还公开了许多实例方法。表 13-7 和表 13-8 列出了一些关键的实例方法。

表 13-7 BinaryWriter 成员

| 方法 | 说明 |
|---|---|
| Close( ) | 关闭当前 BinaryWriter 和基础流 |
| Flush( ) | 清除当前写入器的所有缓冲区，并将任何缓冲数据写入基础设备 |
| Seek( ) | 设置当前流中的位置 |
| Write( ) | 将值写入当前流 |
| Write7BitEncodedInt( ) | 以压缩格式写入 32 位整数 |

