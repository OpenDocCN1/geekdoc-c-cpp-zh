specified the operation being performed

For example, the MemoryStream class in the System.IO namespace provides the Write method to write data synchronously to a stream in memory, but it also provides the BeginWrite and EndWrite methods to perform the same operation asynchronously. The BeginWrite method initiates the write operation that's performed on a new thread. The BeginWrite method expects the programmer to provide a reference to a callback method that runs when the operation completes; this reference is in the form of an AsyncCallback delegate. In this method, the programmer should implement any appropriate tidying up and call the EndWrite method to signify that the operation completed. The following code example shows this pattern in action:

Click here to view code image

```
Byte[] buffer = ...; // populated with data to write to the
MemoryStream
MemoryStream sequence = new MemoryStream();
AsyncCallback callback = new
AsyncCallback(handleWriteCompleted);
ms.BeginWrite(buffer, 0, buffer.Length, callback, ms);

private void handleWriteCompleted(IAsyncResult ar)
{
    MemoryStream ms = ar.AsyncState as MemoryStream;
    // Perform any appropriate tidying up
    ms.EndWrite(ar);
}
```

The parameter to the callback method (handleWriteCompleted) is an IAsyncResult object that contains information about the status of the asynchronous operation and any other state information. You can pass user-defined information to the callback in this parameter; the final argument supplied to the BeginOperationName method is packaged into this parameter. In this example, the callback is passed a reference to MemoryStream.

Although this sequence works, it's a messy paradigm that obscures the operation you're performing. The code for the operation is split into two