Click here to view code image

```
await pixelStream.WriteAsync(data, 0, data.Length);
```

In summary, when you build applications for Windows, you should seek to exploit asynchronicity wherever possible.

# The IAsyncResult design pattern in earlier versions of the .NET Framework

Asynchronicity has long been recognized as a key element in building responsive applications with the .NET Framework, and the concept predates the introduction of the Task class in the .NET Framework version 4.0. Microsoft introduced the IAsyncResult design pattern based on the AsyncCallback delegate type to handle these situations. The exact details of how this pattern works are not appropriate in this book, but from a programmer’s perspective the implementation of this pattern meant that many types in the .NET Framework class library exposed long-running operations in two ways: in a synchronous form consisting of a single method, and in an asynchronous form that used a pair of methods, named BeginOperationName and EndOperationName, where OperationName specified the operation being performed. For example, the MemoryStream class in the System.IO namespace provides the Write method to write data synchronously to a stream in memory, but it also provides the BeginWrite and EndWrite methods to perform the same operation asynchronously. The BeginWrite method initiates the write operation that is performed on a new thread. The BeginWrite method expects the programmer to provide a reference to a callback method that runs when the write operation completes; this reference is in the form of an AsyncCallback delegate. In this method, the programmer should implement any appropriate tidying up and call the EndWrite method to signify that the operation has completed. The following code example shows this pattern in action:

Click here to view code image

```
...
Byte[] buffer = ...; // populated with data to write to the MemoryStream
MemoryStream ms = new MemoryStream();
AsyncCallback callback = new AsyncCallback(handleWriteCompleted);
ms.BeginWrite(buffer, 0, buffer.Length, callback, ms);
...

private void handleWriteCompleted(IAsyncResult ar)
{
    MemoryStream ms = ar.AsyncState as MemoryStream;
    ... // Perform any appropriate tidying up
    ms.EndWrite(ar);
}
```