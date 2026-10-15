# D.

# Timers Prior to the Async/Await Pattern of C# 5.0

CHAPTER 19 INTRODUCED THE USE of Task.Delay() when a timer was required. For scenarios prior to .NET 4.5, several timer classes are available, including System.Windows.Forms.Timer, System.Timers.Timer, and System.Threading.Timer.

The development team designed System.Windows.Forms.Timer specifically for use within a rich client user interface. Programmers can drag it onto a form as a nonvisual control and regulate the behavior from within the Properties window. Most importantly, it will always safely fire an event from a thread that can interact with the user interface.

The other two timers are very similar. System.Timers.Timer is a wrapper for System.Threading.Timer, abstracting and layering on functionality. Specifically, System.Threading.Timer does not derive from System.ComponentModel.Component, and therefore, you cannot use it as a component within a component container, something that implements System.ComponentModel.IContainer. Another difference is that System.Threading.Timer enables the passing of state, an object parameter, from the call to start the timer and then into the call that fires the timer notification. The remaining differences simply concern API usability, with System.Timers.Timer supporting a synchronization object and having calls that are slightly more intuitive. Both System.Timers.Timer and System.Threading.Timer are designed for use in server-type processes,