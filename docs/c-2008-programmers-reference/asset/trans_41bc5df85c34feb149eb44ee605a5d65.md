

![](img/a977a875c7c627b45d939729705a252e_550_0.png)

图 16-13

要在 Windows 应用程序中加入打印功能，可以将 `PrintDocument` 控件拖放到窗体上，也可以在运行时创建 `PrintDocument` 类的实例。本例采用后一种方法。

要启动打印过程，请使用 `PrintDocument` 类的 `Print()` 方法。若要使用 `PrintDocument` 对象自定义打印过程，通常需要了解以下三个事件：

- BeginPrint — 在调用 Print() 方法后、打印文档第一页之前发生。通常使用此事件初始化打印过程中所用的字体、文件流和其他资源。
- PrintPage — 在需要打印当前页的输出内容时发生。这是编写将输出内容发送到打印机所需逻辑的主要事件。
- EndPrint — 在文档最后一页打印完成时发生。通常使用此事件释放打印过程中所用的字体、文件流和其他资源。

## 向项目添加打印支持

要为 `PhotoViewer` 应用程序添加打印支持，首先添加下表中的控件（见图 16-14）。

| 控件 | 文本 | 名称 |
|---|---|---|
| 标签控件 (2) | 打印范围： | |
|  | 至 | |
| 文本框控件 (2) |  | txtFrom |
|  |  | txtTo |
| 按钮控件 (2) | 预览 | btnPreview |
|  | 打印 | btnPrint |

## 第二部分：使用 C# 进行应用程序开发

![](img/a977a875c7c627b45d939729705a252e_551_0.png)

图 16-14

切换到 Form1 的代码隐藏文件，并导入以下命名空间：

```csharp
using System.Drawing.Printing;
```

声明以下成员变量：

```csharp
public partial class Form1 : Form
{
    //---constants for the icon images---
    const int ico_OPEN = 0;
    const int ico_CLOSE = 1;
    const int ico_PHOTO = 2;

    //---font variables---
    Font f_title;
    Font f_body;

    //---page counter---
    int pagecounter;

    //---PrintDocument variable---
    PrintDocument printDoc;
}
```

窗体在运行时加载时，创建 `PrintDocument` 类的实例，并为其连接前面介绍的三个主要事件处理程序：

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    printDoc = new PrintDocument()
    {
        DocumentName = "Printing from Photo Viewer"
    };
    printDoc.BeginPrint += new PrintEventHandler(printDoc_BeginPrint);
    printDoc.PrintPage += new PrintPageEventHandler(printDoc_PrintPage);
    printDoc.EndPrint += new PrintEventHandler(printDoc_EndPrint);

    try
    {
        //---load the application settings values
        // into the textbox controls---
        ...
```

在 BeginPrint 事件的事件处理程序中，初始化页计数器以及用于打印页面文本的字体：

```csharp
void printDoc_BeginPrint(object sender, PrintEventArgs e)
{
    //---initialize the page counter---
    pagecounter = int.Parse(txtFrom.Text);

    //---initialize the fonts---
    f_title = new Font("Arial", 16, FontStyle.Bold);
    f_body = new Font("Times New Roman", 10);
}
```

在 EndPrint 事件处理程序中，取消引用所使用的字体变量：

```csharp
void printDoc_EndPrint(object sender, PrintEventArgs e)
{
    //---de-reference the fonts---
    f_title = null;
    f_body = null;
}
```

最后，PrintPage 事件处理程序用于完成将输出内容发送到打印机的大部分工作。基本上，使用 `PrintPageEventArgs` 类中的 `Graphics` 对象指定要打印的输出内容。例如，若要绘制矩形，可使用 `e.Graphics.DrawRectangle()` 方法（其中 `e` 是 `PrintPageEventArgs` 类的实例）。若要打印字符串，则使用 `e.Graphics.DrawString()` 方法。打印后，递增页计数并判断是否还有更多页面需要打印。如果还有页面，将 `PrintPageEventArgs` 类的 `HasMorePages` 属性设为 `true`，即可再次触发 `printDoc_PrintPage` 事件处理程序。没有剩余页面时，将 `HasMorePages` 属性设为 `false`：

```csharp
void printDoc_PrintPage(object sender, PrintPageEventArgs e)
{
    Graphics g = e.Graphics;

    //--draws the title--
    g.DrawString(TreeView1.SelectedNode.Text,
        f_title, Brushes.Black, 20, 30);

    //--draws a border...--
    Rectangle border =
        new Rectangle(10, 10,
            PictureBox1.Width + 20, PictureBox1.Height + 60);

    //--...using a thick pen---
    Pen thickPen = new Pen(Color.Black, 3);
    g.DrawRectangle(thickPen, border);

    //--draws the picture--
    if (PictureBox1.Image != null)
    {
        g.DrawImage(PictureBox1.Image, 20, 60,
            PictureBox1.Size.Width,
            PictureBox1.Size.Height);
    }

    //--draws the page count--
    g.DrawString("Page " + pagecounter,
        f_body, Brushes.Black,
        20, 420);

    //--increments the page counter---
    pagecounter += 1;

    //--determine if you have more pages to print---
    if (pagecounter <= int.Parse(txtTo.Text))
        e.HasMorePages = true;
    else
        e.HasMorePages = false;
}
```

## 第二部分：使用 C# 进行应用程序开发

若要将图像打印到打印机，请使用 `PrintDialog` 类让用户选择所需的打印机（见图 16-16），而不是将输出内容直接发送到默认打印机：

```csharp
private void btnPrint_Click(object sender, EventArgs e)
{
    //---let user select a printer to print---
    PrintDialog pd = new PrintDialog()
    {
        Document = printDoc,
        AllowSomePages = true
    };

    DialogResult result = pd.ShowDialog();
    if (result == DialogResult.OK)
        printDoc.Print();
}
```

![](img/a977a875c7c627b45d939729705a252e_555_0.png)

图 16-16

图 16-17 显示了用户（在 Form1 中）指定打印第 1 页至第 3 页时的输出。请注意，图像下方显示了页码。

![](img/a977a875c7c627b45d939729705a252e_556_0.png)

图 16-17

## 部署应用程序

现在，应用程序已准备好部署给客户。如今，Windows 应用程序开发人员面临的最具挑战性的任务之一，就是将应用程序部署到客户端计算机上。应用程序部署后，任何更改或维护都需要重新部署。更糟的是，客户端配置千差万别，更新 Windows 应用程序总是充满未知因素。

## 第二部分：使用 C# 进行应用程序开发

从 Visual Studio 2005 开始，Microsoft 推出了一种名为 ClickOnce 的全新部署技术，使部署乃至更新都变得极其轻松省事。ClickOnce 专为简化 Windows 应用程序的部署而设计，尤其适用于智能客户端。智能客户端基本上是一种 Windows 应用程序，它能够利用本地资源，并根据需要智能地连接到分布式数据源（例如 Web 服务）。如今，许多公司都在部署 Web 应用程序（因为 Web 可随处访问），但网络延迟和服务器响应延迟等问题，阻碍了开发人员充分发挥 Web 的优势。Web 应用程序常见的问题包括网站响应缓慢，以及功能有限（这是由 HTTP 协议的无状态特性导致的）。智能客户端旨在兼具客户端（Windows）的丰富功能与后端 Web 服务的强大能力。

借助 ClickOnce，Windows 应用程序可以通过 Web 服务器、文件服务器，甚至 CD 轻松部署。使用 ClickOnce 安装应用程序后，它可以自动检查发布者是否提供了新更新，从而大大减少维护和升级应用程序所需的工作量。在安全性方面，ClickOnce 应用程序运行在安全沙盒中，并使用代码访问安全性模型进行配置。

## 使用 ClickOnce 发布应用程序

使用 ClickOnce 部署应用程序非常简单。在 Visual Studio 2008 中，选择“生成” → “发布 PhotoViewer”（见图 16-18）。

![](img/a977a875c7c627b45d939729705a252e_557_0.png)

图 16-18

随后将打开“发布向导”（见图 16-19）。默认情况下，应用程序将发布到本地 Web 服务器（IIS），路径如文本框中所示。不过，也可以通过磁盘路径、文件共享、FTP 或外部 Web 服务器发布应用程序。本例使用默认设置，单击“下一步”。

