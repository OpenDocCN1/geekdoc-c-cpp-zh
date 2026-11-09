
## C#'s Support for Volatile Fields

Making sure that programmers call the **VolatileRead** and **VolatileWrite** methods correctly is a lot to ask. It's hard for programmers to keep all of this in their minds and to start imagining what other threads might be doing to shared data in the background. To simplify this, the C# compiler has the **volatile** keyword, which can be applied to static or instance fields of any of these types: **Byte, SByte, Int16, UInt16, Int32, UInt32, Char, Single,** or **Boolean**. You also can apply the **volatile** keyword to reference types and any enum field so long as the enumerated type has an underlying type of **Byte, SByte, Int16, UInt16, Int32, UInt32, Single,** or **Boolean**. The JIT compiler ensures that all accesses to a volatile field are performed as volatile reads and writes so that it is not necessary to explicitly call **Thread**'s static **VolatileRead** or **VolatileWrite** methods. Furthermore, the **volatile** keyword tells the C# and JIT compilers not to cache the field in a CPU register, ensuring that all reads to and from the field actually cause the value to be read from memory.

Using the **volatile** keyword, we can rewrite the **ThreadsSharingData** class as follows:

```csharp
internal sealed class ThreadsSharingData {
    private volatile Int32 m_flag = 0;
    private          Int32 m_value = 0;

    // This method is executed by one thread
    public void Thread1() {
        // Note: 5 must be written to m_value before 1 is written to m_flag
        m_value = 5;
        m_flag = 1;
    }

    // This method is executed by another thread
    public void Thread2() {
        // Note: m_value must be read after m_flag is read
        if (m_flag == 1)
            Console.WriteLine(m_value);
    }
}
```

There are some developers (and I am one of them) who do not like C#'s **volatile** keyword, and they think that the language should not provide it. Our array: one response for each request
    private WebResponse[] m_results = new WebResponse[2];

    public MultiWebRequests(Int32 timeout = Timeout.Infinite) {
        // Asynchronously initiate all the requests all at once
        for (Int32 n = 0; n < m_requests.Length; n++) {
            m_ac.AboutToBegin(1);
            m_requests[n].BeginGetResponse(EndGetResponse, n);
        }

        // Tell the helper class that all operations have been initiated
        // and to call AllDone when all operations complete, Cancel is
        // called, or the timeout occurs
        m_ac.AllBegun(AllDone, timeout);
    }

    // Calling this method indicates that the results don't matter anymore
    public void Cancel() { m_ac.Cancel(); }

    // As each Web server responds, this method is called
    private void EndGetResponse(IAsyncResult result) {
        // Get the index corresponding to the request
        Int32 n = (Int32)result.AsyncState;

        // Store the response in the same index as the request
        m_results[n] = m_requests[n].EndGetResponse(result);

        // Tell the helper class that a Web server responded
        m_ac.JustEnded();
    }
}
```

```csharp
// This method is called after all Web servers respond,
// Cancel is called, or the timeout occurs
private void AllDone(CoordinationStatus status) {
    switch (status) {
        case CoordinationStatus.Cancel:
            Console.WriteLine("The operation was canceled"); break;

        case CoordinationStatus.Timeout:
            Console.WriteLine("The operation timed-out"); break;

        case CoordinationStatus.AllDone:
            Console.WriteLine("Here are the results from all the Web servers");
            for (Int32 n = 0; n < m_requests.Length; n++) {
                Console.WriteLine("{0} returned {1} bytes.",
                    m_results[n].ResponseUri, m_results[n].ContentLength);
            }
            break;
    }
}
```

OK, the code above doesn't actually use any **Interlocked** methods directly because I encapsulated all the coordination code in a reusable class called **AsyncCoordinator**, which I'll explain shortly. Let me first explain what this class is doing. When the **MultiWebRequests** class is constructed, it initializes an **AsyncCoordinator**, the array of **WebRequest** objects, and the array of **WebResponse** objects. It then issues all the Web requests asynchronously by calling **BeginGetResponse**. Just before issuing each request, it calls the **AsyncCoordinator**'s **AboutToBegin** method, passing it the number of requests about to be issued.⁶

After all the Web servers' requests have been made, **AsyncCoordinator**'s **AllBegun** method is called, passing it the name of the method that should execute when all the operations complete (**AllDone**) and a timeout value. As each Web server responds, various thread pool threads will call the **MultiWebRequests** class's **EndGetResponse** method. This method determines which request it is processing (by examining the **IAsyncResult**'s **AsyncState** property) and then saves the **WebResponse** object in the **m_results** array. After storing each result, **AsyncCoordinator**'s **JustEnded** method is called to let the **AsyncCoordinator** object know that an operation completed.

If all the operations have completed, then the **AsyncCoordinator** will invoke the **AllDone** method to process the results from all the Web servers. The code executing the **AllDone** method will be the thread pool thread that just happened to get the last Web server response. If timeout or cancellation occurs, then **AllDone** will be invoked via whatever thread pool thread notifies the **AsyncCoordinator** of timeout or using whatever thread happened to call the **Cancel** method. There is also a chance that the thread issuing the Web server requests could invoke **AllDone** itself if the last request completes before **AllBegun** is called.
