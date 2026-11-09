Microsoft, and in 2009, the Patent Office issued the patent (Patent #7,603,502). However, even though Microsoft owns the patent for this idea, the FCL does not provide any class that implements this idea. However, I provide an implementation in my Power Threading library. When I sold the rights to Microsoft, I acquired a license allowing Wintellect customers to use this “invention” with the caveat that it can be used only on a Microsoft platform.¹⁰ By downloading the library from the Wintellect Web site, you are a Wintellect customer, and you can use the library subject to the caveat in the restriction.

In Chapter 27, I gave a brief introduction to my **AsyncEnumerator** class, which is also part of my Power Threading library. This class enabled you to use asynchronous programming model with classes that support the CLR’s APM, and since my **ReaderWriterGate** supports the APM, you can use it with the **AsyncEnumerator**. However, when I first tried this, I discovered that I could simplify the programming model even more. So if you want to use my **AsyncEnumerator** and also have multiple iterators accessing shared data in a thread-safe way, use my **SyncGate** class instead of **ReaderWriterGate**. The **SyncGate** class is also in my Power Threading library, and it looks like this:

```
```csharp
public sealed class SyncGate {
    public SyncGate();
    public void BeginRegion(SyncGateMode mode,
        AsyncCallback asyncCallback, Object asyncState);
    public void EndRegion(IAsyncResult result);
}
```
```

You should see the samples in my Power Threading library for examples of using these classes together, but I’ll show a brief example here. I took the **PipeServerAsyncEnumerator** method shown in Chapter 27 and modified it to record the timestamp of the most recent client request in a static field accessible to all threads. Since multiple client requests can be running simultaneously using various threads, updating the static field must be done in a thread-safe way. To accomplish this, I create a static field that holds a reference to a **SyncGate** object, and I call its **BeginRegion** and **EndRegion** methods to acquire and release exclusive access, respectively. Here is the new version of the code with the added lines highlighted:

```
```csharp
// This field records the timestamp of the most recent client's request
private static DateTime s_lastClientRequestTimestamp = DateTime.MinValue;

// The SyncGate enforces thread-safe access to the s_lastClientRequestTimestamp field
private static readonly SyncGate s_gate = new SyncGate();

private static IEnumerator<Int32> PipeServerAsyncEnumerator(AsyncEnumerator ae) {
    // Each server object performs asynchronous operations on this pipe
    using (var pipe = new NamedPipeServerStream(
```
```

¹⁰ Silverlight is considered a Microsoft platform even if your Silverlight application is running in a non-Microsoft operating system. And, my Power Threading library does have a version of this class for Silverlight as well as the Microsoft .NET Compact Framework.