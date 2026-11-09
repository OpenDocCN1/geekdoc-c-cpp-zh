work is being performed on behalf of the original client request, the culture and identity needs to “flow” to the new thread pool thread so any additional work done on behalf of the client is performed using the client’s culture and identity information.

Fortunately, the FCL defines a base class, called System.Threading.SynchronizationContext, which solves all these problems. Simply stated, a SynchronizationContext-derived object connects an application model to its threading model. The FCL defines several classes derived from SynchronizationContext, but usually you will not deal directly with these classes; in fact, many of them are not publicly exposed or documented.

For the most part, application developers do not need to know anything about the SynchronizationContext class. When you await a Task, the calling thread’s SynchronizationContext object is obtained. When a thread pool thread completes the Task, the SynchronizationContext object is used, ensuring the right threading model for your application model. So, when a GUI thread awaits a Task, the code following the await operator is guaranteed to execute on the GUI thread as well, allowing that code to update UI elements.<sup>12</sup> For an ASP.NET application, the code following the await operator is guaranteed to execute on a thread pool thread that has the client’s culture and principal information associated with it.

Most of the time, having a state machine resume using the application model’s threading model is phenomenally useful and convenient. But, on some occasions, this can get you into trouble. Here is an example that causes a WPF application to deadlock.

```
```csharp
private sealed class MyWpfWindow : Window {
    public MyWpfWindow() { Title = "WPF Window"; }

    protected override void OnActivated(EventArgs e) {
        // Querying the Result property prevents the GUI thread from returning;
        // the thread blocks waiting for the result
        String http = GetHttp().Result; // Get the string synchronously!

        base.OnActivated(e);
    }

    private async Task<String> GetHttp() {
        // Issue the HTTP request and let the thread return from GetHttp
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // We never get here: The GUI thread is waiting for this method to finish but this method
        // can't finish because the GUI thread is waiting for it to finish --> DEADLOCK!

        return await msg.Content.ReadAsStringAsync();
    }
}
```
```

Developers creating class libraries definitely need to be aware of the SynchronizationContext class so they can write high-performance code that works with all application models. Because a lot of class library code is application model agnostic, we want to avoid the additional overhead involved

12 Internally, the various SynchronizationContext-derived classes get the GUI thread to resume the state machine using methods like System.Windows.Forms.Control.BeginInvoke, System.Windows.Threading.Dispatcher.BeginInvoke, and Windows.UI.Core.CoreDispatcher.RunAsync.