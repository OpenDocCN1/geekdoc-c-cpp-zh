of blocking. This is especially useful for web applications and services that may need to handle many thousands of concurrent requests.

+   You shouldn't ConfigureAwait(false) if the code that runs after an await operator must execute on the original thread. In the example discussed earlier, adding ConfigureAwait(false) to each awaited operation will run in the likelihood that the continuations compiler generates run on separate threads. This includes the continuation that attempts to set the Text property for message, causing the display of the following message: *The application called an interface that was marshaled for a different thread.*

Click here to view code image

```
private async void slowMethod()
    await doFirstLongRunningOperation().ConfigureAwait(false);
    await doSecondLongRunningOperation().ConfigureAwait(false);
    await doThirdLongRunningOperation().ConfigureAwait(false);
    message.Text = "Processing Complete";
```

+   Careless use of asynchronous methods that return results and run on the user interface thread can generate deadlocks, causing the application to freeze. Consider the following example:

Click here to view code image

```
private async void myWeb()
    var data = generateResult();
    ...
    message.Text = $"result: {data.Result}";
```

```
private async Task<string> generateResult()
    string result;
    ...
    result = ...;
    return result;
```