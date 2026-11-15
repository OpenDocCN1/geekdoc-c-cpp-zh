```
state.ResetEvent.Wait();
}

// Retrieve the results when finished downloading
private static void GetResponseAsyncCompleted(
    IAsyncResult asyncResult)
{
    State completedState =
        (WebRequestState)asyncResult.AsyncState;
    HttpWebResponse response =
        (HttpWebResponse)completedState.WebRequest
        .EndGetResponse(asyncResult);

    Stream stream = response.GetResponseStream();
    StreamReader reader = new StreamReader(stream);
    int length = reader.ReadToEnd().Length;

    Console.WriteLine(FormatBytes(length));
    completedState.ResetEvent.Set();
    completedState.Dispose();
}

// ...
```

```
class WebRequestState : IDisposable
{
    public WebRequestState(WebRequest webRequest)
    {
        WebRequest = webRequest;
    }

    public WebRequest WebRequest { get; private set; }

    private ManualResetEventSlim _ResetEvent =
        new ManualResetEventSlim();

    public ManualResetEventSlim ResetEvent
    {
        get { return _ResetEvent; }
    }

    public void Dispose()
    {
        ResetEvent.Dispose();
        GC.SuppressFinalize(this);
    }
}
```

Notice that in Listing 19.15, we pass data for both of the parameters on BeginGetResponse(). The first parameter is a delegate of type System.AsyncCallback that takes a single parameter of type System.AsyncResult. The AsyncCallback identifies the code that will execute once the