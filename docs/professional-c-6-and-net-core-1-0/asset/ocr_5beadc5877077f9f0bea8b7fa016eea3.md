A major functionality of the FlowDocument class is that it is used to break up the flow into multiple pages. This is done via the IDocumentPaginatorSource interface, which is implemented by FlowDocument.

Other options with a FlowDocument are to set up the default font and foreground and background brushes, and to configure the page and column sizes.

The following XAML code for the FlowDocument defines a default font and font size, a column width, and a ruler between columns:

```
<FlowDocument
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation'

    ColumnWidth="300" FontSize="16" FontFamily="Segoe UI"
    ColumnRuleWidth="3" ColumnRuleBrush="Violet">
```

Now you just need a way to view the documents. The following list describes several viewers:

+   - RichTextBox—A simple viewer that also allows editing (as long as the IsReadOnly property is not set to true). The RichTextBox doesn’t display the document with multiple columns but instead in scroll mode. This is similar to the Web layout in Microsoft Word. The scrollbar can be enabled by setting the HorizontalScrollbarVisibility to ScrollbarVisibility.Auto.

+   - FlowDocumentScrollViewer—A reader that is meant only to read but not edit documents. This reader enables zooming into the document. There’s also a toolbar with a slider for zooming that can be enabled with the property IsToolbarEnabled. Settings such as CanIncreaseZoom, CanDecreaseZoom, MinZoom, and MaxZoom enable setting the zoom features.

+   - FlowDocumentPageViewer—A viewer that paginates the document. With this viewer you not only have a toolbar to zoom into the document, you can also switch from page to page.

+   - FlowDocumentReader—A viewer that combines the functionality of FlowDocumentScrollViewer and FlowDocumentPageViewer. This viewer supports different viewing modes that can be set from the toolbar or with the property ViewingMode that is of type FlowDocumentReaderViewingMode. This enumeration has the possible values Page, TwoPage, and Scroll. You can also disable the viewing modes according to your needs.

The sample application to demonstrate flow documents defines several readers such that one reader can be chosen dynamically. Within the Grid element you can find the FlowDocumentReader, RichTextBox, FlowDocumentScrollViewer, and FlowDocumentPageViewer. With all the readers the Visibility property is set to Collapsed, so on startup none of the readers appear. The ComboBox that is the first child element within the grid enables the user to select the active reader. The