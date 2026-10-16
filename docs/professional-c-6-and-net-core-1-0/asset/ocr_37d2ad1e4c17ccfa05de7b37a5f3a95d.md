method. GetBooksAsync creates a ValueSet with the GET command that is sent to the app service with the helper method SendMessageAsync. This helper method returns a JSON string, which in turn is converted to a Book collection that is used to fill the ObservableCollection for the Books property (code file AppServices/BooksCacheClient/ViewModels/BooksViewModel.cs):

```
public class BooksViewModel
{
    private const string BookServiceName
="com.CNinnovation.BooksCache";
    private const string BooksPackageName =
        "CNinnovation.Samples.BookCache_p2wxv0ry6mv8g";

    public ObservableCollection<Book> Books { get; } =
        new ObservableCollection<Book>();

    public async void GetBooksAsync()
    {
        var message = new ValueSet();
        message.Add("command","GET");
        string json = await SendMessageAsync(message);
        IEnumerable<Book> books = json.ToBooks();
        foreach (var book in books)
        {
            Books.Add(book);
        }
    }
}
```

The method PostBookAsync creates a Book object, serializes it to JSON, and sends it via a ValueSet to the SendMessageAsync method:

```
public string NewBookTitle { get; set; }
    public string NewBookPublisher { get; set; }

    public async void PostBookAsync()
    {
        var message = new ValueSet();
        message.Add("command","POST");
        string json = new Book
        {
            Title = NewBookTitle,
            Publisher = NewBookPublisher
        }.ToJson();
        message.Add("book", json);
        string result = await SendMessageAsync(message);
    }
```

The app service–relevant client code is contained within the method SendMessageAsync. Here, an AppServiceConnection is created. The connection is closed after use by disposing it with the using statement. To map the connection to the correct service, the AppServiceName and PackageFamilyName properties need to be supplied. After setting these properties, the connection is opened by invoking the method OpenAsync. Only when the connection is opened successfully is a request sent with the ValueSet received from the calling method. The AppServiceConnection method SendMessageAsync makes the request to the service and returns an AppServiceResponse object. The response contains the result from the service, which is dealt with accordingly: