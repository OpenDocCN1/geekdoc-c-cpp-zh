```
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