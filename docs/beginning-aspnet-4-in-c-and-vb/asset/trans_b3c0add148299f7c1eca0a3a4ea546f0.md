
```
Grid.SetRow(t3, i);
grid1.Children.Add(t3);
}

FixedPage.SetLeft(grid1, 100);
FixedPage.SetTop(grid1, 140);
return grid1;
}
```

运行应用程序以查看在图 37-13 中显示的创建的固定文档。

![](img/d7d2ffa0a76feaab821930e95daace93_1150_0.png)

图 37-13

## XPS 文档

使用 Microsoft Word 可以将文档保存为 PDF 或 XPS 文件。自 Word 2007 SP2 起，此功能已包含在 Microsoft Word 中。如果您拥有 Word 2007 但尚未安装 SP2，可以免费下载该插件。XPS 是 XML Paper Specification，是 WPF 的子集。Windows 包含 XPS 阅读器。

.NET 包含用于读取和写入 XPS 文档的类和接口，其命名空间为 `System.Windows.Xps`、`System.Windows.Xps.Packaging` 和 `System.IO.Packaging`。

XPS 封装在 ZIP 文件格式中，因此您可以通过将扩展名为 .xps 的文件重命名为 .zip 并打开归档文件来轻松分析 XPS 文档。

XPS 文件需要在压缩文档中具有特定的结构，该结构由 XML Paper Specifications 定义（您可以从 http://www.microsoft.com/whdc/xps/xpsspec.mspx 下载）。该结构基于 Open Packaging Convention（OPC），Word 文档（OOXML 或 Office Open XML）也是基于该规范。在此类文件中，您可以找到用于元数据、资源（如字体和图片）以及文档本身的不同文件夹。在 XPS 文档的文档文件夹中，您可以找到代表 XPS XAML 子集的 XAML 代码。

要创建 XPS 文档，请使用命名空间 System.Windows.Xps.Packaging 中的 XpsDocument 类。要使用此类，还需要引用 ReachFramework 程序集。使用此类，您可以向文档添加缩略图（AddThumbnail()）和固定文档序列（AddFixedDocumentSequence()），以及对文档进行数字签名。固定文档序列是通过使用接口 IXpsFixedDocumentSequenceWriter 编写的，而该接口又使用 IXpsFixedDocumentWriter 在序列中写入文档。

如果 FixedDocument 已存在，则有更简便的方法来写入 XPS 文档。无需添加每个资源和每个文档页面，您可以使用命名空间 System.Windows.Xps 中的 XpsDocumentWriter 类。对于此类，必须引用 System.Printing 程序集。

以下代码片段展示了创建 XPS 文档的处理程序。首先，为菜单计划创建一个文件名，该文件名除了名称 menuplan 外还使用周数。周数借助 GregorianCalendar 类计算。然后打开 SaveFileDialog，让用户覆盖创建的文件名并选择文件应存储的目录。SaveFileDialog 类定义在命名空间 Microsoft.Win32 中，并封装了原生文件对话框。然后创建一个新的 XpsDocument，将文件名传递给构造函数。请记住，XPS 文件使用 ZIP 格式压缩内容。您可以使用 CompressionOption 指定压缩应优化时间还是空间。

接下来，使用静态方法 XpsDocument.CreateXpsDocumentWriter() 创建 XpsDocumentWriter。XpsDocumentWriter 的 Write 方法被重载，可接受不同的内容或内容部分来写入文档。使用 Write() 方法的可接受选项示例包括 FixedDocumentSequence、FixedDocument、FixedPage、string 和 DocumentPaginator。在示例代码中，仅传递了之前创建的 fixedDocument：

```csharp
private void OnCreateXps(object sender, RoutedEventArgs e)
{
    var c = new GregorianCalendar();
    int weekNumber = c.GetWeekOfYear(menu[0].Day,
        CalendarWeekRule.FirstFourDayWeek, DayOfWeek.Monday);
    string fileName = String.Format("menuplan{0}", weekNumber);

    var dlg = new SaveFileDialog
    {
        FileName = fileName,
        DefaultExt = ".xps",
        Filter = "XPS Documents|*.xps|All Files|*.*",
        AddExtension = true
    };

    if (dlg.ShowDialog() == true)
    {
        XpsDocument doc = new XpsDocument(dlg.FileName, FileAccess.Write,
            CompressionOption.Fast);
        XpsDocumentWriter writer = XpsDocument.CreateXpsDocumentWriter(doc);
        writer.Write(fixedDocument);
        doc.Close();
    }
}
```

代码片段 CreateXps/DocumentPage.xaml.cs

通过运行应用程序存储 XPS 文档，您可以使用 XPS 查看器查看文档，如图 37-14 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1152_0.png)

图 37-14

也可以向 XpsDocumentWriter 的 Write() 方法的一个重载传递 Visual，Visual 是 UIElement 的基类，因此您可以将任何 UIElement 传递给写入器以轻松创建 XPS 文档。此功能将在以下打印示例中使用。

## 打印

使用 DocumentViewer 在屏幕上显示的 FixedDocument 进行打印的最简单方法是调用与文档关联的 DocumentViewer 的 Print() 方法。在菜单规划应用程序的 OnPrint() 处理程序中，仅此操作即可完成。DocumentViewer 的 Print() 方法打开 PrintDialog 并将关联的 FixedDocument 发送到所选打印机：

```
private void OnPrint(object sender, RoutedEventArgs e)
{
    viewer.Print();
}
```

代码片段 CreateXps/DocumentPage.xaml.cs

### 使用 PrintDialog 打印

如果您想要对打印过程有更多控制，可以实例化 PrintDialog，并使用 PrintDocument() 方法打印文档。PrintDocument() 方法需要第一个参数为 DocumentPaginator。FixedDocument 使用 DocumentPaginator 属性返回 DocumentPaginator 对象。第二个参数定义在当前打印机和打印作业的打印机对话框中显示的字符串：

```
var dlg = new PrintDialog();
if (dlg.ShowDialog() == true)
{
    dlg.PrintDocument(fixedDocument.DocumentPaginator, "Menu Plan");
}
```

代码片段 CreateXps/DocumentPage.xaml.cs

### 打印 Visual

创建 UIElement 对象也很简单。以下 XAML 代码定义了一个 Ellipse、一个 Rectangle 和一个 Button，后者通过两个 Ellipse 元素进行视觉表示。Button 中有一个 Click 处理程序 OnPrint()，它启动视觉元素的打印作业：

```
<Canvas x:Name="canvas">
<Ellipse Canvas.Left="10" Canvas.Top="20" Width="180" Height="60"
Stroke="Red" StrokeThickness="3" >
<Ellipse.Fill>
<RadialGradientBrush>
<GradientStop Offset="0" Color="LightBlue" />
<GradientStop Offset="1" Color="DarkBlue" />
</RadialGradientBrush>
</Ellipse.Fill>
</Ellipse>
<Rectangle Width="180" Height="90" Canvas.Left="50" Canvas.Top="50">
<Rectangle.LayoutTransform>
<RotateTransform Angle="30" />
</Rectangle.LayoutTransform>
<Rectangle.Fill>
<LinearGradientBrush>
<GradientStop Offset="0" Color="Aquamarine" />
<GradientStop Offset="1" Color="ForestGreen" />
</LinearGradientBrush>
</Rectangle.Fill>
<Rectangle.Stroke>
<LinearGradientBrush>
<GradientStop Offset="0" Color="LawnGreen" />
<GradientStop Offset="1" Color="SeaGreen" />
</LinearGradientBrush>
</Rectangle.Stroke>
</Rectangle>
<Button Canvas.Left="90" Canvas.Top="190" Content="Print" Click="OnPrint">
<Button.Template>
<ControlTemplate TargetType="Button">
<Grid>
<Grid.RowDefinitions>
<RowDefinition />
<RowDefinition />
</Grid.RowDefinitions>
<Ellipse Grid.Row="0" Grid.RowSpan="2" Width="60"
Height="40" Fill="Yellow" />
<Ellipse Grid.Row="0" Width="52" Height="20"
HorizontalAlignment="Center">
<Ellipse.Fill>
<LinearGradientBrush StartPoint="0.5,0.0"
EndPoint="0.5,1">
<GradientStop Color="White" Offset="0" />
<GradientStop Color="Transparent"
Offset="0.9" />
</LinearGradientBrush>
</Ellipse.Fill>
</Ellipse>
<ContentPresenter Grid.Row="0" Grid.RowSpan="2"
HorizontalAlignment="Center"
VerticalAlignment="Center" />
</Grid>
</ControlTemplate>
</Button.Template>
</Button>
</Canvas>
```

代码片段 PrintingDemo/MainWindow.xaml

在 OnPrint() 处理程序中，可以通过调用 PrintDialog 的 PrintVisual() 方法启动打印作业。PrintVisual() 接受派生自基类 Visual 的任何对象：

```
private void OnPrint(object sender, RoutedEventArgs e)
{
    PrintDialog dlg = new PrintDialog();
    if (dlg.ShowDialog() == true)
    {
        dlg.PrintVisual(canvas, "Print Demo");
    }
}
```

代码片段 PrintingDemo/MainWindow.xaml.cs

对于无需用户干预的程序化打印，可以使用命名空间 System.Printing 中的 PrintDialog 类来创建打印作业并调整打印设置。LocalPrintServer 类提供有关打印队列的信息，并使用 DefaultPrintQueue 属性返回默认的 PrintQueue。您可以使用 PrintTicket 配置打印作业。PrintQueue.DefaultPrintTicket 返回与队列关联的默认 PrintTicket。PrintQueue 方法 GetPrintCapabilities() 返回打印机的功能，并且根据功能，您可以按以下代码段所示配置 PrintTicket。在完成打印票据的配置后，静态方法 PrintQueue.CreateXpsDocumentWriter() 返回 XpsDocumentWriter 对象。XpsDocumentWriter 类之前已用于创建 XPS 文档。您也可以使用它来启动打印作业。XpsDocumentWriter 的 Write() 方法不仅接受第一个参数为 Visual 或 FixedDocument，还接受第二个参数为 PrintTicket。如果使用第二个参数传递 PrintTicket，则写入器的目标是与票据关联的打印机，因此写入器将打印作业发送到打印机。

```
LocalPrintServer printServer = new LocalPrintServer();

PrintQueue queue = printServer.DefaultPrintQueue;

PrintTicket ticket = queue.DefaultPrintTicket;
PrintCapabilities capabilities = queue.GetPrintCapabilities(ticket);
if (capabilities.DuplexingCapability.Contains(
    Duplexing.TwoSidedLongEdge))
    ticket.Duplexing = Duplexing.TwoSidedLongEdge;
if (capabilities.InputBinCapability.Contains(InputBin.AutoSelect))
    ticket.InputBin = InputBin.AutoSelect;
if (capabilities.MaxCopyCount > 3)
    ticket.CopyCount = 3;
if (capabilities.PageOrientationCapability.Contains(
    PageOrientation.Landscape))
    ticket.PageOrientation = PageOrientation.Landscape;
if (capabilities.PagesPerSheetCapability.Contains(2))
    ticket.PagesPerSheet = 2;
if (capabilities.StaplingCapability.Contains(
    Stapling.StapleBottomLeft())
    ticket.Stapling = Stapling.StapleBottomLeft;
XpsDocumentWriter writer = PrintQueue.CreateXpsDocumentWriter(queue);
writer.Write(canvas, ticket);
```
