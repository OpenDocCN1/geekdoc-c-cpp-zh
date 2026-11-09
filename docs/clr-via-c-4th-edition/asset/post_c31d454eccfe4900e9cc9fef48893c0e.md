
There are also overloads of the preceding methods that operate on Int64 values. Furthermore, the Interlocked class offers Exchange and CompareExchange methods that take Object, IntPtr, Single, and Double, and there is also a generic version in which the generic type is constrained to class (any reference type).

Personally, I love the Interlocked methods, because they are relatively fast and you can do so much with them. Let me show you some code that uses the Interlocked methods to asynchronously query several web servers and concurrently process the returned data. This code is pretty short, never blocks any threads, and uses thread pool threads to scale automatically, consuming up to the number of CPUs available if its workload could benefit from it. In addition, the code, as is, supports accessing up to 2,147,483,647 (Int32.MaxValue) web servers. In other words, this code is a great model to follow for your own scenarios.

```csharp
internal sealed class MultiWebRequests {
    // This helper class coordinates all the asynchronous operations
    private AsyncCoordinator m_ac = new AsyncCoordinator();

    // Set of web servers we want to query & their responses (Exception or Int32)
    // NOTE: Even though multiple could access this dictionary simultaneously,
    //       there is no need to synchronize access to it because the keys are
    //       read-only after construction
    private Dictionary<String, Object> m_servers = new Dictionary<String, Object> {
        { "http://Wintellect.com/", null },
        { "http://Microsoft.com/", null },
        { "http://1.1.1.1/",      null }
    };

    public MultiWebRequests(Int32 timeout = Timeout.Infinite) {
        // Asynchronously initiate all the requests all at once
        var httpClient = new HttpClient();
        foreach (var server in m_servers.Keys) {
            m_ac.AboutToBegin(1);
            httpClient.GetByteArrayAsync(server)
                .ContinueWith(task => ComputeResult(server, task));
        }

        // Tell AsyncCoordinator that all operations have been initiated and to call
        // AllDone when all operations complete, Cancel is called, or the timeout occurs
        m_ac.AllBegun(AllDone, timeout);
    }

    private void ComputeResult(String server, Task<Byte[]> task) {
        Object result;
        if (task.Exception != null) {
            result = task.Exception.InnerException;
        } else {
            // Process I/O completion here on thread pool thread(s)
            // Put your own compute-intensive algorithm here...
            result = task.Result.Length;   // This example just returns the length
        }

        // Save result (exception/sum) and indicate that 1 operation completed
        m_servers[server] = result;
        m_ac.JustEnded();
    }

    // Calling this method indicates that the results don't matter anymore
    public void Cancel() { m_ac.Cancel(); }

    // This method is called after all web servers respond,
    // Cancel is called, or the timeout occurs
    private void AllDone(CoordinationStatus status) {
        switch (status) {
            case CoordinationStatus.Cancel:
                Console.WriteLine("Operation canceled.");
                break;

            case CoordinationStatus.Timeout:
                Console.WriteLine("Operation timed-out.");
                break;

            case CoordinationStatus.AllDone:
                Console.WriteLine("Operation completed; results below:");
                foreach (var server in m_servers) {
                    Console.Write("{0} ", server.Key);
                    Object result = server.Value;
                    if (result is Exception) {
                        Console.WriteLine("failed due to {0}.", result.GetType().Name);
                    } else {
                        Console.WriteLine("returned {0:N0} bytes.", result);
                    }
                }
                break;
        }
    }
}
```

OK, the preceding code doesn't actually use any Interlocked methods directly, because I encapsulated all the coordination code in a reusable class called AsyncCoordinator, which I'll explain shortly. Let me first explain what this class is doing. When the MultiWebRequests class is constructed, it initializes an AsyncCoordinator and a dictionary containing the set of server URIs (and their future result). It then issues all the web requests asynchronously one right after the other. It does this by first calling AsyncCoordinator's AboutToBegin method, passing it the number of requests about to be issued.⁷ It then initiates the request by calling HttpClient's GetByteArrayAsync. This returns a Task and I then call ContinueWith on this Task so that when the server replies with the bytes, they can be processed by my ComputeResult method concurrently via many thread pool threads. After all the web servers' requests have been made, the AsyncCoordinator's AllBegun method is called, passing it the name of the method (AllDone) that should execute when all the operations complete and a timeout value. As each web server responds, various thread pool threads will call the MultiWebRequests's ComputeResult method. This method processes the bytes returned from the server (or any error that may have occurred) and saves the result in the dictionary collection. After storing each result, AsyncCoordinator's JustEnded method is called to let the AsyncCoordinator object know that an operation completed.

If all the operations have completed, then the AsyncCoordinator will invoke the AllDone method to process the results from all the web servers. The code executing the AllDone method will be the thread pool thread that just happened to get the last web server response. If timeout or cancellation occurs, then AllDone will be invoked via whatever thread pool thread notifies the AsyncCoordinator of timeout or using whatever thread happened to call the Cancel method. There is also a chance that the thread issuing the web server requests could invoke AllDone itself if the last request completes before AllBegun is called.

Note that there is a race because it is possible that all web server requests complete, AllBegun is called, timeout occurs, and Cancel is called all at the exact same time. If this happens, then the AsyncCoordinator will select a winner and three losers, ensuring that the AllDone method is never called more than once. The winner is identified by the status argument passed into AllDone, which can be one of the symbols defined by the CoordinationStatus type.

```csharp
internal enum CoordinationStatus { AllDone, Timeout, Cancel };
```

Now that you get a sense of what happens, let's take a look at how it works. The AsyncCoordinator class encapsulates all the thread coordination logic in it. It uses Interlocked methods for everything to ensure that the code runs extremely fast and that no threads ever block. Here is the code for this class.

```csharp
internal sealed class AsyncCoordinator {
    private Int32 m_opCount = 1;        // Decremented when AllBegun calls JustEnded
    private Int32 m_statusReported = 0; // 0=false, 1=true
    private Action<CoordinationStatus> m_callback;
    private Timer m_timer;

    // This method MUST be called BEFORE initiating an operation
    public void AboutToBegin(Int32 opsToAdd = 1) {
        Interlocked.Add(ref m_opCount, opsToAdd);
    }

    // This method MUST be called AFTER an operation's result has been processed
    public void JustEnded() {
        if (Interlocked.Decrement(ref m_opCount) == 0)
            ReportStatus(CoordinationStatus.AllDone);
    }

    // This method MUST be called AFTER initiating ALL operations
    public void AllBegun(Action<CoordinationStatus> callback,
        Int32 timeout = Timeout.Infinite) {
        m_callback = callback;
        if (timeout != Timeout.Infinite)
            m_timer = new Timer(TimeExpired, null, timeout, Timeout.Infinite);
        JustEnded();
    }

    private void TimeExpired(Object o) { ReportStatus(CoordinationStatus.Timeout); }
    public void Cancel() { ReportStatus(CoordinationStatus.Cancel); }

    private void ReportStatus(CoordinationStatus status) {
        // If status has never been reported, report it; else ignore it
        if (Interlocked.Exchange(ref m_statusReported, 1) == 0)
            m_callback(status);
    }
}
```

The most important field in this class is the m_opCount field. This field keeps track of the number of asynchronous operations that are still outstanding. Just before each asynchronous operation is started, AboutToBegin is called. This method calls Interlocked.Add to add the number passed to it to the m_opCount field in an atomic way. Adding to m_opCount must be performed atomically because web servers could be processing responses on thread pool threads as more operations are being started. As web server responses are processed, JustEnded is called. This method calls Interlocked.Decrement to atomically subtract 1 from m_opCount. Whichever thread happens to set m_opCount to 0 calls ReportStatus.

> **Note** The m_opCount field is initialized to 1 (not 0); this is critically important because it ensures that AllDone is not invoked while the thread executing the constructor method is still issuing web server requests. Before the constructor calls AllBegun, there is no way that m_opCount will ever reach 0. When the constructor calls AllBegun, AllBegun internally calls JustEnded, which decrements m_opCount and effectively undoes the effect of having initialized it to 1. Now, m_opCount can reach 0, but only after we know that all the web server requests have been initiated.

The ReportStatus method arbitrates the race that can occur among all the operations completing, the timeout occurring, and Cancel being called. ReportStatus must make sure that only one of these conditions is considered the winner so that the m_callback method is invoked only once. Arbitrating the winner is done via calling Interlocked.Exchange, passing it a reference to the m_statusReported field. This field is really treated as a Boolean variable; however, it can't actually be a Boolean variable because there are no Interlocked methods that accept a Boolean variable. So I use an Int32 variable instead where 0 means false and 1 means true.

Inside ReportStatus, the Interlocked.Exchange call will change m_statusReported to 1. But only the first thread to do this will see Interlocked.Exchange return a 0, and only this thread will invoke the callback method. Any other threads that call Interlocked.Exchange will get a return value of 1, effectively notifying these threads that the callback method has already been invoked and therefore it should not be invoked again.
