# 210 | CHAPTER 12 RESOURCES

The Window's constructor creates a new Timer that fires every 1,000 milliseconds (i.e., every second). The event handler tmClock_Elapsed to handle the Timer's Elapsed events and enables the Timer. It finishes by calling SetTimeResource to display the initial time.

When the Timer raises its Elapsed event, the event handler runs in a different thread of execution from the code that manages the user interface (UI) and controls. Windows does not allow code to directly access UI objects from a separate thread, so the program must use the Invoke method to make the Dispatcher object running the UI thread run. In this example, the code uses Invoke to execute the SetTimeResource function on the UI thread.

> INDIRECT INVOCATION
Contrast this to Invoke with the constructor's initial call to SetTimeResource. The constructor is running in the same thread as the UI objects, so it can call SetTimeResource directly. Later, when the Timer fires its event, it is running on a separate thread, so it must use Invoke.

The function SetTimeResource removes the TimeNow resource from the Window's resource dictionary and re-adds it with a new value showing the current time.

Figure 12-11 shows the SimpleClock program on top of the Windows 7 Desktop Background applet. The users (Right-click on the desktop, select Personalize, and click on the "Desktop Background" link.) You may want to refer back to the XAML code as you review this figure.

![](bbox=[0.115, 0.568, 0.745, 0.908])

FIGURE 12-11