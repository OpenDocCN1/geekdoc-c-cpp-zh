To convert a list of Book objects to HTML, the extension method ToHtml returns an HTML table with the help of LINQ to XML (code file SharingSource\Utilities\BooksExtensions.cs):

```
public static class BookExtensions
{
    public static string ToHtml(this IEnumerable<Book> books) =>
        new XElement("table",
            new XElement("thead",
                new XElement("tr",
                    new XElement("td","Title"),
                    new XElement("td","Publisher"))),
            books.Select(b =>
                new XElement("tr",
                    new XElement("td", b.Title),
                    new XElement("td", b.Publisher))).ToString();
}
```

> NOTE LINQ to XML is covered in Chapter 27.

With the MainPage, you define a Button, where the user can initiate the sharing, and a TextBox control for the user to enter textual data to share (code file SharingSource\MainPage.xaml):

```
<RelativePanel Margin="24">
    <Button x:Name="shareDataButton" Content="Share Data"
        Click="{x:Bind DataSharing.ShowShareUI, Mode=OneTime}"
    Margin="12" />
    <TextBox RelativePanel.RightOf="shareDataButton"
        Text="{x:Bind DataSharing.SimpleText, Mode=TwoWay}"
    Margin="12" />
</RelativePanel>
```

In the code-behind file, the DataSharing property returns the ShareDataViewModel where all the important features for sharing are implemented (code file SharingSource\MainPage.xaml.cs):

```
public ShareDataViewModel DataSharing { get; set; } = new ShareDataViewModel();
```

The ShareDataViewModel defines the property SimpleText that is bound by the XAML file to enter the simple text to be shared. For sharing, the event handler method ShareDataRequested is assigned to the event DataRequested of the DataTransferManager. This event is fired when the user requests sharing data (code file SharingSource\ViewModels\ShareDataViewModel.cs):

```
public class ShareDataViewModel
{
    public ShareDataViewModel()
    {
        DataTransferManager.GetForCurrentView().DataRequested +=
            ShareDataRequested;
    }

    public string SimpleText { get; set; } = string.Empty;
```