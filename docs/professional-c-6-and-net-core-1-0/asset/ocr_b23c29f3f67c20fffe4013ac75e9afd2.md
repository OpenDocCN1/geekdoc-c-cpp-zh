![](bbox=[0.105, 0.062, 0.894, 0.308])

# Figure 35.14

To one overload of the Write method of the XpsDocumentWriter you can also pass a Visual, which is the base class of UIElement, and thus you can pass any UIElement to the writer to create an XPS document easily. This functionality is used in the following printing example.

# Printing

The simplest way to print a FixedDocument that is shown onscreen with the DocumentViewer is to invoke the Print method of the DocumentViewer with which the document is associated. This is all that needs to be done with the menu planner application in an OnPrint handler. The Print method of the DocumentViewer opens the PrintDialog and sends the associated FixedDocument to the selected printer (code file CreateXps/CerateXpsDocumentPage.xaml.cs):

```
private void OnPrint(object sender, RoutedEventArgs e)
{
    viewer.Print();
}
```

# Printing with the PrintDialog

If you want more control over the printing process, the PrintDialog can be instantiated, and the document printed with the PrintDocument method. The PrintDocument method requires a DocumentPaginator with the first argument. The FixedDocument returns a DocumentPaginator object with the DocumentPaginator property. The second argument defines the string that appears with the current printer and in the printer dialogs for the print job:

```
var dlg = new PrintDialog();
if (dlg.ShowDialog() == true)
{
    dlg.PrintDocument(fixedDocument.DocumentPaginator,"Menu Plan");
}
```