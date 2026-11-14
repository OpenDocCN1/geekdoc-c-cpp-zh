Let's dig a little deeper into this pattern to examine the methods used for starting and reporting the completion of each download. The finish-Download method is rather simple, and I'll show it only for completeness:

```
private static void finishDownload(string url, byte[] bytes)
{
    Console.WriteLine("Read {0} bytes from {1}",
        bytes.Length, url);
}
```

Start Download shows a bit more of the interface provided by the Parallel Task Library. The specific types used help to support the Task interface. I'd like to abstract that away, but handling these types will be a bit different for each specific task you want to accomplish. In fact, the Parallel Task Library puts a common interface on top of the many different async patterns that existed in the .NET BCL prior to this version.

```
private static Task<byte[]> startDownload(string url)
{
    var tcs = new TaskCompletionSource<byte[]>(url);
    var wc = new WebClient();
    wc.DownloadDataCompleted += (sender, e) =>
    {
        if (e.UserState == tcs)
        {
            if (e.Cancelled)
                tcs.TrySetCanceled();
            else if (e.Error != null)
                tcs.TrySetException(e.Error);
            else
                tcs.TrySetResult(e.Result);
        }
    };
    wc.DownloadDataAsync(new Uri(url), tcs);
    return tcs.Task;
}
```

This method has a mix of general Task code and code specific to downloading data from a URL, so let's go through it very carefully. First, it creates a TaskCompletionSource object for this task. A TaskCompletionSource object enables you to separate the creation of a task from its completion.