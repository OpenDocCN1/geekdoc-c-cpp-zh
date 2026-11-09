And, here’s yet another benefit: let’s say that your application wants to download 10 images from various websites, and that it takes 5 seconds to download each image. If you perform this work synchronously (downloading one image after another), then it takes you 50 seconds to get the 10 images. However, if you use just one thread to initiate 10 asynchronous download operations, then all 10 are being performed concurrently and all 10 images will come back in just 5 seconds! That is, when performing multiple synchronous I/O operations, the time it takes to get all the results is the sum of the times required for each individual result. However, when performing multiple asynchronous I/O operations, the time it takes to get all the results is the time required to get the single worst-performing operation.

For GUI applications, asynchronous operations offer yet another advantage: the application’s user interface doesn’t hang and remains responsive to the end user. In fact, if you are building a Microsoft Silverlight or Windows Store application, you must perform all I/O operations asynchronously, because the class libraries available to you for performing I/O operations only expose these operations asynchronously; the equivalent synchronous methods simply do not exist in the library. This was done purposely ensuring that these applications can never issue a synchronous I/O operation, thereby blocking the GUI thread making the application nonresponsive to the end user. This forces developers to build responsive applications providing end users a better experience.

# ## C#'s Asynchronous Functions

Performing asynchronous operations is the key to building scalable and responsive applications that allow you to use very few threads to execute lots of operations. And when coupled with the thread pool, asynchronous operations allow you to take advantage of all of the CPUs that are in the machine. Realizing the enormous potential here, Microsoft designed a programming model that would make it easy for developers to take advantage of this capability.3 This pattern leverages Tasks (as discussed in Chapter 27, “Compute-Bound Asynchronous Operations”) and a C# language feature called asynchronous functions (or async functions, for short). Here is an example of code that uses an async function to issue two asynchronous I/O operations.

```
```csharp
private static async Task<String> IssueClientRequestAsync(String serverName, String message) {
    using (var pipe = new NamedPipeClientStream(serverName, "PipeName", PipeDirection.InOut,
        PipeOptions.Asynchronous | PipeOptions.WriteThrough)) {

        pipe.Connect(); // Must Connect before setting ReadMode
        pipe.ReadMode = PipeTransmissionMode.Message;

        // Asynchronously send data to the server
        Byte[] request = Encoding.UTF8.GetBytes(message);
        await pipe.WriteAsync(request, 0, request.Length);
```
```

3 For developers using a version of the Microsoft .NET Framework prior to version 4.5, my AsyncEnumerator class (that is part of my Power Threading library available at http://Wintellect.com/) allows you to use a programming model quite similar to the programming model that now ships as part of .NET Framework 4.5. In fact, the success of my AsyncEnumerator class allowed me to assist Microsoft in designing the programming model I explain in this chapter. Due to the similarities, it is trivial to migrate code using my AsyncEnumerator class to the new programming model.