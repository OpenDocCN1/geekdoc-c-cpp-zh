# # Implementing a Server Asynchronously

From talking to many developers over the years, I’ve discovered that very few of them are aware that the .NET Framework has built-in support allowing you to build asynchronous servers that scale really well. In this book, I can’t explain how to do this for every kind of server, but I can list what you should look for in the MSDN documentation.

+   - To build asynchronous ASP.NET Web Forms: in your .aspx file, add "Async=true" to your page directive and look up the System.Web.UI.Page’s RegisterAsyncTask method.
+   - To build an asynchronous ASP.NET MVC controller: derive your controller class from System.Web.Mvc.AsyncController and simply have your action method return a Task<ActionResult>.
+   - To build an asynchronous ASP.NET handler: derive your class from System.Web.HttpTaskAsyncHandler and then override its abstract ProcessRequestAsync method.
+   - To build an asynchronous WCF service: implement your service as an async function and have it return Task or Task<TResult>.

# ## Canceling I/O Operations

In general, Windows doesn’t give you a way to cancel an outstanding I/O operation. This is a feature that many developers would like, but it is actually quite hard to implement. After all, if you make a request from a server and then you decide you don’t want the response anymore, there is no way to tell the server to abandon your original request. The way to deal with this is just to let the bytes come back to the client machine and then throw them away. In addition, there is a race condition here—your request to cancel the request could come just as the server is sending the response. Now what should your application do? You’d need to handle this potential race condition occurring in your own code and decide whether to throw the data away or act on it.

To assist with this, I recommend you implement a WithCancellation extension method that extends Task<TResult> (you need a similar overload that extends Task too) as follows.

```
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