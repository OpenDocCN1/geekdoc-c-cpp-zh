
## Barrier

```csharp
for (int i = 0; i < taskCount; i++)
{
    Console.WriteLine("{0}* task for {1}, result: {1}", i, calcs[i].Result);
}
```

For synchronization, .NET 4 offers the new Barrier class. Barrier is great for a scenario where work is forked into multiple tasks, and the work needs to be joined afterward. Barrier is used for participants need to be synchronized. While the job is active, additional participants can be added dynamically, for example, child tasks that are created from a parent task. Participants can wait until the work is done by all the other participants before continuing.

The sample application uses a collection containing 2,000,000 strings. Multiple tasks are used to iterate through the collection and count the number of strings starting with a, b, c, and so on.

The method FillData() creates a collection and fills it with random strings.

```csharp
public static IEnumerable<string> FillData(int size)
{
    List<string> data = new List<string>(size);
    Random r = new Random();
    for (int i = 0; i < size; i++)
    {
        data.Add(GetString(r));
    }
    return data;
}
private static string GetString(Random r)
{
    StringBuilder sb = new StringBuilder(6);
    for (int i = 0; i < 6; i++)
    {
        sb.Append((char)(r.Next(26) + 97));
    }
    return sb.ToString();
}
```

The CalculationInTask() method defines the job that's done by a task. With the parameter, a tuple containing four items is received. The third parameter is a reference to the Barrier instance. When the job is done by the task, the task removes itself from the barrier with the RemoveParticipant() method.

```csharp
static int[] CalculationInTask(object p)
{
    var p1 = p as Tuple<int, int, Barrier, List<string>>;
    Barrier barrier = p1.Item3;
    List<string> data = p1.Item4;

    int start = p1.Item1 * p1.Item2;
    int end = start + p1.Item2;
    Console.WriteLine("Task {0}: partition from {1} to {2}*", Task.CurrentId, start, end);
    int[] charCount = new int[26];
    for (int j = start; j < end; j++)
    {
        char c = data[j][0];
        charCount[c - 97]++;
    }
```

```
Writer 2 waiting for the write lock
current reader count: 4
reader 4, loop: 3, item: 4
reader 1, loop: 3, item: 4
reader 2, loop: 3, item: 4
reader 3, loop: 3, item: 4
reader 4, loop: 4, item: 5
reader 1, loop: 4, item: 5
Writer 2 waiting for the write lock
current reader count: 4
reader 2, loop: 4, item: 5
reader 3, loop: 4, item: 5
reader 4, loop: 5, item: 6
reader 1, loop: 5, item: 6
reader 2, loop: 5, item: 6
reader 3, loop: 5, item: 6
Writer 2 waiting for the write lock
current reader count: 4
Writer 2 acquired the lock
Writer 2 finished
```

## TIMERS

The .NET Framework offers several Timer classes that can be used to invoke a method after some time interval. The following table lists the Timer classes and their namespaces, as well as their functionality.

| NAMESPACE | DESCRIPTION |
|---|---|
| System.Threading | The Timer class from the System.Threading namespace offers core functionality. In the constructor, you can pass a delegate that should be invoked at the time interval specified. |
| System.Timers | The Timer class from the System.Timers namespace is a component, because it derives from the Component base class. So, you can drag and drop it from the toolbox to the design surface of a server application such as a Windows service. This Timer class uses System.Threading.Timer but provides an event-based mechanism instead of a delegate. |
| System.Windows.Forms | With the Timer classes from the namespaces System.Threading and System.Timers, the callback or event methods are invoked from a different thread than the calling thread. Windows Forms controls are bound to the creator thread. Calling back into this thread is done by the Timer class from the System.Windows.Forms namespace. |
| System.Web.UI | The Timer from the System.Web.UI namespace is an AJAX Extension that can be used with web pages. |
| System.Windows.Threading | The DispatcherTimer class from the System.Windows.Threading namespace is used by WPF applications. DispatcherTimer runs on the UI thread. |

Using the System.Threading.Timer class, you can pass the method to be invoked as the first parameter in the constructor. This method must fulfill the requirements of the TimerCallback delegate, which defines a void return type and an object parameter. With the second parameter, you can pass any object, which is then received with the object argument in the callback method. For example, you can pass an Event object to signal the caller. The third parameter specifies the time span during which the callback should be invoked the first time. With the last parameter, you specify the repeating interval for the callback. If the timer should fire only once, set the fourth parameter to the value -1.

If the time interval should be changed after creating the Timer object, you can pass new values with the Change() method.

```csharp
private static void ThreadingTimer()
{
    var t1 = new System.Threading.Timer(
        TimeAction, null, TimeSpan.FromSeconds(2),
        TimeSpan.FromSeconds(3));

    Thread.Sleep(15000);

    t1.Dispose();
}

static void TimeAction(object o)
{
    Console.WriteLine("System.Threading.Timer {0:T}", DateTime.Now);
}
```

*code snippet TimerSampleProgram.cs*

The constructor of the Timer class from the System.Timers namespace requires just a time interval. The method that should be invoked after the interval is specified by the Elapsed event. This event requires a delegate of type ElapsedEventHandler, which requires object and ElapsedEventArgs parameters, as you can see with the TimeAction method. The AutoReset property specifies whether the timer should be fired repeatedly. If you set this property to false, the event is fired only once. Calling the Start method enables the timer to fire the events. Instead of calling the Start method, you can set the Enabled property to true. Behind the scenes Start() does nothing else. The Stop() method sets the Enabled property to false to stop the timer.

```csharp
private static void TimersTimer()
{
    var t1 = new System.Timers.Timer(1000);
    t1.AutoReset = true;
    t1.Elapsed += TimeAction;
    t1.Start();
    Thread.Sleep(10000);
    t1.Stop();

    t1.Dispose();
}

static void TimeAction(object sender, System.Timers.ElapsedEventArgs e)
{
    Console.WriteLine("System.Timers.Timer {0:T}", e.SignalTime);
}
```

## EVENT-BASED ASYNCHRONOUS PATTERN

Earlier in this chapter, you saw the asynchronous pattern based on the IAsyncResult interface. With an asynchronous callback, the callback thread is different from the calling thread. Using Windows Forms or WPF, this is a problem, because Windows Forms and WPF controls are bound to a single thread. With every control, you can invoke methods only from the thread that created the control. This also means that if you have a background thread, you can only directly access the UI controls from this thread.

The only methods with Windows Forms controls that you can invoke from a different thread than the creator thread are Invoke(), BeginInvoke(), EndInvoke(), and the property InvokeRequired. BeginInvoke() and EndInvoke() are asynchronous variants of Invoke(). These methods switch to the creator thread to invoke the method that is assigned to a delegate parameter that you can pass to these methods. Using these

methods is not that easy, which is why beginning with .NET 2.0 a new component, together with a new asynchronous pattern, was added: the event-based asynchronous pattern.

With the event-based asynchronous pattern, the asynchronous component offers a method with the suffix Async; for example, the synchronous method DoTask() has the name DoTaskAsync() in the asynchronous version. To get the result information, the component also needs to define an event that has the suffix Completed, for example, DoTaskCompleted. While the action happening in the DoTaskAsync() method is running in a background thread, the event DoTaskCompleted is fired in the same thread as the caller.

With the event-based asynchronous pattern, the asynchronous component optionally can support cancellation and information about progress. For cancellation, the method should have the name CancelAsync(), and for progress information, an event with the suffix ProgressChanged, for example, DoTaskProgressChanged, is provided.

## BackgroundWorker

The BackgroundWorker class is one implementation of the asynchronous event pattern. The method RunWorkerAsync() starts the method that is associated with the DoWork event asynchronously. As soon as the work is done, the event RunWorkerCompleted is fired. The names used here are in complete conformance with the event-based asynchronous pattern naming explained earlier.

The BackgroundWorker might also support cancellation if the property WorkerSupportsCancellation is set to true. In that case, the work can be canceled by invoking the CancelAsync method. However, the job that is done needs to check for the CancellationPending property to verify if it should stop its work. Similar to the new cancellation framework, the BackgroundWorker supports cooperative cancellation.

Displaying progress information, the BackgroundWorker also does a useful job. The property WorkerReportsProgress provides information if the task at work returns progress information. If that's the case, the ProgressChanged event can be assigned to receive information about progress changes. The job that does the work needs to report progress by calling the method ReportProgress() with the percentage of completed information.

> > Another class that implements the asynchronous event pattern is the component WebClient in the System.Net namespace. This class uses the WebRequest and WebResponse classes but provides an easier-to-use interface. The WebRequest and WebResponse classes also offer asynchronous programming, but here it is based on the asynchronous pattern with the IAsyncResult interface.

The sample application demonstrates the use of the BackgroundWorker control in a WPF application by doing a task that takes some time. Create a new WPF application, and add three Label controls, three TextBox controls, two Button controls, and one ProgressBar to the window, as you can see for the running application in Figure 20-3. Configure the properties of the controls as listed in the following table.

| CONTROL | PROPERTY AND EVENTS | VALUE |
|---|---|---|
| Label | Content | X: |
| TextBox | x:Name | textX |
| Label | Content | Y: |
| TextBox | x:Name | textY |

![](img/d7d2ffa0a76feaab821930e95daace93_596_0.png)

FIGURE 20-3
