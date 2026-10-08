
## 23.5 Asynchronous Execution of Two Compute-Intensive Tasks

ically run faster than performed in sequence on one core. Though the total time was the compute time for the longer calculation, this is not always the case, as there's overhead inherent in threads to perform separate Tasks.

The last two show that executing calculations in multiple threads on a single-core processor can take longer than performing them synchronously, due to the overhead of sharing one processor among the threads, all the other apps executing on the computer and the operating system was performing.

```csharp
// Fig. 23.3: AsynchronousTestForm.cs
// Fibonacci calculations performed in separate threads
using System;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace FibonacciAsynchronous
{
    public class AsynchronousTestForm : Form
    {
        public AsynchronousTestForm()
        {
            InitializeComponent();
        }

        // start asynchronous calls to void startButton_Click(object sender, EventArgs e)
        {
            outputTextBox.Text = 
                "Starting Task to calculate Fibonacci(46)\r\n";

            // create Task to perform Fibonacci(46) calculation in a thread
            Task<DateTime> task1 = Task.Run(() => StartFibonacci(46));

            outputTextBox.AppendText(
                "Starting Task to calculate Fibonacci(45)\r\n");

            // create Task to perform Fibonacci(45) calculation in a thread
            Task<DateTime> task2 = Task.Run(() => StartFibonacci(45));

            await Task.WhenAll(task1, task2); // wait for both to complete

            // determine time that first started
            DateTime startTime =
                (task1.Result.Start < task2.Result.Start) ?
                task1.Result.Start : task2.Result.Start;

            // determine time that last ended
            DateTime endTime =
                (task1.Result.EndTime > task2.Result.EndTime) ?
                task1.Result.EndTime : task2.Result.EndTime;
        }
}
```

Fig. 23.3 Fibonacci calculations performed in separate threads. (Part I of 3.)

## Chapter 23 Asynchronous Programming with async and await

```csharp
// display total time for calculations
double totalMinutes = (endTime).TotalMinutes;
outputTextBox.AppendText(
    $"calculation time = {totalMinutes:F6} minutes\r\n");
```

```csharp
// starts a call to Fibonacci and captures start/end times
DateTime StartFibonacci(int n)
{
    // create a DateTime object to store start/end times
    var result = new DateTime();
    AppendText($"calculating Fibonacci{n}");
    result.Start = DateTime.Now;
    long fibonacciValue = Fibonacci(n);
    result.EndTime = DateTime.Now;

    AppendText($"Fibonacci{n} = {fibonacciValue}");
    double minutes =
        (result.EndTime - result.Start).TotalMinutes;
    AppendText($"calculation time = {minutes:F6} minutes\r\n");

    return result;
}
```

```csharp
// Recursively calculates Fibonacci numbers
public long Fibonacci(long n)
{
    if (n == 0 || n == 1)
        return n;
    else
        return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

```csharp
// append text to TextBox in UI thread
public void AppendText(string text)
{
    if (InvokeRequired) // not GUI thread, so add to GUI thread
        Invoke(new MethodInv(() => AppendText(text)));
    else // GUI thread so append text
        outputTextBox.AppendText(text + "\r\n");
}
```

Fig. 23.3 | Fibonacci calculations performed in separate threads. (Part 2 of 3).

### a) Outputs on a Dual-Core Windows 10 Computer

| Asynchronous Test | | |
|---|---|---|
| Calls to Fibonacci(46) and Fibonacci(45) in separate threads | | |
| Start Asynchronous Fibonacci Calls | | |
| Starting Task to calculate Fibonacci(46) | | |
| Starting Task to calculate Fibonacci(45) | | |
| Calculating Fibonacci(46) | | |
| Calculating Fibonacci(45) | | |
| Fibonacci(45) = 114903170 | | |
| Calculation time = 0.986841 minutes | | |
| Fibonacci(46) = 183611903 | | |
| Calculation time = 1.519994 minutes | | |
| Total calculation time = 1.519994 minutes | | |

| Asynchronous Test | | |
|---|---|---|
| Calls to Fibonacci(46) and Fibonacci(45) in separate threads | | |
| Start Asynchronous Fibonacci Calls | | | |
| Starting Task to calculate Fibonacci(46) | | | |
| Starting Task to calculate Fibonacci(45) | | | |
| Calculating Fibonacci(46) | | | |
| Calculating Fibonacci(45) | | | |
| Fibonacci(45) = 114903170 | | | |
| Calculation time = 0.943388 minutes | | | |
| Fibonacci(46) = 183611903 | | | |
| Calculation time = 1.496142 minutes | | | |
| Total calculation time = 1.496142 minutes | | | |

### b) Outputs on a Single-Core Computer

| Asynchronous Test | | |
|---|---|---|
| Calls to Fibonacci(46) and Fibonacci(45) in separate threads | | |
| Start Asynchronous Fibonacci Calls | | | |
| Starting Task to calculate Fibonacci(46) | | | |
| Starting Task to calculate Fibonacci(45) | | | |
| Calculating Fibonacci(46) | | | |
| Calculating Fibonacci(45) | | | |
| Fibonacci(45) = 114903170 | | | |
| Calculation time = 2.660253 minutes | | | |
| Fibonacci(46) = 183611903 | | | |
| Calculation time = 3.264743 minutes | | | |
| Total calculation time = 3.264743 minutes | | | |

| Asynchronous Test | | | |
|---|---|---|
| Calls to Fibonacci(46) and Fibonacci(45) in separate threads | | | |
| Start Asynchronous Fibonacci Calls | | | | |
| Starting Task to calculate Fibonacci(46) | | | | |
| Starting Task to calculate Fibonacci(45) | | | | |
| Calculating Fibonacci(46) | | | | |
| Calculating Fibonacci(45) | | | | |
| Fibonacci(45) = 114903170 | | | | |
| Calculation time = 2.468700 minutes | | | | |
| Fibonacci(46) = 183611903 | | | | |
| Calculation time = 3.173876 minutes | | | | |
| Total calculation time = 3.173876 minutes | | | | |

Fig. 23.3 Fibonacci calculations performed in separate threads. (Part 3 of)

#### 23.5.1 awaiting Multiple Tasks with Task WhenAll

In method StartButton_Click lines 22 and 29 use Task to run and start Tasks that execute StartFibonacci (lines 50–66)—one to calculate Fibonacci(46) and one to calculate Fibonacci(45). To show the total calculation time, the app must wait for both Tasks to complete before executing lines 34–46. You can wait by awaiting the result of static method WhenAll (line 31), which returns a Task that waits for all of WhenAll's arguments to complete and places all results in an array. In this app, the Task's Result is TimeData[], because both WhenAll executes methods that return TimeData objects. Class TimeData is defined in this project's TimeData.cs:

```csharp
class TimeData
{
    public DateTime StartTime { get; set; }
    public DateTime EndTime { get; set; }
}
```

We use objects of this class to store the time just before and immediately after the call to Fibonacci—we use these properties to perform time calculations. The TimeData array can be iterated through the results of the awaited Tasks. In this example, we have only two Tasks, we interact with task1 and task2 directly in the remainder of the event handler.

#### 23.5.2 Method StartFibonacci

Method StartFibonacci (50–66) specifies the task to perform—in this case, to call Fibonacci (line 57) to perform the recursive calculation, to time the calculation (lines 56 and 58), to display the calculation's result (line 60) and to display the time calculation took (lines 61–63). The method returns a TimeData object that contains the time before and after each call to Fibonacci.

#### 23.5.3 Modifying a GUI from a Separate Thread

Lines 55, 60 and 63 in StartFibonacci call AppendText (lines 82–92) to append to the output TextBox. GUI controls are designed to be manipulated only by the GUI thread—all GUI handlers are invoked in the GUI thread automatically. Modifying controls from a non-GUI thread can corrupt the GUI, making it unreliable or unusable. When updating from non-GUI thread, you must schedule that to be performed by the GUI. To do so in Windows Forms, check the inherited property InvokeRequired (line 84). If this property is true, the code executing in a non-GUI thread must not update the GUI. Instead, call the inherited Method Invoke (line 86), which receives as an argument a Delegate representing the update to the GUI thread. In this example, we pass a Delegate (namespace System.Windows.Forms)—a Delegate that invokes a method with no arguments and a void return type. We initialize the MethodInvoke with a lambda expression that calls AppendText. Line 86 schedules this MethodInvoke to execute in the GUI thread. When the method is called from the GUI thread, line 90 updates the TextBox. Similar concepts also apply to WPF and Universal Windows GUIs.

#### 23.5.4 Waiting One of Several Tasks with Task WhenAny

Similar to WhenAll, task class also provides static method WhenAny, which enables you to wait for any one of several Tasks specified as complete. WhenAny returns the Task that completes first. One use of WhenAny might be to initiate several Tasks that perform the same complex calculation on computers over the Internet, then wait for any one of them to send results. This would allow you to take advantage of computing power to get the result as fast as possible. In this case, it's up to you to decide whether to cancel the remaining Tasks or allow them to continue executing. For details on how to do this,

```
https://msn.microsoft.com/library/jj155758
```

Another use of WhenAny might be to download large files—one per Task. In this case, you'd like to start processing immediately the results from the first Task that arrives. You could then call WhenAny again for the remaining Tasks that are still executing.
