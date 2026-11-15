```
{
string digits = (string)eventArgs.UserState;
Console.Write(digits);
}

static void Complete(
object sender,
RunWorkerCompletedEventArgs eventArgs)
{
// ...
}
}
```

```
public class PIDigitCalculator
{
// ...
}
```

# Establishing the Pattern

The process of hooking up the background worker pattern is as follows:

+   1. Register the long-running method with the BackgroundWorker.
+   DoWork event. In this example, the long-running task is the call to
+   CalculatePi().
+   
+   2. To receive progress or status notifications, hook up a listener to
+   BackgroundWorker.ProgressChanged and set Background-
+   Worker.WorkerReportsProgress to true. In Listing 19.8, the
+   UpdateDisplayWithMoreDigits() method takes care of updating
+   the display as more digits become available.
+   
+   3. Register a method (Complete()) with the BackgroundWorker.
+   RunWorkerCompleted event.
+   
+   4. Assign the WorkerSupportsCancellation property to support
+   cancellation. Once this property is assigned the value true,
+   a call to BackgroundWorker.CancelAsync will set the
+   DoWorkEventArgs.CancellationPending flag.
+   
+   5. Within the DoWork-provided method (CalculatePi()), check the
+   DoWorkEventArgs.CancellationPending property and exit the
+   method when it is true.