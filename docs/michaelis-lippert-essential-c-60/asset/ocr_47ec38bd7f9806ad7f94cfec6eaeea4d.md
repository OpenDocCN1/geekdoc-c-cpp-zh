```
WebRequest webRequest =
    WebRequest.Create(url);

IAsyncResult asyncResult =
    webRequest.BeginGetResponse(null, null);

// Indicate busy using dots; ideally (at least in a non-Console
// implementation) should use a callback rather than a wait.
while (
    !asyncResult.AsyncWaitHandle.WaitOne(100))
{
    Console.Write('.');
}

// Retrieve the results when finished downloading.
WebResponse response =
    webRequest.EndGetResponse(asyncResult);
using (StreamReader reader =
    new StreamReader(response.GetResponseStream()))
{
    // Note: ReadToEnd() is blocking. A production implementation
    // should offload this to another thread.
    int length = reader.ReadToEnd().Length;
    Console.WriteLine(FormatBytes(length));
}

static public string FormatBytes(long bytes)
{
    string[] magnitudes =
        new string[] { "GB", "MB", "KB", "Bytes" };
    long max =
        (long)Math.Pow(1024, magnitudes.Length);

    return string.Format("{1:##.##} {0}",
        magnitudes.FirstOrDefault(
            magnitude =>
                bytes > (max /= 1024) )?? "0 Bytes",
        (decimal)bytes / (decimal)max).Trim();
}
```

The results of Listing C.1 appear in Output C.1.

# OUTPUT C.1

```
http://www.IntelliTect.com........29.36 KB
```

As mentioned, the key aspect of the APM pattern is the pair of BeginX and EndX methods with well-established signatures. The BeginX method returns a System.IAsyncResult object providing access to the state of the