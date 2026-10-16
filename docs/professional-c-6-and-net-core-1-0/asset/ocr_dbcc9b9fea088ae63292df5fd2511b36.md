help of the HttpClient method PutAsync. PutAsync requires the updated content with the second parameter, and the URL to the service including the identifier in the first (code file BookServiceClientApp/HttpClientHelper.cs):

```
public async Task PutAsync(string uri, T item)
{
    using (var client = new HttpClient())
    {
        client.BaseAddress = _baseAddress;
        string json = JsonConvert.SerializeObject(item);
        HttpContent content = new StringContent(json, Encoding.UTF8, "application/json");
        HttpResponseMessage resp = await client.PutAsync(uri, content);
        WriteLine($"status from PUT {resp.StatusCode}");
        resp.EnsureSuccessStatusCode();
    }
}
```

In the Program class, the chapter Windows Store Apps is updated to a different chapter number and the title Windows Apps (code file BookServiceClientApp/Program.cs):

```
private static async Task UpdateChapterAsync()
{
    WriteLine(nameof(UpdateChapterAsync));
    var client = new BookChapterClient(Addresses.BaseAddress);
    var chapters = await client.GetAllAsync(Addresses.BooksApi);
    var chapter = chapters.SingleOrDefault(c => c.Title =="Windows Store Apps");
    if (chapter != null)
    {
        chapter.Number = 32;
        chapter.Title ="Windows Apps";
        await client.PutAsync(Addresses.BooksApi + chapter.Id, chapter);
        WriteLine($"updated chapter {chapter.Title}");
    }
    WriteLine();
}
```

The console output of the UpdateChapterAsync method shows an HTTP NoContent result and the updated chapter title:

```
UpdateChapterAsync
status from GET OK
status from PUT NoContent
updated chapter Windows Apps
```

# Sending DELETE Requests

The last request shown with the sample client is the HTTP DELETE request. After invoking GetAsync, PostAsync, and PutAsync of the HttpClient class, it should be obvious that the format is DeleteAsync. What’s shown in this code snippet is that the DeleteAsync method just needs a URI parameter to identify the object to delete (code file BookServiceClientApp/HttpClientHelper.cs):