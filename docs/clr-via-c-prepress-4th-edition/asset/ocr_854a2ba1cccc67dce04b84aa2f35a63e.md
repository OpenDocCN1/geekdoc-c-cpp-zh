```
~~~csharp
        break;

    case CoordinationStatus.AllDone:
        Console.WriteLine("Operation completed; results below:");
        foreach (var server in m_servers) {
            Console.WriteLine("{0} ", server.Key);
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
~~~
```

OK, the code above doesn't actually use any Interlocked methods directly, because I encapsulated all the coordination code in a reusable class called AsyncCoordinator, which I'll explain shortly. Let me first explain what this class is doing. When the MultiWebRequest class is constructed, it initializes an AsyncCoordinator and a dictionary containing the set of server URIs (and their future result). It then issues all the web requests asynchronously one right after the other. It does this by first calling AsyncCoordinator's AboutToBegin method, passing it the number of requests about to be issued.<sup>70</sup> Then it initiates the request by calling HttpClient's GetByteArrayAsync. This returns a Task and I then call ContinueWith on this Task so that when the server replies with the bytes, they can be processed by my ComputeResult method concurrently via many thread pool threads. After all the web servers' requests have been made, the AsyncCoordinator's AllBegin method is called, passing it the name of the method (AllDone) that should execute when all the operations complete and a timeout value. As each web server responds, various thread pool threads will call the MultiWebRequest's ComputeResult method. This method processes the bytes returned from the server (or any error that may have occurred) and saves the result in the dictionary collection. After storing each result, AsyncCoordinator's JustEnded method is called to let the AsyncCoordinator object know that an operation completed.

If all the operations have completed, then the AsyncCoordinator will invoke the AllDone method to process the results from all the web servers. The code executing the AllDone method will be the thread pool thread that just happened to get the last web server response. If timeout or

> <sup>70</sup> The code would still work correctly if it was rewritten calling `m_ac.AboutToBegin(m_requests.Count)` just once before the `for` loop instead of calling AboutToBegin inside the loop.