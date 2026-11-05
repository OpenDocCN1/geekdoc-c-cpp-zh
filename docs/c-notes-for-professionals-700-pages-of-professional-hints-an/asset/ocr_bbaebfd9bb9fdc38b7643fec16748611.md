# Chapter 110: Timers

# Section 110.1: Multithreaded Timers

System.Threading.Timer - Simplest multithreaded timer. Contains two methods and one constructor.

Example: A timer calls the DataWrite method, which writes "multithread executed..." after five seconds have elapsed, and then every second after that until the user presses Enter:

```
using System;
using System.Threading;
class Program
{
    static void Main()
    {
        // First interval = 5000ms; subsequent intervals = 1000ms
        Timer timer = new Timer(DataWrite, "multithread executed...", 5000, 1000);
        Console.ReadLine();
        timer.Dispose(); // This both stops the timer and cleans up.
    }

    static void DataWrite(object data)
    {
        // This runs on a pooled thread
        Console.WriteLine(data); // Writes "multithread executed..."
    }
}
```

Note : Will post a separate section for disposing multithreaded timers.

Change - This method can be called when you would like change the timer interval.

Timeout.Infinite - If you want to fire just once. Specify this in the last argument of the constructor.

System.Timers - Another timer class provided by .NET Framework. It wraps the System.Threading.Timer.

# Features:

+   - IComponent - Allowing it to be sited in the Visual Studio's Designer's component tray
+   - Interval property instead of a Change method
+   - Elapsed event instead of a callback delegate
+   - Enabled property to start and stop the timer (default value = false)
+   - Start & Stop methods in case if you get confused by Enabled property (above point)
+   - AutoReset - for indicating a recurring event (default value = true)
+   - SynchronizingObject property with Invoke and BeginInvoke methods for safely calling methods on WPF elements and Windows Forms controls

Example representing all the above features:

```
using System;
using System.Timers; // Timers namespace rather than Threading
class SystemTimer
{
    static void Main()
    {
        Timer timer = new Timer(); // Doesn't require any args
        timer.Interval = 500;
    }
}
```