6. Once everything is set up, start the work by calling BackgroundWorker.RunWorkerAsync() and providing a state parameter that is passed to the specified DoWork() method.

When you break it into steps, the background worker pattern is relatively easy to follow and, true to EAP, it provides explicit support for progress notification. The drawback is that you cannot use it arbitrarily on any method. Instead, the DoWork() method must conform to a System.ComponentModel.DoWorkEventHandler delegate, which takes arguments of type object and DoWorkEventArgs. If this isn’t the case, a wrapper function is required—something fairly trivial using anonymous methods. The cancellation- and progress-related methods also require specific signatures, but these are in control of the programmer setting up the background worker pattern.

# Exception Handling

If an unhandled exception occurs while the background worker thread is executing, the RunWorkerCompletedEventArgs parameter of the RunWorkerCompleted delegate (Completed’s eventArgs) will have an Error property set with the exception. As a result, checking the Error property within the RunWorkerCompleted callback in Listing C.10 provides a means of handling the exception.

# LISTING C.10: Handling Unhandled Exceptions from the Worker Thread

```
// ...
static void Complete(
    object sender, RunWorkerCompletedEventArgs eventArgs)
{
    Console.WriteLine();
    if (eventArgs.Cancelled)
    {
        Console.WriteLine("Cancelled");
    }
    else if (eventArgs.Error != null)
    {
        // IMPORTANT: check error to retrieve any exceptions.
        Console.WriteLine(
            "ERROR: {0}", eventArgs.Error.Message);
    }
    else
    {
        Console.WriteLine("Finished");
    }
```