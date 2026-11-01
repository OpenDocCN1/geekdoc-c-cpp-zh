
```
if (position.X > margin + theLine.Width)
{
    return -1;
}
// all is OK. We can return answer
return index;
```

最后，在某些情况下，你还需要在线索引和页面坐标之间进行转换，而不是世界坐标。以下方法实现了这一点：

```
private Point LineIndexToPageCoordinates(int index)
{
    return LineIndexToWorldCoordinates(index) +
        new Size(AutoScrollPosition);
}
private int PageCoordinatesToLineIndex(Point position)
{
    return WorldCoordinatesToLineIndex(position - new
        Size(AutoScrollPosition));
}
```

请注意，在转换为页面坐标时，你需要加上 AutoScrollPosition，而它为负值。

虽然这些方法本身看起来并不特别有趣，但它们展示了一种通用技术，你很可能会经常需要使用它。使用 GDI+ 时，你经常会遇到这样一种情况：你获得了特定的坐标（例如用户点击鼠标的位置），并且需要弄清楚该点显示的是什么项目。或者情况可能相反——某个特定的显示项目应该在哪里显示？因此，如果你正在编写 GDI+ 应用程序，那么编写与此处所示的坐标转换方法等效的方法对你来说可能很有用。

## 响应用户输入

到目前为止，除了 CapeEditor 示例中的 File 菜单之外，本章中你所做的一切都是单向的：应用程序通过在屏幕上显示信息来与用户对话。当然几乎所有软件都是双向工作的：用户也可以与软件对话。你现在将把该功能添加到 CapeEditor。

让 GDI+ 应用程序响应用户输入实际上比编写向屏幕绘制的代码要简单得多。（第 39 章介绍如何处理用户输入。）本质上，你需要重写 Form 类中的方法，这些方法由相关事件处理程序调用，就像 OnPaint() 在引发 Paint 事件时被调用一样。

下表列出了当用户点击或移动鼠标时你可能想要重写的方法。

| 方法 | 何时调用 ... |
|---|---|
| OnClick(EventArgs e) | 鼠标被点击。 |
| OnDoubleClick(EventArgs e) | 鼠标被双击。 |
| OnMouseDown(MouseEventArgs e) | 左鼠标按钮被按下。 |
| OnMouseHover(MouseEventArgs e) | 鼠标在移动后停留在某处不动。 |
| OnMouseMove(MouseEventArgs e) | 鼠标被移动。 |
| OnMouseUp(MouseEventArgs e) | 左鼠标按钮被释放。 |

如果你想检测用户输入的任何文本，那么你可能想要重写下表中列出的方法。

打印或打印预览与显示到屏幕之间存在一些重要差异。打印机无法滚动；相反，它们会输出页面。因此，你需要确保找到一种合理的方式将文档分成页面并按请求绘制每个页面。在其他方面，这意味着要计算文档中有多少内容可以放入单页中，因此需要多少页以及文档的每个部分需要写入哪一页。

尽管存在这些复杂性，打印过程相当简单。在程序上，你需要经历的步骤大致如下：

- **打印** — 你实例化一个 PrintDocument 对象并调用其 Print() 方法。此方法触发 PrintPage 事件以打印第一页。PrintPage 接受一个 PrintPageEventArgs 参数，该参数提供有关纸张大小和设置的信息，以及用于绘图命令的 Graphics 对象。因此，你应该为此事件编写一个事件处理程序，并实现该处理程序以打印一页。此事件处理程序还应将 PrintPageEventArgs 的一个布尔属性 HasMorePages 设置为 true 或 false，以指示是否还有更多页面需要打印。PrintDocument.Print() 方法将反复引发 PrintPage 事件，直到它看到 HasMorePages 被设置为 false。
- **打印预览** — 在这种情况下，你实例化一个 PrintDocument 对象和一个 PrintPreviewDialog 对象。你将 PrintDocument 附加到 PrintPreviewDialog（使用属性 PrintPreviewDialog.Document），然后调用对话框的 ShowDialog() 方法。此方法以模态方式显示对话框，该对话框是一个标准的 Windows 打印预览窗体，并显示文档的页面。内部通过反复引发 PrintPage 事件直到 HasMorePages 属性为 false 来显示页面。无需为此编写单独的事件处理程序；你可以使用与打印每页时相同的事件处理程序，因为绘图代码在两种情况下应该是相同的。（毕竟，打印预览的内容应该与打印版本完全相同！）

## 实现打印和打印预览

现在该过程已大致概述，在本节中你将看到它在代码方面的实现。你可以从 www.wrox.com 下载代码作为 PrintingCapsEdit 项目；它由 CapsEditor 项目组成，并包含以下片段中显示的更改。

你首先使用 Visual Studio 2010 设计视图在 File 菜单中添加两个新项：Print 和 Print Preview。你还使用属性窗口将这些项命名为 menuFilePrint 和 menuFilePrintPreview，并将它们设置为在应用程序启动时被禁用（在打开文档之前无法打印任何内容！）。你通过向主窗体的 LoadFile() 方法添加以下代码来安排这些菜单项被启用，该方法负责将文件加载到 CapsEditor 应用程序中：

```
private void LoadFile(string FileName)
{
    StreamReader sr = new StreamReader(FileName);
    string nextLine;
    documentLines.Clear();
    nLines = 0;
    TextLineInformation nextLineInfo;
    while ( (nextLine = sr.ReadLine()) != null)
    {
        nextLineInfo = new TextLineInformation();
        nextLineInfo.Text = nextLine;
        documentLines.Add(nextLineInfo);
        ++nLines;
    }
    sr.Close();
}
```

```
if (nLines > 0)
{
    documentHasData = true;
    menuFilePrint.Enabled = true;
    menuFilePrintPreview.Enabled = true;
}
else
{
    documentHasData = false;
    menuFilePrint.Enabled = false;
    menuFilePrintPreview.Enabled = false;
}
CalculateLineWidths();
CalculateDocumentSize();
Text = standardTitle + " - " + FileName;
Invalidate();
}
```

code download Printing.sln

上述代码是添加到此方法中的新代码。接下来，你向 Form1 类添加一个成员字段：

```
public partial class Form1 : Form
{
    private int pagesPrinted = 0;
```

此字段将用于指示你当前正在打印的是哪一页。你将其设为成员字段，因为你需要在 PrintPage 事件处理程序的调用之间记住此信息。

接下来，你将找到处理 Print 或 Print Preview 菜单选项选择的事件处理程序：

```
private void menuFilePrintPreview_Click(object sender, System.EventArgs e)
{
    this.pagesPrinted = 0;
    PrintPreviewDialog ppd = new PrintPreviewDialog();
    PrintDocument pd = new PrintDocument();
    pd.PrintPage += this.pd_PrintPage;
    ppd.Document = pd;
    ppd.ShowDialog();
}
private void menuFilePrint_Click(object sender, System.EventArgs e)
{
    this.pagesPrinted = 0;
    PrintDocument pd = new PrintDocument();
    pd.PrintPage += new PrintPageEventHandler
        (this.pd_PrintPage);
    pd.Print();
}
```

code download Printing.sln

你已经看到了打印所涉及的步骤，并且可以看到这些事件处理程序只是实现了该过程。在这两种情况下，你都在实例化一个 PrintDocument 对象并将事件处理程序附加到其 PrintPage 事件。对于打印，你调用 PrintDocument.Print()，而对于打印预览，你将 PrintDocument 对象附加到 PrintPreviewDialog 并调用预览对话框对象的 ShowDialog() 方法。PrintPage 事件的实际工作在事件处理程序中完成。以下是此处理程序的示例：

```
private void pd_PrintPage(object sender, PrintPageEventArgs e)
{
    float yPos = 0;
    float leftMargin = e.MarginBounds.Left;
```
