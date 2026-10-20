
Let’s dig a little deeper into this pattern to examine the methods used for starting and reporting the completion of each download. The finishDownload method is rather simple, and I’ll show it only for completeness:

```
private static void finishDownload(string url, byte[] bytes)
{
    Console.WriteLine("Read {0} bytes from {1}",
        bytes.Length, url);
}
```

StartDownload shows a bit more of the interface provided by the Task Parallel Library. The specific types used help to support the Task interface. I’d like to abstract that away, but handling these types will be a bit different for each specific task you want to accomplish. In fact, the Task Parallel Library puts a common interface on top of the many different async patterns that existed in the .NET BCL prior to this version.

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

This method has a mix of general Task code and code specific to downloading data from a URL, so let’s go through it very carefully. First, it creates a TaskCompletionSource object for this task. A TaskCompletionSource object enables you to separate the creation of a task from its completion.

It’s important here because you are using the WebClient class’s async methods to create the task. The type parameter for the TaskCompletionSource is the type of result returned from the task.

The WebClient class uses the Event-based Asynchronous Pattern (EAP). That means you register a handler for an event that will be raised when an asynchronous operation completes. startDownload() stores the task completion information in the TaskCompletionSource when that event is raised. The TaskScheduler picks up the task and then the download is started. The method returns the Task object embedded inside the TaskCompletionSource so that the event results can be processed once the task completes.

After this bit of work, the Web download occurs asynchronously on another thread. When the download completes, the DownloadDataCompleted event is raised. The event handler will set the completion status for the TaskCompletionSource. That signals the Task embedded in the TaskCompletionSource that it has finished.

Now, the task will invoke ContinueWith(), which will report the results for that download. It takes a bit of unwinding, but after you’ve unwound it once, the pattern isn’t that hard to understand.

The sample shown above is the correct idiom to use when the underlying source uses the Event-based Asynchronous Pattern. Other areas of the .NET library will use the Asynchronous Programming Model (APM) pattern. In that pattern, for some operation Foo you’ll call BeginFoo(), which will return an IAsyncResult. Once the operation has completed, you’ll call EndFoo(), passing in the IAsyncResult. You can use the `Task<TResult>.Factory.FromAsync()` method to implement this pattern using the Task Parallel Library. The underlying idiom will be similar to the version I’ve shown for downloading Web data. The difference would be where you create the task you’d provide a different set of delegates to match the async method being used.

The Task Parallel Library provides a series of methods that enable working with I/O bound operations as well as CPU bound partitions of work. Using the Task class, you can support a variety of asynchronous patterns that work with I/O bound operations, or those that are a mixture of I/O and CPU bound operations. Parallel tasks are still not easy, but the Task Parallel Library and PLINQ provide better language level support for asynchronous programming than previous libraries had. It will continue to be more important as more of our programs must access data on different machines and more threads are waiting for responses from remote machines.

## Item 37: Construct Parallel Algorithms with Exceptions in Mind

The previous two items blissfully ignored the possibility of anything going wrong with any of the child threads doing its work. That’s clearly not how the real world works. Exceptions will occur in your child threads, and you’ll be left to pick up the pieces somehow. Of course, exceptions in background threads increase the complexity in several ways. Exceptions can’t just continue up the call stack across thread boundaries. Instead, if an Exception reaches the thread start method, that thread gets terminated. There’s no way for the calling thread to retrieve the error, or do anything about it. Furthermore, if your parallel algorithm must support rollback if there are problems, you’ll have to do more work to understand any side effects that have occurred and what you should do to recover from those errors. Every algorithm has different requirements, so there are no universal answers for handling exceptions in a parallel environment. The guidelines I provide here are just that: guidelines that you can use to determine the best strategy for your particular application.

Let’s begin with the async download method from the last item. That has a very simple strategy in that there are no side effects, and the downloads from all other Web hosts can continue without concern for the one download that is failing. Parallel operations use the new AggregateException type to handle exceptions in parallel operations. The AggregateException is a container that holds all exceptions generated from any of the parallel operations in an InnerExceptions property. There are a couple different ways to handle the exception in this process. First, I’ll show the more general case, how to handle any errors generated by subtasks in the outer processing.

The RunAsync() method shown in the previous Item uses more than one parallel operation. That means you may have AggregateExceptions in the InnerExceptions collection that is part of the AggregateException you actually catch. The more parallel operations you have, the deeper this nesting can go. Because of the way parallel operations compose with each other, you may end up with multiple copies of the original exception in the final collection of exceptions. I modified the call to RunAsync() to process possible errors:

```
try
{
    urls.RunAsync(
        url => startDownload(url),
        task => finishDownload(
            task.AsyncState.ToString(), task.Result));
}
catch (AggregateException problems)
{
    ReportAggregateError(problems);
}
```

```
private static void ReportAggregateError(
    AggregateException aggregate)
{
    foreach (var exception in aggregate.InnerExceptions)
        if (exception is AggregateException)
            ReportAggregateError(
                exception as AggregateException);
        else
            Console.WriteLine(exception.Message);
}
```

The ReportAggregateError prints out the messages for all exceptions that are not themselves AggregateExceptions. Of course, this has the nasty side effect of swallowing all exceptions, whether you anticipated them or not. That’s rather dangerous. Instead, what you want to do is handle only those exceptions from which you can recover, and rethrow any other exceptions.

There are enough recursive collections here that a utility method makes sense. The generic method must know which exception types you want to handle, and which are not expected, and how you’ll handle the ones you are handling. You need to send this method a set of exception types, and the code to handle the exception. That’s simply a dictionary of types and `Action<T>` lambda expressions. And, if the handler doesn’t process everything in the collection of InnerExceptions, clearly something else went wrong. That means it’s time to rethrow the original exception. Here’s the updated code that calls RunAsync:

```
try
{
    urls.RunAsync(
```
