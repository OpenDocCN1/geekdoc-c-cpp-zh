# Chapter 73: C# 5.0 Features

| Method/Modifier with Parameter | Details |
|---|---|
| Type<T> | T is the return type |

# Section 73.1: Async & Await

async and await are two operators that are intended to improve performance by freeing up Threads and waiting for operations to complete before moving forward.

Here's an example of getting a string before returning it's length:

```
```csharp
//This method is async because:
//1. It has async and Task or Task<T> as modifiers
//2. It ends in "Async"
async Task<int> GetStringLengthAsync(string URL){
    HttpClient client = new HttpClient();
    //Sends a GET request and returns the response body as a string
    Task<string> getString = client.GetStringAsync(URL);
    //Waits for getString to complete before returning its length
    string contents = await getString;
    return contents.Length;
}
```
```

```
```csharp
private async void doProcess(){
    int length = await GetStringLengthAsync("http://example.com/");
    //Waits for all the above to finish before printing the number
    Console.WriteLine(length);
}
```
```

Here's another example of downloading a file and handling what happens when it's progress has changed and when the download completes (there are two ways to do this):

Method 1:

```
```csharp
//This one using async event handlers, but not async coupled with await
private void DownloadAndUpdateAsync(string url, string DownloadLocation){
    WebClient web = new WebClient();
    //Assign the event handler
    web.DownloadProgressChanged += new DownloadProgressChangedEventHandler(ProgressChanged);
    web.DownloadFileCompleted += new AsyncCompletedEventHandler(FileCompleted);
    //Download the file asynchronously
    web.DownloadFileAsync(new Uri(url), DownloadLocation);
}
```
```

```
```csharp
//event called for when download progress has changed
private void ProgressChanged(object sender, DownloadProgressChangedEventArgs e){
    //example code
    int i = 0;
    i++;
    doSomething();
}
```
```

```
```csharp
//event called for when download has finished
private void FileCompleted(object sender, AsyncCompletedEventArgs e){
    Console.WriteLine("Completed!")
}
```
```