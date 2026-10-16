
```csharp
public IEnumerable<object> Readers => GetReaders();

private List<object> _documentReaders = null;
private IEnumerable<object> GetReaders()
{
    return _documentReaders ??
    (
        _documentReaders =

        LogicalTreeHelper.GetChildren(grid1).OfType<FrameworkElement>()
            .Where(el => el.GetType().GetProperties()
                .Where(pi => pi.Name == "Document").Count() > 0)
            .Select(el => new
            {
                Name = el.GetType().Name,
                Instance = el
            }).Cast<object>().ToList();
    }
}
```

> **NOTE** *The coalescing operator (`??`) used with the `GetReaders` method is explained in detail in Chapter 8, "Operators and Casts."*

> **NOTE** *The sample code makes use of the `dynamic` keyword—the variable `activeDocumentReader` is declared as `dynamic` type. The `dynamic` keyword is used because the `SelectedItem` from the ComboBox returns either a `FlowDocumentReader`, a `FlowDocumentScrollViewer`, a `FlowDocumentPageViewer`, or a `RichTextBox`. All these types are flow document readers that offer a `Document` property of type `FlowDocument`. However, there’s no common base class or interface defining this property. The `dynamic` keyword allows accessing these different types from the same variable and using the `Document` property. The `dynamic` keyword is explained in detail in Chapter 16, “Reflection, Metadata, and Dynamic Programming.”*

When the user selects a flow document reader, the method `OnReaderSelectionChanged` is invoked. The XAML code that references this method was shown earlier. Within this method the previously selected flow document reader is made invisible by setting it to collapsed, and the variable `activeDocumentReader` is set to the selected reader:

```csharp
private void OnReaderSelectionChanged(object sender,
                                      SelectionChangedEventArgs
                                      e)
{
    dynamic item = (sender as ComboBox).SelectedItem;
    if (_activedocumentReader != null)
    {
        _activedocumentReader.Visibility = Visibility.Collapsed;
    }
    _activedocumentReader = item.Instance;
}
```

```
}

private dynamic _activedocumentReader = null;
```

When the user clicks the button to open a document, the method `OnOpenDocument` is invoked. With this method the `XamlReader` class is used to load the selected XAML file. If the reader returns a `FlowDocument` (which is the case when the root element of the XAML is the `FlowDocument` element), the `Document` property of the `activeDocumentReader` is assigned, and the `Visibility` is set to visible:

```csharp
private void OnOpenDocument(object sender, RoutedEventArgs e)
{
    try
    {
        var dlg = new OpenFileDialog();
        dlg.DefaultExt ="*.xaml";
        dlg.InitialDirectory = Environment.CurrentDirectory;
        if (dlg.ShowDialog() == true)
        {
            using (FileStream xamlFile = File.OpenRead(dlg.FileName))
            {
                var doc = XamlReader.Load(xamlFile) as FlowDocument;
                if (doc != null)
                {
                    _activedocumentReader.Document = doc;
                    _activedocumentReader.Visibility = Visibility.Visible;
                }
            }
        }
    }
    catch (XamlParseException ex)
    {
        MessageBox.Show($"Check content for a Flow document:
{ex.Message}");
    }
}
```

The running application is shown in Figure 35.11. This figure shows a flow document with the `FlowDocumentReader` in `TwoPage` mode.

![](img/3d365b72b289213a91ade7eb366b8f35_1398_0.png)

## Figure 35.11

## Fixed Documents

*Fixed documents* always define the same look, the same pagination, and the same fonts—no matter where the document is copied or used. WPF defines the class `FixedDocument` to create fixed documents, and the class `DocumentViewer` to view fixed documents.

This section uses a sample application to create a fixed document programmatically by requesting user input for a menu plan. The data for the menu plan is the content of the fixed document. Figure 35.12 shows the main user interface of this application, where the user can select a day with the `DatePicker` class, enter menus for a week in a `DataGrid`, and click the Create Doc button to create a new `FixedDocument`. This application uses `Page` objects that are navigated within a `NavigationWindow`. Clicking the Create Doc button navigates to a new page that contains the fixed document.

![](img/3d365b72b289213a91ade7eb366b8f35_1398_1.png)

## Figure 35.12

The event handler for the Create Doc button, OnCreateDoc, navigates to a new page. To do this, the handler instantiates the new page: DocumentPage. This page includes a handler —NavigationService_LoadCompleted—that is assigned to the LoadCompleted event of the NavigationService. Within this handler the new page can access the content that is passed to the page. Then the navigation is done by invoking the Navigate method to page2. The new page receives the object menus that contains all the menu information needed to build the fixed page. _menus is a readonly variable of type ObservableCollection<MenuEntry> (code file CreateXps/CreateXps/MenuPlannerPage.xaml.cs):

```csharp
private void OnCreateDoc(object sender, RoutedEventArgs e)
{
    if (_menus.Count == 0)
    {
        MessageBox.Show("Select a date first","Menu Planner", MessageBoxButton.OK);
        return;
    }

    var page2 = new DocumentPage();
    NavigationService.LoadCompleted += page2.NavigationService_LoadCompleted;
    NavigationService.Navigate(page2, _menus);
}
```

Within the DocumentPage, a DocumentViewer is used to provide read access to the fixed document. The fixed document is created in the method NavigationService_LoadCompleted. With the event handler, the data that is passed from the first page is received with the ExtraData property of NavigationEventArgs.

The received ObservableCollection<MenuEntry> is assigned to a menus variable that is used to build the fixed page (code file CreateXps/CreateXps/MenuDocumentPage.xaml.cs):

```csharp
internal void NavigationService_LoadCompleted(object sender, NavigationEventArgs e)
{
    _menus = e.ExtraData as ObservableCollection<MenuEntry>;

    _fixedDocument = new FixedDocument();
    var pageContent1 = new PageContent();
    _fixedDocument.Pages.Add(pageContent1);
    var page1 = new FixedPage();
    pageContent1.Child = page1;
    page1.Children.Add(GetHeaderContent());
    page1.Children.Add(GetLogoContent());
    page1.Children.Add(GetDateContent());
    page1.Children.Add(GetMenuContent());

    viewer.Document = _fixedDocument;

    NavigationService.LoadCompleted -= NavigationService_LoadCompleted;
}
```

Fixed documents are created with the FixedDocument class. The

`FixedDocument` element only contains `PageContent` elements that are accessible via the `Pages` property. The `PageContent` elements must be added to the document in the order in which they should appear on the page. `PageContent` defines the content of a single page.

`PageContent` has a `Child` property such that a `FixedPage` can be associated with it. To the `FixedPage` you can add elements of type `UIElement` to the `Children` collection. This is where you can add all the elements you’ve learned about in the last two chapters, including a `TextBlock` element that itself can contain `Inline` and `Block` elements.

In the sample code, the children to the `FixedPage` are created with helper methods `GetHeaderContent`, `GetLogoContent`, `GetDateContent`, and `GetMenuContent`.

The method `GetHeaderContent` creates a `TextBlock` that is returned. The `TextBlock` has the `Inline` element `Bold` added, which in turn has the `Run` element added. The `Run` element then contains the header text for the document. With `FixedPage.SetLeft` and `FixedPage.SetTop` the position of the `TextBox` within the fixed page is defined:

```csharp
private static UIElement GetHeaderContent()
{
    var text1 = new TextBlock
    {
        FontFamily = new FontFamily("Segoe UI"),
        FontSize = 34,
        HorizontalAlignment = HorizontalAlignment.Center
    };
    text1.Inlines.Add(new Bold(new Run("cn|elements")));
    FixedPage.SetLeft(text1, 170);
    FixedPage.SetTop(text1, 40);
    return text1;
}
```

The method `GetLogoContent` adds a logo in the form of an `Ellipse` with a `RadialGradientBrush` to the fixed document:

```csharp
private static UIElement GetLogoContent()
{
    var ellipse = new Ellipse
    {
        Width = 90,
        Height = 40,
        Fill = new RadialGradientBrush(Colors.Yellow,
Colors.DarkRed)
    };
    FixedPage.SetLeft(ellipse, 500);
    FixedPage.SetTop(ellipse, 50);
    return ellipse;
}
```

The method `GetDateContent` accesses the `menus` collection to add a date range to the document:

```csharp
private UIElement GetDateContent()
{
    string dateString = $"{menus[0].Day:d} to {menus[menus.Count - 1].Day:d}";
    var text1 = new TextBlock
```
