
### Converting the IAsyncResult APM to a Task

In “The APM and Compute-Bound Operations” section earlier in this chapter, I showed how to use the APM to perform a compute-bound operation. In this section, I show how to do the opposite: use a Task to perform an I/O-bound operation.

In the **System.Threading.Tasks** namespace, there is a class called **TaskFactory**. This class was discussed in Chapter 26. However, this class offers a **FromAsync** method, which I did not discuss in Chapter 26. This method accepts four arguments and returns a reference to a **Task** object. The four arguments are a **BeginXxx** method, an **EndXxx** method, an **Object** state, and an optional **TaskCreationOptions**^10^ value. So instead of initiating an asynchronous operation like this:

```csharp
WebRequest webRequest = WebRequest.Create("http://Wintellect.com/");
webRequest.BeginGetResponse(Result => {
    WebResponse webResponse = null;
    try {
        webResponse = webRequest.EndGetResponse(result);
        Console.WriteLine("Content length: " + webResponse.ContentLength);
    }
    catch (WebException we) {
        Console.WriteLine("Failed: " + we.GetBaseException().Message);
    }
    finally { if (webResponse != null) webResponse.Close(); }
}, null);
```

you can turn it into a **Task**, and then use it with the rest of the **Task** infrastructure like this:

```csharp
WebRequest webRequest = WebRequest.Create("http://Wintellect.com/");
Task.Factory.FromAsync<WebResponse>(
    webRequest.BeginGetResponse, webRequest.EndGetResponse, null, TaskCreationOptions.None)
.ContinueWith(task => {
    WebResponse webResponse = null;
    try {
        webResponse = task.Result;
        Console.WriteLine("Content length: " + webResponse.ContentLength);
    }
    catch (AggregateException ae) {
        if (ae.GetBaseException() is WebException)
            Console.WriteLine("Failed: " + ae.GetBaseException().Message);
        else throw;
    }
    finally { if (webResponse != null) webResponse.Close(); }
});
```

Since the EAP was created for Windows Forms developers, let me show you some Windows Forms code that uses the pattern:

```csharp
internal static class Eap {
    public static void Main() {
        // Create the form and show it
        Application.Run(new MyForm());
    }

    private sealed class MyForm : Form {
        protected override void OnClick(EventArgs e) {
            // The System.Net.WebClient class supports the Event-based Asynchronous Pattern
            WebClient wc = new WebClient();

            // When a string completes downloading, the WebClient object raises the
            // DownloadStringCompleted event which will invoke our ProcessString method
            wc.DownloadStringCompleted += ProcessString;

            // Start the asynchronous operation (this is like calling a BeginXxx method)
            wc.DownloadStringAsync(new Uri("http://Wintellect.com"));
            base.OnClick(e);
        }

        // This method is guaranteed to be called via the GUI thread
        private void ProcessString(Object sender, DownloadStringCompletedEventArgs e) {
            // If an error occurred, display it; else display the downloaded string
            MessageBox.Show((e.Error != null) ? e.Error.Message : e.Result);
        }
    }
}
```

In this sample, I manually wrote all the code, but I could have used Visual Studio to drag a **WebClient** control to my form. Then Visual Studio could have emitted the **ProcessString** method with no code in it and emitted the code to register this method with **WebClient**'s **DownloadStringCompleted** event. The EAP also guarantees that the event is raised on the application's GUI thread, allowing code in the event handler method to update UI controls. In addition to Visual Studio designer support, this is another big feature of the EAP. That is, classes that support the EAP automatically map the application model to its threading model; the EAP classes use the **SynchronizationContext** class internally. In addition, some of the EAP classes offer cancellation and progress reporting.

In the whole FCL, there are just 17 types that implement the EAP pattern. Some of these classes are derived from **System.ComponentModel.Component**, which allows them to be dragged and dropped onto a Visual Studio design surface, but most of the classes derive directly from **System.Object**. Here is the list of classes that support the EAP:

- System.ComponentModel.Component-derived types
  - System.ComponentModel.BackgroundWorker
  - System.Media.SoundPlayer
  - System.Net.WebClient
  - System.Net.NetworkInformation.Ping
  - System.Windows.Forms.PictureBox (derived from Control)
- System.Object-derived types
  - System.Net.Mail.SmtpClient
  - System.Deployment.Application.ApplicationDeployment
  - System.Deployment.Application.InPlaceHostingManager
  - System.Activities.WorkflowInvoker
  - System.ServiceModel.Activities.WorkflowControlClient
  - System.Net.PeerToPeer.PeerNameResolver
  - System.Net.PeerToPeer.Collaboration.ContactManager
  - System.Net.PeerToPeer.Collaboration.Peer
  - System.Net.PeerToPeer.Collaboration.PeerContact
  - System.Net.PeerToPeer.Collaboration.PeerNearMe
  - System.ServiceModel.Discovery.AnnouncementClient
  - System.ServiceModel.Discovery.DiscoveryClient

The FCL ships 60 classes that implement the `IAsyncResult` pattern, including the following classes for which there is no equivalent class available that implements the EAP: the various `Stream`-derived classes (`FileStream`, `IsolatedStorageFileStream`, `DeflateStream`, `GZipStream`, and `PipeStream`), `SqlCommand`, and more.

I should also point out that tools that produce Web service proxy classes, like `WSDL.exe` and `SvcUtil.exe`, can produce proxy classes that support both the APM and the EAP.

If you look at the 17 classes listed above, they are all related to performing I/O-bound work except for one: `BackgroundWorker`. The `BackgroundWorker` class is designed for doing asynchronous compute-bound work, but unfortunately, a lot of developers use `BackgroundWorker` to perform synchronous I/O-bound work, which blocks a thread. I/O-bound work should be performed using one of the other 16 EAP classes or any of the classes that support the APM. The `BackgroundWorker` class offers the following three events:

- **DoWork**：The method that you register with this event should contain the compute-bound code. This event is raised by a thread pool thread.
- **ProgressChanged**：The method that you register with this event should contain the code that updates the UI with progress information. This event is always raised on the GUI thread. The `DoWork` event handler method must periodically call `BackgroundWorker`'s `ReportProgress` method to raise the `ProgressChanged` event.
- **RunWorkerCompleted**：The method that you register with this event should contain the code that updates the UI with the result of the compute-bound operation. This event is always raised on the GUI thread. The `DoWork` event handler method is passed a reference to a `DoWorkEventArgs` object. This object's `Result` property must be set to the value that the compute-bound operation wishes to return.

### Converting the EAP to a Task

In the "Converting the `IAsyncResult` APM to a `Task`" section earlier in this chapter, I showed how to use the `IAsyncResult` APM to turn an asynchronous operation into a `Task` so that it could be used with the rest of the `Task` infrastructure. Well, it is also possible to turn an asynchronous operation using the EAP into a `Task`. The `System.Threading.Tasks` namespace defines a `TaskCompletionSource` class that looks like this:

### Comparing the APM and the EAP

In this section, I compare the APM to the EAP. The biggest benefit of the EAP over the APM is that it can be used with the Visual Studio offering a design-time approach to invoke asynchronous operations. In addition, the EAP was introduced in the FCL at the same time as the **SynchronizationContext** class, and therefore it has built into it the ability to understand an application’s threading model to ensure that, for GUI applications, the event handler method is invoked on the GUI thread.

However, the APM is closer to the metal and the EAP classes are typically implemented internally using the APM. This means that EAP classes tend to use more memory and perform slower than their APM equivalents. In fact, the EAP must allocate `EventArgs`-derived objects for all progress reporting and completion events that are raised. Several EAP classes also contain a collection of `UserState` objects identifying separate operations and an `AsyncOperation` object, too. In a typical GUI application, these additional memory allocations (which cause additional garbage collections) are probably insignificant. However, the EAP would be an inappropriate choice for building a high-performance server application.

For simple scenarios, the EAP is easy to use and a fine choice. However, there are some scenarios where the EAP will actually be more complicated to use. If you call the `XxxAsync` method before registering the event handler method, it is possible that the asynchronous operation could complete before registering the event handler method and then the event handler method will not be invoked. Also, events are cumulative, and so you must unregister a method from the event and register a new method with the event if you want your next asynchronous operation to invoke a different method. Furthermore, static methods and singleton classes cannot offer the EAP for the same reason: different parts of an application may all register events at once, and all event handlers would be invoked when an operation completes regardless of which part of the application issued the asynchronous operation.

Error handling with the EAP is incongruous with the rest of the system. First, exceptions aren’t thrown; in your event handler, you must query the `AsyncCompletedEventArgs`’s `Exception` property to see if it is `null` or not. If it is not `null`, then you have to use `if` statements to determine the type of the `Exception`-derived object instead of using `catch` blocks. And, if your code ignores the error, then no unhandled exception occurs, errors go undetected, and your application continues running with unpredictable results.

### Programming Model Soup

Over the years, the .NET Framework has amassed a number of asynchronous programming models, each with its pros and cons, and I’m sure that new programming models will appear in the future. In an effort to help you, I have produced Table 27-1, which summarizes the various models that currently exist. For each model, I show what its intended primary use is (compute-bound or I/O-bound operations), how it can emulate the other kind of operation,
