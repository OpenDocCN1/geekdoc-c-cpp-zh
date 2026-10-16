```
return JsonConvert.DeserializeObject<T>(json);
}
```

Instead of using the generic HttpClientHelper class from the client code, a specialization is done with the BookChapterClient class. This class derives from HttpClientHelper passing a BookChapter for the generic parameter. This class also overrides the GetAllAsync method from the base class to have the returned chapters sorted by the chapter number (code file BookServiceClientApp/BookChapterClient.cs):

```
public class BookChapterClient: HttpClientHelper<BookChapter>
{
    public BookChapterClient(string baseAddress)
    : base(baseAddress) { }

    public override async Task<IEnumerable<BookChapter>>
GetAllAsync(
    string requestUri)
    {
        IEnumerable<BookChapter> chapters = await
base.GetAllAsync(requestUri);
        return chapters.OrderBy(c => c.Number);
    }
}
```

The BookChapter class contains the properties that are received with the JSON content (code file BookServiceClientApp/BookChapter.cs):

```
public class BookChapter
{
    public Guid Id { get; set; }
    public int Number { get; set; }
    public string Title { get; set; }
    public int Pages { get; set; }
}
```

The Main method of the client application invokes the different methods to show GET, POST, PUT, and DELETE requests (code file BookServiceClientApp/Program.cs):

```
static void Main()
{
    WriteLine("Client app, wait for service");
    ReadLine();
    ReadChaptersAsync().Wait();
    ReadChapterAsync().Wait();
    ReadNotExistingChapterAsync().Wait();
    ReadXmlAsync().Wait();
    AddChapterAsync().Wait();
    UpdateChapterAsync().Wait();
    RemoveChapterAsync().Wait();
    ReadLine();
}
```

The method ReadChaptersAsync invokes the GetAllAsync method from the BookChapterClient to retrieve all chapters and shows the titles of the chapters on the console (code file BookServiceClientApp/Program.cs):

```
private static async Task ReadChaptersAsync()
{
```