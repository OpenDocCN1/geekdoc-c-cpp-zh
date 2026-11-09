
```
// If there is a pending continuation, this thread takes it
Action continuation = Interlocked.Exchange(ref m_continuation, null);
if (continuation != null) continuation();   // Resume the state machine
}
}
```

And here is a method that uses my EventAwaiter class to return from an await operator whenever an event is raised. In this case, the state machine continues whenever any thread in the AppDomain throws an exception:

```
private static async void ShowExceptions() {
    var eventAwaiter = new EventAwaiter<FirstChanceExceptionEventArgs>();
    AppDomain.CurrentDomain.FirstChanceException += eventAwaiter.EventRaised;

    while (true) {
        Console.WriteLine("AppDomain exception: {0}",
            (await eventAwaiter).Exception.GetType());
    }
}
```

And finally, here is some code that demonstrates it all working:

```
public static void Go() {
    ShowExceptions();

    for (Int32 x = 0; x < 3; x++) {
        try {
            switch (x) {
                case 0: throw new InvalidOperationException();
                case 1: throw new ObjectDisposedException("");
                case 2: throw new ArgumentOutOfRangeException();
            }
        }
        catch { }
    }
}
```

## Async Functions and Event Handlers

Async functions usually have a return type of either Task or Task<TResult> to represent the completion of the function's state machine. However, it is also possible to define an async function with a void return type. This is a special case that the C# compiler allows to simplify the very common scenario where you want to implement an asynchronous event handler.

Almost all event handler methods adhere to a method signature similar to this:

```
void EventHandlerCallback(Object sender, EventArgs e);
```

But, it is common to want to perform I/O operations inside an event handler, for example, when a user clicks a UI element to open a file and read from it. To keep the UI responsive, this I/O should be done asynchronously. Allowing you to write this code in an event handler method which has a void return type, requires that the C# compiler allows async functions to have a void return type so you can use the await operator to perform non-blocking I/O operations. When an async function has a void return type, the compiler still generates code to create the state machine but it does not create a Task object since there is no way that one could be used. Because of this, there is no way to know when the state machine of a void-returning async function has run to completion.55

## Async Functions in the Framework Class Library

Personally, I love async functions because they are relatively easy to learn, simple to use, and they are supported by many types in the FCL. It is easy to identify async functions because, by convention, Async is suffixed onto the method's name. In the Framework Class Library (FCL), many of the types that offer I/O operations offer XxxAsync methods56. Here are some examples.

- All the System.IO.Stream-derived classes offer ReadAsync, WriteAsync, FlushAsync, and CopyToAsync methods.
- All the System.IO.TextReader-derived classes offer ReadAsync, ReadLineAsync, ReadToEndAsync, and ReadBlockAsync methods. And the System.IO.TextWriter-derived classes offer WriteAsync, WriteLineAsync, and FlushAsync methods.
- The System.Net.Http.HttpClient class offers GetAsync, GetStreamAsync, GetByteArrayAsync, PostAsync, PutAsync, DeleteAsync, and many more.
- All System.Net.WebRequest-derived classes (including FileWebRequest, FtpWebRequest, and HttpWebRequest) offer GetRequestStreamAsync and GetResponseAsync methods.
- The System.Data.SqlClient.SqlCommand class offers ExecuteDbDataReaderAsync, ExecuteNonQueryAsync, ExecuteReaderAsync, ExecuteScalarAsync, and ExecuteXmlReaderAsync methods.
- Tools (such as SvcUtil.exe) that produce web service proxy types also generate XxxAsync methods.

For anyone who has been working with earlier versions of the .NET Framework, you may be familiar with some other asynchronous programming models that it offered. There is the programming model that used BeginXxx and EndXxx methods along with an IAsyncResult interface. And there is the event-based programming model that also had XxxAsync methods (that did not return Task objects) and invoked event handler methods when an asynchronous operation completed. These two asynchronous programming models are now considered obsolete and the new model using Task objects is the preferred model.

While looking through the FCL, you might notice some classes that are lacking XxxAsync methods and instead only offer BeginXxx and EndXxx methods. This is mostly due to Microsoft not having the time to update these classes with the new methods. In the future, Microsoft should be enhancing these classes so that they fully support the new model. However, until they do, there is a helper method which you can use to adapt the old BeginXxx and EndXxx model to the new Task-based model.

Earlier I showed the code for a client application that makes a request over a named pipe. Let me show the server side of this code now:

```
private static async void StartServer() {
    while (true) {
        var pipe = new NamedPipeServerStream(c_pipeName, PipeDirection.InOut, -1,
            PipeTransmissionMode.Message, PipeOptions.Asynchronous | PipeOptions.WriteThrough);

        // Asynchronously accept a client connection
        // NOTE: NamedPipeServerStream uses the old Asynchronous Programming Model (APM)
        // I convert the old APM to the new Task model via TaskFactory's FromAsync method
        await Task.Factory.FromAsync(pipe.BeginWaitForConnection, pipe.EndWaitForConnection, null);

        // Start servicing the client which returns immediately since it is asynchronous
        ServiceClientRequestsAsync(pipe);
    }
}
```

The NamedPipeServerStream class has BeginWaitForConnection and EndWaitForConnection methods defined, but it does not yet have a WaitForConnectionAsync method defined. Hopefully this method will be added in a future version of the FCL. However, all is not lost, because, as you see in the code above, I call TaskFactory's FromAsync method passing into it the names of the BeginXxx and EndXxx methods, and then FromAsync internally creates a Task object that wraps these methods. Now I can use the Task object with the await operator.57

57 TaskFactory's FromAsync method has overloads that accept an IAsyncResult as well as overloads that accept delegates to the BeginXxx and EndXxx methods. When

For the old event-based programming model, the FCL does not include any helper methods to adapt this model into the new Task-based model. So you have to hard code it. Here is code demonstrating how to wrap a WebClient (which uses the event-based programming model) with a TaskCompletionSource so it can be awaited on in an async function:

```
private static async Task<String> AwaitWebClient(Uri uri) {
   // The System.Net.WebClient class supports the Event-based Asynchronous Pattern
   var wc = new System.Net.WebClient();

   // Create the TaskCompletionSource and its underlying Task object
   var tcs = new TaskCompletionSource<String>();

   // When a string completes downloading, the WebClient object raises the
   // DownloadStringCompleted event which completes the TaskCompletionSource
   wc.DownloadStringCompleted += (s, e) => {
      if (e.Cancelled) tcs.SetCanceled();
      else if (e.Error != null) tcs.SetException(e.Error);
      else tcs.SetResult(e.Result);
   };

   // Start the asynchronous operation
   wc.DownloadStringAsync(uri);

   // Now, we can await the TaskCompletionSource's Task and process the result as usual
   String result = await tcs.Task;
   // Process the resulting string (if desired)...

   return result;
}
```

## Async Functions and Exception Handling

When a Windows device driver is processing an asynchronous I/O request, it is possible for something to go wrong, and Windows will need to inform your application of this. For example, while sending bytes or waiting for bytes to come in over the network, a timeout could expire. If the data does not come in time, the device driver will want to tell you that the asynchronous operation completed with an error. To accomplish this, the device driver posts the completed IRP to the CLR's thread pool and a thread pool thread will complete the Task object with an exception. When your state machine method is resumed, the await operator sees that the operation failed and throws this exception.

In Chapter 27, I discussed how Task objects normally throw an AggregateException, and then you'd query this exception's InnerExceptions property to see the real exception(s) that occurred. However, when using await with a Task, the first inner exception is thrown instead of an AggregateException.58 This was done to give you the programming experience you expect. Also, if possible, avoid the overloads that accept an IAsyncResult as they are less efficient.

58 For the curious, it is TaskAwaiter's GetResult method that throws the first inner
