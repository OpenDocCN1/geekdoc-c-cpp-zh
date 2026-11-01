
```
Grid.SetRow(t3, i);
grid1.Children.Add(t3);
}

FixedPage.SetLeft(grid1, 100);
FixedPage.SetTop(grid1, 140);
return grid1;
}
```

Run the application to see the created fixed document shown in Figure 37-13.

![](img/d7d2ffa0a76feaab821930e95daace93_1150_0.png)

FIGURE 37-13

## XPS DOCUMENTS

With Microsoft Word you can save a document as a PDF or XPS file. Since Word 2007 SP2 this feature is included with Microsoft Word. If you have Word 2007 but didn't install SP2 yet you can download the add-on for free. XPS is the XML Paper Specification, a subset of WPF. Windows includes an XPS reader.

.NET includes classes and interfaces to read and write XPS documents with the namespaces `System.Windows.Xps`, `System.Windows.Xps.Packaging`, and `System.IO.Packaging`.

XPS is packaged within the ZIP file format, so you can easily analyze an XPS document by renaming a file with an .xps extension to .zip and opening the archive.

An XPS file requires a specific structure in the zipped document that is defined by the XML Paper Specifications (which you can download from http://www.microsoft.com/whdc/xps/xpsspec.mspx). The structure is based on the Open Packaging Convention (OPC) that Word documents (OOXML or Office Open XML) are based on as well. Within such a file you can find different folders for metadata, resources (such as fonts and pictures), and the document itself. Within the document folder of an XPS document you can find the XAML code representing the XPS subset of XAML.

To create an XPS document, you use the XpsDocument class from the namespace System.Windows.Xps.Packaging. To use this class, you will need to reference the assembly ReachFramework as well. With this class you can add a thumbnail (AddThumbnail()) and fixed document sequences (AddFixedDocumentSequence()) to the document, as well as digitally sign the document. A fixed document sequence is written by using the interface IXpsFixedDocumentSequenceWriter that in turn uses an IXpsFixedDocumentWriter to write the document within the sequence.

If a FixedDocument already exists, there’s an easier way to write the XPS document. Instead of adding every resource and every document page, you can use the class XpsDocumentWriter from the namespace System.Windows.Xps. For this class the assembly System.Printing must be referenced.

With the following code snippet you can see the handler to create the XPS document. First, a filename for the menu plan is created that uses a week number in addition to the name menuplan. The week number is calculated with the help of the GregorianCalendar class. Then the SaveFileDialog is opened to let the user overwrite the created filename and select the directory where the file should be stored. The SaveFileDialog class is defined in the namespace Microsoft.Win32 and wraps the native file dialog. Then a new XpsDocument is created where the filename is passed to the constructor. Recall that the XPS file uses a ZIP format to compress the content. With the CompressionOption you can specify whether the compression should be optimized on time or space.

Next, an XpsDocumentWriter is created with the help of the static method XpsDocument.CreateXpsDocumentWriter(). The Write method of the XpsDocumentWriter is overloaded to accept different content or content parts to write the document. Examples of acceptable options with the Write() method are FixedDocumentSequence, FixedDocument, FixedPage, string, and a DocumentPaginator. In the sample code, only the fixedDocument that was created earlier is passed:

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

code snippet CreateXps/DocumentPage.xaml.cs

By running the application to store the XPS document, you can view the document with an XPS viewer, as shown in Figure 37-14.

![](img/d7d2ffa0a76feaab821930e95daace93_1152_0.png)

FIGURE 37-14

To one overload of the Write() method of the XpsDocumentWriter you can also pass a Visual, which is the base class of UIElement, and thus you can pass any UIElement to the writer to create an XPS document easily. This functionality will be used in the following printing example.

## PRINTING

The simplest way to print a FixedDocument that is shown on the screen with the DocumentViewer is to invoke the Print() method of the DocumentViewer that has the document associated. This is all that needs to be done with the menu planner application in an OnPrint() handler. The Print() method of the DocumentViewer opens up the PrintDialog and sends the associated FixedDocument to the selected printer:

```
private void OnPrint(object sender, RoutedEventArgs e)
{
    viewer.Print();
}
```

code snippet CreateXps/DocumentPage.xaml.cs

### Printing with the PrintDialog

If you want more control over the printing process, the PrintDialog can be instantiated, and the document printed with the PrintDocument() method. The PrintDocument() method requires a DocumentPaginator with the first argument. The FixedDocument returns a DocumentPaginator object with the DocumentPaginator property. The second argument defines the string that shows up with the current printer and in the printer dialogs for the print job:

```
var dlg = new PrintDialog();
if (dlg.ShowDialog() == true)
{
    dlg.PrintDocument(fixedDocument.DocumentPaginator, "Menu Plan");
}
```

code snippet CreateXps/DocumentPage.xaml.cs

### Printing Visuals

It's also simple to create UIElement objects. The following XAML code defines an Ellipse, a Rectangle, and a Button that is visually represented with two Ellipse elements. With the Button there's a Click handler OnPrint() that starts the print job of the visual elements:

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

code snippet PrintingDemo/MainWindow.xaml

In the OnPrint() handler the print job can be started by invoking the PrintVisual() method of the PrintDialog. PrintVisual() accepts any object that derives from the base class Visual:

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

code snippet PrintingDemo/MainWindow.xaml.cs

For programmatically printing without user intervention, the PrintDialog classes from the namespace System.Printing can be used to create a print job and adjust print settings. The class LocalPrintServer gives information about print queues and returns the default PrintQueue with the DefaultPrintQueue property. You can configure the print job with a PrintTicket. PrintQueue.DefaultPrintTicket returns a default PrintTicket that is associated with the queue. The PrintQueue method GetPrintCapabilities() returns the capabilities of a printer, and depending on the capabilities you can configure the PrintTicket as shown in the following code segment. After configuration of the print ticket is complete, the static method PrintQueue.CreateXpsDocumentWriter() returns an XpsDocumentWriter object. The XpsDocumentWriter class was previously used to create a XPS document. You can also use it to start a print job. The Write() method of the XpsDocumentWriter not only accepts a Visual or FixedDocument as the first argument but also a PrintTicket as the second argument. If a PrintTicket is passed with the second argument, the target of the writer is the printer that is associated with the ticket and thus the writer sends the print job to the printer.

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
