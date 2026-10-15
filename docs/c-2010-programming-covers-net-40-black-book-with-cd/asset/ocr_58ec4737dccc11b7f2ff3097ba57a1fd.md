```
}
    docViewer.Document = _xpsDocument.GetFixedDocumentSequence();
    _fileName = dlg.FileName;
}
}
private void CloseCommandHandler(object sender, ExecutedRoutedEventArgs e)
{
    this.Close();
}
private void AddCommandBindings(ICommand command, ExecutedRoutedEventHandler handler)
{
    CommandBinding cmdBindings = new CommandBinding(command);
    cmdBindings.Executed += handler;
    CommandBindings.Add(cmdBindings);
}
private XpsDocument _xpsDocument;
private string _fileName;
}
```

+   5. Press the F5 key to run the application. A blank window appears with the File menu.
+   6. Select File→Open from the main menu. This opens the Open dialog box from which you can browse to the location of the XPS document you saved on the computer.
+   7. Select the file and click the Open button. The XPS document opens in MainWindow, as shown in Figure 11.10:

![](bbox=[0.27, 0.445, 0.7, 0.605])

# Creating Flow Documents

In the In Depth section of this chapter, you have learned about Flow documents in detail. You have also learned about the various Flow content elements that help in preparing the structure of a Flow document, such as the Block and Inline elements. In WPF, you can create a Flow document by using any of the three Flow document controls: FlowDocumentReader, FlowDocumentPageViewer, or FlowDocumentScrollViewer. All these controls create a Flow document with different functionalities.

Let's create a WPF application named FlowDocument (also available on the CD-ROM) to learn how to create a simple Flow document. Add the code given in Listing 11.12 to MainWindow.xaml of FlowDocument:

Listing 11.12: Showing the Code to Create a Simple Flow Document

```
<Window x:Class="FlowDocument.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="240" Width="300">
<Grid>
<FlowDocumentReader>
<FlowDocument FontSize="13">
<Paragraph>This is the first paragraph.
```