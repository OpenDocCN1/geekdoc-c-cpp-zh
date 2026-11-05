
```csharp
        // When the form is closing (default window X
        // box is clicked), close the file associated
        // with the StreamWriter object.
        private void SayingGUI_Closing(object sender,
            System.ComponentModel.CancelEventArgs e)
        {
            try
            {
                fil.Close();
            }
            catch
            {
                lblMsg.Text = "File did not close properly: ";
            }
        }
    }
```

运行应用程序，用户输入三条不同的格言，如图 13-5 所示。

![](img/e33ae760e23d89eac66541252ad65de8_825_0.png)

图 13-5 数据正被存储到文本文件中

当你查看示例 13-3 中的语句时，会注意到这个 Windows 应用程序中包含三个事件处理方法。在窗体加载事件处理程序中，实例化了 StreamWriter 类的一个对象。这段代码包含在 try...catch 子句中。按钮单击事件处理方法从文本框中检索字符串，并将文本写入文件。它也包含在 try...catch 子句中。第三个事件处理方法是窗体关闭时的事件。在这个事件处理方法中，文件在另一个 try...catch 块中关闭。使用图 13-5 中输入的数据，本次应用程序运行所创建文件的内容如图 13-6 所示。

![](img/e33ae760e23d89eac66541252ad65de8_826_0.png)

图 13-6 SayingGUI 应用程序创建的文本文件内容

在 Visual Studio 中，创建文件（或尝试访问文件）时，如果没有为文件名指定路径，则会使用当前项目的 bin\Debug 子目录。如果在 StreamWriter 对象的构造函数中列出了无效路径，那么应用程序一启动并加载窗体时，就会抛出 IOException 异常。为了演示这一点，示例 13-3 中更改了对构造函数的调用。在运行此应用程序的系统上，不存在 C:\Bob 子目录。因此，将 SayingGUI_Load( ) 方法中的对象构造函数从：

```csharp
fil = new StreamWriter("saying.txt");
```

改为：

```csharp
fil = new StreamWriter(@"C:\Bob\saying.txt");
```

窗体一加载就会抛出异常。为示例 13-3 设计用户界面时，窗体上放置了一个初始化为 ""（空字符串）的标签，用于显示错误消息。图 13-7 显示了抛出 DirectoryNotFoundException 异常时显示的消息。

![](img/e33ae760e23d89eac66541252ad65de8_827_0.png)

图 13-7 抛出 DirectoryNotFoundException

字符串字面量 "Invalid directory" 被连接到 DirectoryNotFoundException 对象 exc 的 Message 属性返回的字符串上。示例 13-4 重新给出了窗体加载时执行的 SayingGUI_Load( ) 方法。这一次，它包含了抛出异常时用于构造对象的无效路径参数，如图 13-7 所示。

### 示例 13-4

```csharp
private void SayingGUI_Load(object sender,
                          System.EventArgs e)
{
    try
    {
        fil = new StreamWriter
            (@"C:\Bob\saying.txt"); // Invalid path
    }
    catch (DirectoryNotFoundException exc)
    {
        lblMsg.Text = "Invalid directory"
                      + exc.Message;
    }

    catch (System.IO.IOException exc)
    {
        lblMsg.Text = exc.Message;
    }
}
```

如果不在 SayingGUI_Closing( ) 方法中包含 try...catch 子句，程序就会因未处理的异常而崩溃，因为指定无效路径时无法创建文件。

你也不能关闭一个不存在或当前未打开的文件。查看 SayingGUI_Closing( ) 方法中的 try...catch 子句时，注意这个 catch 的主体是空的。如果在尝试关闭文件时抛出并捕获了异常，则该异常会被传回 CLR 处理。

## 读取文本文件

StreamReader 类的设计目的是能够从文件中读取文本行。如果没有指定其他类型的编码（编码表示形式），则读取的字符默认会转换为 Unicode 字符字符串。

![](img/e33ae760e23d89eac66541252ad65de8_828_0.png)

> 默认情况下，使用 Unicode UTF-16 编码方案。它将字符表示为 16 位整数序列。你可以指定 Unicode UTF-8，其中字符表示为 8 位字节序列，或者使用 ASCII 编码，它将字符编码为单个 7 位 ASCII 字符。

使用 StreamReader 类的成员，访问文本文件的内容就像创建它一样容易。如表 13-6 所示，有几种方法可用于从文件中读取字符，包括 ReadLine( ) 方法。与 StreamWriter 类一样，StreamReader 的构造函数是重载的。你可以指定不同的编码方案，或指定用于检索数据的初始缓冲区大小。如果指定缓冲区大小，则必须以 16 位为增量给出。

使用 StreamReader 和 StreamWriter 对象时，你可以使用父类或祖先类的成员，或 File 类的静态成员。如表 13-2 所示，File.Exists( ) 可用于确定文件是否存在。在尝试构造对象之前，可以将文件名作为参数传递给 Exists( )。这是一种通过编程方式避免应用程序中抛出 FileNotFoundException 或 DirectoryNotFoundException 异常的方法。示例 13-5 说明了这一点。

值以顺序方式从文本文件中读取。就像创建文本文件时一样，指针会遍历文件，跟踪下一次读取的当前位置。示例 13-5 从包含姓名列表的文本文件中读取字符串。该文本文件使用这些值填充 Windows 应用程序的列表框。此应用程序演示了如何对 StreamReader 类使用异常处理技术。为简洁起见，下面的代码清单中不包含为 FileAccessApp.Designer.cs 和 Program.cs 文件生成的 Windows 窗体代码。该应用程序包含一个用于显示数据的 ListBox 对象和一个用于显示错误消息的 Label 对象。该标签最初设置为 null/空值。

![](img/e33ae760e23d89eac66541252ad65de8_829_0.png)

因为你经常需要读取一个或多个文件并将输出写入另一个文件，所以可以同时打开多个文件。

### 示例 13-5

```csharp
// FileAccessApp.cs
// Windows application that retrieves
// and stores values from a text file
// to a list box.
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.IO;  // Added for file access

namespace FileAccessApp
{
    public partial class FrmFileGUI : System.Windows.Forms.Form
    {
        private StreamReader inFile; // Declares a file stream object

        public FrmFileGUI()
        {
            InitializeComponent();
        }

        // Form load event handler used to construct
        // object of the StreamReader class, sending the
        // new filename as an argument. Enclosed in
        // a try...catch block.
        private void FrmFileGUI_Load(object sender,
            System.EventArgs e)
        {
            string inValue;
            if (File.Exists("name.txt"))
            {
                try
                {
                    inFile = new StreamReader("name.txt");
                    while ((inValue = inFile.ReadLine()) != null)
                    {
                        this.lstBoxNames.Items.Add(inValue);
                    }
                }
                catch (System.IO.IOException exc)
                {
                    lblMsg.Text = exc.Message;
                }
            }
            else
            {
                lblMsg.Text = "File unavailable";
            }
        }

        // When the close X is clicked, as the form is
        // closing, close the file associated with the
        // StreamReader object.
        private void FrmFileGUI_Closing(object sender,
            System.ComponentModel.CancelEventArgs e)
        {
            try
            {
                inFile.Close();
            }
            catch
            {
            }
        }
    }
}
```

在退出应用程序之前，请务必关闭所有文件。这可以确保数据可供下一个应用程序使用。如示例 13-5 所示，通过调用 Close( ) 方法关闭文件。该方法不接收任何参数；但是，必须使用文件对象来调用它（inFile.Close( )）；

图 13-8 显示了用于测试示例 13-5 中应用程序的文件内容。

![](img/e33ae760e23d89eac66541252ad65de8_830_0.png)

图 13-8 name.txt 文件的内容
