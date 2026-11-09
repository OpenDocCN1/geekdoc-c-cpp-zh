For anyone who has been working with earlier versions of the .NET Framework, you may be familiar with some other asynchronous programming models that it offered. There is the programming model that used BeginXxx and EndXxx methods along with an IAsyncResult interface. And there is the event-based programming model that also had XxxAsync methods (that did not return Task objects) and invoked event handler methods when an asynchronous operation completed. These two asynchronous programming models are now considered obsolete and the new model using Task objects is the preferred model.

While looking through the FCL, you might notice some classes that are lacking XxxAsync methods and instead only offer BeginXxx and EndXxx methods. This is mostly due to Microsoft not having the time to update these classes with the new methods. In the future, Microsoft should be enhancing these classes so that they fully support the new model. However, until they do, there is a helper method that you can use to adapt the old BeginXxx and EndXxx model to the new Task-based model.

Earlier I showed the code for a client application that makes a request over a named pipe. Let me show the server side of this code now.

```
```csharp
private static async void StartServer() {
    while (true) {
        var pipe = new NamedPipeServerStream(c_pipeName, PipeDirection.InOut, -1,
            PipeTransmissionMode.Message, PipeOptions.Asynchronous | PipeOptions.WriteThrough);

        // Asynchronously accept a client connection
        // NOTE: NamedPipeServerStream uses the old Asynchronous Programming Model (APM)
        // I convert the old APM to the new Task model via TaskFactory's FromAsync method
        await Task.Factory.FromAsync(pipe.BeginWaitForConnection, pipe.EndWaitForConnection,
            null);

        // Start servicing the client, which returns immediately because it is asynchronous
        ServiceClientRequestAsync(pipe);
    }
}
```
```

The NamedPipeServerStream class has BeginWaitForConnection and EndWaitForConnection methods defined, but it does not yet have a WaitForConnectionAsync method defined. Hopefully this method will be added in a future version of the FCL. However, all is not lost, because, as you see in the preceding code, I call TaskScheduler's FromAsync method, passing into it the names of the BeginXxx and EndXxx methods, and then FromAsync internally creates a Task object that wraps these methods. Now I can use the Task object with the await operator.