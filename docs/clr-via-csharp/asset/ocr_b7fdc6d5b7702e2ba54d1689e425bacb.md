Reader-writer locks are very popular and useful.<sup>8</sup> Trying to build one of these out of **Task** objects would be quite challenging. However, my Power Threading library includes a non-blocking reader-writer class, which I call **ReaderWriterGate**. It looks like this (some methods are not shown):

```
```csharp
public sealed class ReaderWriterGate : IDisposable {
   public ReaderWriterGate();
   public void Dispose();

   public IAsyncResult BeginRead(ReaderWriterGateCallback callback, Object state,
      AsyncCallback asyncCallback, Object asyncState);
   public Object EndRead(IAsyncResult result);

   public IAsyncResult BeginWrite(ReaderWriterGateCallback callback, Object state,
      AsyncCallback asyncCallback, Object asyncState);
   public Object EndWrite(IAsyncResult result);
}
```
```

The **ReaderWriterGateCallback** is a delegate that looks like this:

```
```csharp
public delegate Object ReaderWriterGateCallback(ReaderWriterGateReleaser releaser);
```
```

The **ReaderWriterGateReleaser** class looks like this (some methods are not shown):

```
```csharp
public sealed class ReaderWriterGateReleaser : IDisposable {
   public Object State { get; }  // Returns the 'state' passed to BeginRead/BeginWrite
   public void Dispose();
}
```
```

The **ReaderWriterGate** makes a lock look just like an asynchronous I/O operation. In fact, my class even offers **BeginRead** and **BeginWrite** methods that take an **AsyncCallback** delegate and return an **IAsyncResult**, as well as **EndRead** and **EndWrite** methods that accept an **IAsyncResult**. I designed the class to work exactly like the APM that was discussed in Chapter 27.

Here's how it works. Put the code that requires read access to a resource in its own method and then call **BeginRead**, passing this method for the **ReaderWriterGateCallback** delegate parameter. When it is safe to read from the resource, the **ReaderWriterGate** object will have a thread pool thread invoke your method. Note that several thread pool threads could be executing methods that read from the resource concurrently. Put the code that requires write access to a resource in its own method and then call **BeginWrite**, passing this method for the **ReaderWriterGateCallback** delegate parameter. When it is safe to write to the resource, the **ReaderWriterGate** object will have a thread pool thread invoke your method. Note that the **ReaderWriterGate** object ensures that there will be only one thread pool thread executing a method that writes to the resource at a particular time.

8 Of course, if you only need mutual-exclusive access to a resource, you can always use a reader-writer lock and request only write access to the resource it protects.