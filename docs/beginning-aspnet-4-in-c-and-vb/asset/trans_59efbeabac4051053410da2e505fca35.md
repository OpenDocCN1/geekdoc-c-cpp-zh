
除此之外，FileStream 还实现了与记账任务相关的各种其他方法和属性，例如确定流中包含多少字节、锁定流或刷新缓冲区。这些其他方法通常不用于基本的读写操作，但如果需要它们，完整的详细信息可在 SDK 文档中找到。

## BinaryFileReader 示例

FileStream 类的使用通过编写一个示例 BinaryFileReader 来说明，该示例读取并显示任何文件。在 Visual Studio 2010 中创建项目作为 Windows 应用程序。它有一个菜单项，会弹出一个标准的 OpenFileDialog，询问要读取哪个文件，然后以二进制代码形式显示该文件。由于您正在读取二进制文件，因此需要能够显示不可打印字符。您将通过单独显示文件的每个字节来实现这一点，在多行文本框的每一行显示 16 个字节。如果字节代表可打印的 ASCII 字符，您将显示该字符；否则，您将以十六进制格式显示该字节的值。在任何一种情况下，您都用空格填充显示的文本，以便每个显示的字节占用四列；这样，字节就能很好地在彼此下方对齐。

图 29-10 显示了在查看文本文件时 BinaryFileReader 应用程序的外观。（由于 BinaryFileReader 可以查看任何文件，因此完全可以将其用于文本文件以及二进制文件。）在这种情况下，应用程序读取了一个基本的 ASP.NET 页面（.aspx）。

![](img/d7d2ffa0a76feaab821930e95daace93_852_0.png)

图 29-10

显然，这种格式更适合查看单个字节的值，而不是显示文本！本章后面，当您开发一个专门用于读取文本文件的示例时，您将看到此文件真正的内容。此示例的优点是您可以查看任何文件的内容。

此示例未演示向文件写入，因为您不想陷入试图将如图 29-10 所示的文本框内容转换为二进制流的复杂性！您将在开发只能对文本文件进行读写操作的示例时 later 看到如何写入文件。

以下是用于获得这些结果的代码。首先，您需要确保已通过 using 语句引入 System.IO 命名空间：

```
using System.IO;
```

接下来，您在主窗体类中添加几个字段——一个表示文件对话框，一个字符串给出当前正在查看的文件的路径：

```
partial class Form1: Form
{
    private readonly OpenFileDialog chooseOpenFileDialog =
        new OpenFileDialog();
    private string chosenFile;
}
```

代码下载 BinaryFileReader.sln

您还需要添加一些标准的 Windows Forms 代码来处理菜单和文件对话框的事件处理程序：

```
public Form1()
{
    InitializeComponent();
    menuFileOpen.Click += OnFileOpen;
    chooseOpenFileDialog.FileOk += OnOpenFileDialogOK;
}

void OnFileOpen(object Sender, EventArgs e)
{
    chooseOpenFileDialog.ShowDialog();
}

void OnOpenFileDialogOK(object Sender, CancelEventArgs e)
{
    chosenFile = chooseOpenFileDialog.FileName;
    this.Text = Path.GetFileName(chosenFile);
    DisplayFile();
}
```

代码下载 BinaryFileReader.sln

正如这段代码所示，当用户在文件对话框中单击“确定”以选择文件时，您会调用 DisplayFile() 方法，该方法负责读取所选文件的工作：

```
void DisplayFile()
{
    int nCols = 16;
    FileStream inStream = new FileStream(chosenFile, FileMode.Open,
        FileAccess.Read);
    long nBytesToRead = inStream.Length;
    if (nBytesToRead > 65536/4)
        nBytesToRead = 65536/4;
    int nLines = (int)(nBytesToRead/nCols) + 1;
    string [] lines = new string[nLines];
    int nBytesRead = 0;
    for (int i=0; i<nLines; i++)
    {
        StringBuilder nextLine = new StringBuilder();
        nextLine.Capacity = 4*nCols;
        for (int j = 0; j<nCols; j++)
        {
            int nextByte = inStream.ReadByte();
            nBytesRead++;
            if (nextByte < 0 || nBytesRead > 65536)
                break;
            char nextChar = (char)nextByte;
            if (nextChar < 16)
                nextLine.Append('x' + string.Format("{0,1:X}", (int)nextChar));
            else if
                (char.IsLetterOrDigit(nextChar)) ||
                    char.IsPunctuation(nextChar)
                nextLine.Append(' ' + nextChar + ' ');
            else
                nextLine.Append('x' + string.Format("{0,2:X}", (int)nextChar));
        }
        lines[i] = nextLine.ToString();
    }
    inStream.Close();
}
this.textBoxContents.Lines = lines;
```

此方法中有相当多的内容，下面是分解说明。您为所选文件实例化一个 FileStream 对象，该对象指定您想要打开现有文件以进行读取。然后您计算出要读取的字节数以及应显示的行数。字节数通常为文件中的字节数。此示例将文本框控件中内容显示限制为最多 65,536 个字符——使用所选的显示格式，您为文件中的每个字节显示四个字符。

> > 您可能想查阅 System.Windows.Forms 命名空间中的 RichTextBox 类。RichTextBox 与文本框类似，但具有更多高级格式功能。这里使用 TextBox 是为了保持示例简单并专注于读取文件的过程。

该方法的大部分内容用于两个嵌套的 for 循环来构建要显示的每一行文本。您使用 StringBuilder 类来构建每一行，原因是为了性能：您将为每一行代表的字符串的每个字节附加合适的文本，共 16 次。如果每次都分配一个新字符串并复制半成品的行，您不仅会在分配字符串上花费大量时间，还会在堆上浪费大量内存。请注意，可打印字符的定义是字母、数字或标点符号，如相关的静态 System.Char 方法所示。但是，您将值小于 16 的任何字符从可打印列表中排除；这意味着您会将回车（13）和换行（10）捕获为二进制字符（多行文本框无法在行内单独出现时正确显示这些字符）。

此外，使用属性窗口，您将文本框的 Font 属性更改为等宽字体。在此情况下，您选择 Courier New 9pt regular，并将文本框设置为具有垂直和水平滚动条。

完成后，您关闭流并将文本框的内容设置为您构建的字符串数组。

## 读写文本文件

从理论上讲，完全可以使用 FileStream 类读取和显示文本文件。毕竟，您刚刚做过。前面示例中 Default.aspx 文件的显示格式并不特别用户友好，但这与 FileStream 类的任何固有问题无关，只与您选择在文本框中显示结果的方式有关。

话虽如此，如果您知道某个文件包含文本，通常会发现使用 StreamReader 和 StreamWriter 类而不是 FileStream 类更方便读写。这是因为这些类在稍微高一点的级别上工作，并且专门用于读写文本。它们实现的方法能够根据流的内容自动检测停止读取文本的合适点。特别是：

- 这些类实现按行读取或写入文本的方法，StreamReader.ReadLine() 和 StreamWriter.WriteLine()。在读取的情况下，这意味着流会为您自动确定下一个回车的位置并在该点停止读取。在写入的情况下，这意味着流会自动将回车-换行组合附加到写入的文本中。

- 通过使用 StreamReader 和 StreamWriter 类，您无需担心文件中使用的编码（文本格式）。可能的编码包括 ASCII（每个字符 1 个字节），或任何基于 Unicode 的格式，Unicode、UTF7、UTF8 和 UTF32。Windows 9x 系统上的文本文件始终为 ASCII，因为 Windows 9x 不支持 Unicode；然而，由于 Windows NT、2000、XP、2003、Vista、Windows Server 2008 和 Windows 7 都支持 Unicode，文本文件理论上可能包含 Unicode、UTF7、UTF8 或 UTF32 数据而不是 ASCII 数据。惯例是，如果文件为 ASCII 格式，它将只包含文本。如果它为任何 Unicode 格式，这将由文件的前 2 或 3 个字节指示，这些字节设置为特定值组合以指示文件中使用的格式。

这些字节被称为字节顺序标记。当您使用任何标准 Windows 应用程序（如记事本或写字板）打开文件时，您无需担心这一点，因为这些应用程序了解不同的编码方法并会自动正确读取文件。对于 StreamReader 类也是如此，它能正确读取任何这些格式的文件，而 StreamWriter 类能够使用您请求的任何编码技术格式化其写入的文本。但是，如果您想使用 FileStream 类读取和显示文本文件，则需要自行处理此问题。

## StreamReader 类

StreamReader 用于读取文本文件。与构造 FileStream 实例相比，构造 StreamReader 在某些方面更容易，因为使用 StreamReader 时不需要一些 FileStream 选项。特别是，模式和访问类型与 StreamReader 无关，因为您只能使用 StreamReader 进行读取！此外，没有直接选项来指定共享权限。但是，有几个新选项：

- 您需要指定如何处理不同的编码方法。您可以指示 StreamReader 检查文件开头的字节顺序标记以确定编码方法，或者您可以简单地告诉 StreamReader 假设文件使用指定的编码方法。

- 而不是提供要读取的文件名，您可以提供另一个流的引用。

最后一个选项值得更详细地讨论，因为它说明了将读写数据的模型基于流概念的另一个优点。由于 StreamReader 在相对较高的级别工作，如果您有另一个流用于从其他来源读取数据，但希望使用 StreamReader 提供的功能将该其他流作为包含文本进行处理，您可以这样做，只需将此流的输出传递给 StreamReader。这样，StreamReader 可用于读取和处理来自任何数据源的数据——不仅仅是文件。这本质上是前面关于 BinaryReader 类讨论的情况。然而，在本书中，您仅使用 StreamReader 直接连接到文件。

这些可能性导致 StreamReader 具有大量构造函数。不仅如此，还有另一个 FileInfo 方法返回 StreamReader 引用：OpenText()。以下只是说明了一些构造函数。
