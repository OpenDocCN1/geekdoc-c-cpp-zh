There are overloads of the preceding methods that operate on Int64 values. Furthermore, the Interlocked class offers Exchange and CompareExchange methods that take Object, IntPtr, Single, and Double, and there is also a generic version in which the generic is constrained to class (any reference type).

Personally, I love the locked methods, because they are relatively fast and you can do so much with them. Let me show you code that uses the Interlocked to asynchronously query web servers and concurrently return the data. This code is pretty short, never blocks any, and uses thread pools to scale automatically, consuming up to the number of CPUs available if its workload could benefit from it. In addition, the code, as it is, supports accessing up to 2,147,483,647 (Int32.MaxValue) web servers. In other words, this is a great model for your own scenarios.

```
internal sealed class MultiWebRequest {
// This helper class coordinates all the asynchronous operations
    AsyncCoordinator m_ac = new AsyncCoordinator();
    // Set of web servers we want to query & their responses (Exception or Int32)
    // NOTE: Even though multiple could access this dictionary simultaneously,
    // there is no need to access it because the keys are
    // read-only after construction
    private Dictionary<String, Object> m_servers = new Dictionary<String, Object> {
    "http://Winlect.com", null },
    "http://Microsoft.com", null },
    "http://1.1.1.1/", null }
};
ublic MultiWebRequest(Int32 timeout = Timeout.Infinite) {
// Asynchronously initialize all the requests all at once
    var httpClient = new HttpClient();
    foreach (var server in m_servers.Keys) {
        m_ac.AboutToBegin(1);
        httpClient.GetByteArrayAsync(server)
        .ContinueWith(task => ComputeResult(server, task));
    }
// Tell AsyncCoordinator that all operations have been initiated and to call
// When AllDone all operations complete, Cancel is called, or the timeout occurs
    m_ac.AllDoneBegun(AllDone, timeout);
}\private void ComputeResult(String server, Task<Byte[]> task) {
Object result;
if (task.Exception == null) {
    result = task.Exception.InnerException;
} else {
// Process I/O completion on thread pool thread(s)
// Put your own code-intensive algorithm here...
    result = task.Result.Length; // This example returns the length
}}
```