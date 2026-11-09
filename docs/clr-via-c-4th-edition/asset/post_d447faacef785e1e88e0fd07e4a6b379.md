
work is being performed on behalf of the original client request, the culture and identity needs to “flow” to the new thread pool thread so any additional work done on behalf of the client is performed using the client’s culture and identity information.

Fortunately, the FCL defines a base class, called `System.Threading.SynchronizationContext`, which solves all these problems. Simply stated, a `SynchronizationContext`-derived object connects an application model to its threading model. The FCL defines several classes derived from `SynchronizationContext`, but usually you will not deal directly with these classes; in fact, many of them are not publicly exposed or documented.

For the most part, application developers do not need to know anything about the `SynchronizationContext` class. When you await a `Task`, the calling thread’s `SynchronizationContext` object is obtained. When a thread pool thread completes the `Task`, the `SynchronizationContext` object is used, ensuring the right threading model for your application model. So, when a GUI thread awaits a `Task`, the code following the await operator is guaranteed to execute on the GUI thread as well, allowing that code to update UI elements.<sup>12</sup> For an ASP.NET application, the code following the await operator is guaranteed to execute on a thread pool thread that has the client’s culture and principal information associated with it.

12 Internally, the various `SynchronizationContext`-derived classes get the GUI thread to resume the state machine using methods like `System.Windows.Forms.Control.BeginInvoke`, `System.Windows.Threading.Dispatcher.BeginInvoke`, and `Windows.UI.Core.CoreDispatcher.RunAsync`.

Most of the time, having a state machine resume using the application model’s threading model is phenomenally useful and convenient. But, on some occasions, this can get you into trouble. Here is an example that causes a WPF application to deadlock.

```csharp
private sealed class MyWpfWindow : Window {
    public MyWpfWindow() { Title = "WPF Window"; }

    protected override void OnActivated(EventArgs e) {
        // Querying the Result property prevents the GUI thread from returning;
        // the thread blocks waiting for the result
        String http = GetHttp().Result; // Get the string synchronously!

        base.OnActivated(e);
    }

    private async Task<String> GetHttp() {
        // Issue the HTTP request and let the thread return from GetHttp
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // We never get here: The GUI thread is waiting for this method to finish but this method
        // can't finish because the GUI thread is waiting for it to finish --> DEADLOCK!

        return await msg.Content.ReadAsStringAsync();
    }
}
```

Developers creating class libraries definitely need to be aware of the `SynchronizationContext` class so they can write high-performance code that works with all application models. Because a lot of class library code is application model agnostic, we want to avoid the additional overhead involved in using a `SynchronizationContext` object. In addition, class library developers should do everything in their power to help application developers avoid deadlock situations. To solve both of these problems, both the `Task` and `Task<TResult>` classes offer a method called `ConfigureAwait` whose signature looks like this.

```csharp
// Task defines this method:
public ConfiguredTaskAwaitable ConfigureAwait(Boolean continueOnCapturedContext);

// Task<TResult> defines this method:
public ConfiguredTaskAwaitable<TResult> ConfigureAwait(Boolean continueOnCapturedContext);
```

Passing true to this method gives you the same behavior as not calling the method at all. But, if you pass false, the await operator does not query the calling thread’s `SynchronizationContext` object and, when a thread pool thread completes the `Task`, it simply completes it and the code after the await operator executes via the thread pool thread.

Even though my `GetHttp` method is not class library code, the deadlock problem goes away if I add calls to `ConfigureAwait`. Here is the modified version of my `GetHttp` method.

```csharp
private async Task<String> GetHttp() {
    // Issue the HTTP request and let the thread return from GetHttp
    HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/")
        .ConfigureAwait(false);
    // We DO get here now because a thread pool can execute this code
    // as opposed to forcing the GUI thread to execute it.

    return await msg.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

As the preceding code shows, `ConfigureAwait(false)` must be applied to every `Task` object you await. This is because asynchronous operations may complete synchronously and, when this happens, the calling thread simply continues executing without returning to its caller; you never know which operation requires ignoring the `SynchronizationContext` object, so you have to tell all of them to ignore it. This also means that your class library code should be application model agnostic.

Alternatively, I could re-write my `GetHttp` method as follows so that the whole thing executes via a thread pool thread.

```csharp
private Task<String> GetHttp() {
    return Task.Run(async () => {
        // We run on a thread pool thread now that has no SynchronizationContext on it
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // We DO get here because some thread pool can execute this code

        return await msg.Content.ReadAsStringAsync();
    });
}
```

In this version of the code, notice that my `GetHttp` method is not an async function; I removed the `async` keyword from the method signature, because the method no longer has an await operator in it. On the other hand, the lambda expression I pass to `Task.Run` is an async function.

## Implementing a Server Asynchronously

From talking to many developers over the years, I’ve discovered that very few of them are aware that the .NET Framework has built-in support allowing you to build asynchronous servers that scale really well. In this book, I can’t explain how to do this for every kind of server, but I can list what you should look for in the MSDN documentation.

- To build asynchronous ASP.NET Web Forms: in your .aspx file, add `Async="true"` to your page directive and look up the `System.Web.UI.Page`’s `RegisterAsyncTask` method.
- To build an asynchronous ASP.NET MVC controller: derive your controller class from `System.Web.Mvc.AsyncController` and simply have your action method return a `Task<ActionResult>`.
- To build an asynchronous ASP.NET handler: derive your class from `System.Web.HttpTaskAsyncHandler` and then override its abstract `ProcessRequestAsync` method.
- To build an asynchronous WCF service: implement your service as an async function and have it return `Task` or `Task<TResult>`.

### Canceling I/O Operations

In general, Windows doesn’t give you a way to cancel an outstanding I/O operation. This is a feature that many developers would like, but it is actually quite hard to implement. After all, if you make a request from a server and then you decide you don’t want the response anymore, there is no way to tell the server to abandon your original request. The way to deal with this is just to let the bytes come back to the client machine and then throw them away. In addition, there is a race condition here—your request to cancel the request could come just as the server is sending the response. Now what should your application do? You’d need to handle this potential race condition occurring in your own code and decide whether to throw the data away or act on it.

To assist with this, I recommend you implement a `WithCancellation` extension method that extends `Task<TResult>` (you need a similar overload that extends `Task` too) as follows.

```csharp
private struct Void { } // Because there isn't a non-generic TaskCompletionSource class.

private static async Task<TResult> WithCancellation<TResult>(this Task<TResult> originalTask,
    CancellationToken ct) {

    // Create a Task that completes when the CancellationToken is canceled
    var cancelTask = new TaskCompletionSource<Void>();

    // When the CancellationToken is canceled, complete the Task
    using (ct.Register(
        t => ((TaskCompletionSource<Void>)t).TrySetResult(new Void()), cancelTask)) {

        // Create a Task that completes when either the original or
        // CancellationToken Task completes
```
