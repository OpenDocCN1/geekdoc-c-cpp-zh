```
```csharp
{
 var clientHandler = new HttpClientHandler
 {
  Credentials = req.Credentials
 }
};
 var client = new HttpClient(clientHandler);
 var response = await client.GetAsync(req.Url, cts.Token);
 string resp = await response.Content.ReadAsStringAsync();
 await Task.Run(() =>
 {
  IEnumerable<SearchItemResult> images = req.Parse(resp);
  foreach (var image in images)
  {
   _searchInfo.List.Add(image);
  }
 }
);
}
```

Because the method passed to the Task.Run method is running in a background thread, here we have the same problem as before referencing some UI code. One solution would be to just do req.Parse within the Task.Run method, and do the foreach loop outside the task to add the result to the list in the UI thread. WPF offers a better solution, however, that enables filling collections that are bound to the UI from a background thread. This extension only requires enabling the collection for synchronization using BindingOperations.EnableCollectionSynchronization, as shown in the following code snippet:

```
```csharp
public partial class MainWindow : Window
{
 private SearchInfo _searchInfo = new SearchInfo();
 private object _lockList = new object();

 public MainWindow()
 {
  InitializeComponent();
  this.DataContext = _searchInfo;
  BindingOperations.EnableCollectionSynchronization(
   _searchInfo.List, _lockList);
 }
}
```

Now that you’ve seen the advantages of the async and await keywords, the next section examines the programming foundation behind these keywords.

# Foundation of Asynchronous Programming

The async and await keywords are just a compiler feature. The compiler creates code by using the Task class. Instead of using the new keywords, you could get the same functionality with C# 4 and methods of the Task class; it’s just not as convenient.

This section gives information about what the compiler does with the async and await keywords. It shows you an easy way to create an asynchronous method and demonstrates how to invoke multiple