
```csharp
catch (System.IO.IOException exc)
{
    lblMessage.Text = exc.Message;
}
else
{
    lblMessage.Text = "File unavailable";
}

// When the close X is clicked, as the form is
// closing, close the file associated with the
// StreamReader object.
private void FrmFileGUI_FormClosing(object sender,
    FormClosingEventArgs e)
{
    try
    {
        inFile.Close();
    }
    catch
    {
    }
}
```

## 注意

务必在退出应用程序之前关闭所有文件。这样可以确保数据可供下一个应用程序使用。如示例 13-5 所示，通过调用 Close( ) 方法关闭文件。不向该方法发送任何参数；但是，必须使用文件对象调用它（inFile.Close( );）。

图 13–8 显示了示例 13–5 中用于测试应用程序的文件内容。为了排序，文本文件中的姓名按姓氏在前的顺序放置。

![](img/36e48639a06772bcb0fa1ea2525b33a3_898_0.png)

**图 13–8** name.txt 文件的内容

> **注意**
> 
> 该文件使用记事本显示。但是，它是在 Visual Studio 中使用 **TextFile** 模板创建的，该模板可从 **文件、新建文件、常规** 菜单选项中找到。它实际位于 bin\Debug 文件夹下的项目子目录中。如果尝试在字处理应用程序（如 Microsoft Word）中创建它，请小心。必须将其保存为不带任何特殊格式的纯文本文件。

图 13–9 显示了该应用程序的一次示例运行。

![](img/36e48639a06772bcb0fa1ea2525b33a3_899_0.png)

**图 13–9** FileAccessApp 应用程序的输出

> **注意** ListBox 对象的属性之一是 `Sorted`。默认情况下，它被设置为 `false`；但是，您可以更改它，使列表框中的项按排序顺序排列——即使它们在文件中未排序。对于此应用程序，`Sorted` 属性已更改为 `true`。

在示例 13–5 中，try...catch 块被包含在一个选择语句中。if 语句用于检查文件是否存在。当指定了无效路径时，不会引发异常，并且会跳过 try...catch 块。请查看示例 13–5 中出现的 while 语句。

```
while ((inValue = inFile.ReadLine()) != null)
```

ReadLine() 方法与 infile 对象一起使用，以从文件中检索一行文本。该行存储在 inValue 变量中。while 语句测试每次从文件进行的访问，并继续循环，直到 inValue == null，表示所有行都已读取。

## 添加 using 语句

using 关键字有两个主要用途。以前，您向程序语句添加 using 子句，以导入命名空间中定义的类型。通过这样做，您可以避免对类型引用进行完全限定。例如，通过添加

using System，您可以编写 Console.WriteLine()，而不是 System.Console.WriteLine()。在 Visual Studio 中工作时，您还注意到，一旦使用 using 语句添加了对特定命名空间的引用，IntelliSense 就能够列出该命名空间中引用的该类型的有效成员。

using 关键字的第二个主要用途是为对象定义作用域，并让公共语言运行时（CLR）在对象超出作用域时自动释放该资源。这在处理文件或数据库时非常有用。例如，如果您正在将数据写入文件，则在文件关闭之前，数据不会正确存储在文件中。如果未能关闭文件，您会发现一个空文件。当与文件一起使用时，using 块可确保文件正确关闭。您不必调用 Close() 方法。当对象超出作用域时，CLR 会自动为您调用它。示例 13-6 说明了如何添加 using 语句来定义 StreamReader 对象。

## 示例 13.6

```csharp
// FileAccessAppWithUsing.cs
using System;
using System.Windows.Forms;
using System.IO; //Added for file access
namespace FileAccessApp
{
    public partial class FrmFileGUI : Form
    {
        public FrmFileGUI()
        {
            InitializeComponent();
        }

        private void FrmFileGUI_Load(object sender, EventArgs e)
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
                        this.lstBxNames.Items.Add(inValue);
                    }
                }

                catch (FileNotFoundException exc)
                {
                    lblMessage.Text = "File Not Found !\n" +
                        exc.Message;
                }
            }
        }
    }
}
```

```csharp
catch (Exception exc)
{
    lblMessage.Text = exc.Message;
}
}
}
}
}
```

> **注意**
> 
> 与之前的示例一样，未显示 FileAccessApp.Designer.cs 和 Program.cs 文件。这些文件包含由 Visual Studio 自动生成的代码。与教科书中的所有其他示例一样，完整应用程序可从出版商处获得，为可完全正常运行的 Visual Studio 项目。

请注意，在示例 13-6 中，StreamReader 对象是在 using 块内定义和实例化的。这发生在 try 子句内。通过在此处实例化 inFile 对象，该对象仅存在于该块中，并且可以保证在退出该块时文件已关闭。此时，inFile 对象的资源被释放回内存。另请注意，通过将对象的声明和实例化放在 using 语句中，您不再需要调用 Close() 方法。因此，您不再需要注册 Form_Closing() 事件。

如果将示例 13-6 与示例 13-5 进行比较，您还会注意到，用于检查文件是否存在的 if 语句已被移除。为 FileNotFoundException 添加了一个额外的 catch 子句。它被放在带有 Exception 类的 catch 之前，因为 Exception 是所有异常类的基类，并且比 FileNotFoundException 类更通用。

using 语句可以独立于 try...catch 子句使用。它在处理文件时非常有用，因为它会在退出时自动释放资源并关闭文件。但是，当如示例 13-7 所示那样使用时，aFont 和 c 对象仅存在于花括号指定的块内，因为它们是在那里定义的。尝试在该块外引用这些对象将产生编译器错误。

## 示例 13.7

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

FileStream 类还支持随机访问数据。值可以按任意顺序处理。使用随机访问时，可以在处理第一条记录之前检索并处理第五条数据记录。这是通过一个称为查找（seeking）的概念完成的，它会修改当前位置。因此，您不必从文件或内存流的开头按顺序读取或写入数据，而是指定要处理的位置或记录。

FileStream 类的成员之一是 Seek() 方法。Seek() 允许您使用偏移引用参数将读取或写入位置移动到流中的任意位置。偏移可以相对于开头、当前位置或结尾来指定。Seek() 方法接受两个参数。第一个参数指定从原点开始的字节数，第二个参数指定原点。原点的枚举值为 SeekOrigin.Begin、SeekOrigin.End 和 SeekOrigin.Current。

还支持查找到超出流长度的位置。当您查找到超出文件长度的位置时，文件大小会增长。随机访问和查找可用于文本文件，也可用于二进制文件，这是下一节的主题。

## BinaryReader 和 BinaryWriter 类

BinaryWriter 和 BinaryReader 类用于写入和读取二进制数据，而不是字符串。创建的文件可由计算机读取，但与 StreamWriter 类创建的文件不同，您不能简单地使用记事本打开并读取二进制文件的内容。需要程序来解释文件内容。写入二进制文件或从二进制文件读取很容易。除了构造函数之外，BinaryWriter 和 BinaryReader 类还公开了许多实例方法。表 13-7 和表 13-8 列出了一些关键的实例方法。

表 13-7 BinaryWriter 成员

| 方法 | 描述 |
|---|---|
| Close() | 关闭当前 BinaryWriter 和基础流 |
| Flush() | 清除当前写入器的所有缓冲区，并使所有缓冲数据写入基础设备 |
| Seek() | 设置当前流中的位置 |
| Write() | 将值写入当前流 |
| Write7BitEncodedInt() | 以压缩格式写入 32 位整数 |

