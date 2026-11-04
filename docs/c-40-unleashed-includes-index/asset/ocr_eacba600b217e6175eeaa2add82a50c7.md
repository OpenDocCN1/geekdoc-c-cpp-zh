# DON'T CATCH ALL (AGAIN)

Based on the discussion in the previous section, you should be discouraged from catching all exceptions already. Some simply cannot be caught, and others should be propagated to the caller to take meaningful action, if possible. Very few exceptions to this rule exist, and I won't try to define such exceptions here.

# Beyond Your Control

Catching exceptions using try statements works only if your code appears somewhere higher up on the call stack. After all, a protected block protects only the code that runs inside it. You don't possess magical powers to stretch an exception handler around code that is not yours, somewhere in an unrelated corner of the system.

A typical source of such practical issues is in UI programming, where a dispatcher is used to run work on behalf of the user, on the right thread and with a specified right priority. The code that dispatches work items that have been scheduled is beyond your control. For example, in Windows Presentation Foundation (WPF), it's the application's Run method that starts the dispatcher. We talk more about the dispatcher's role when covering WPF in more detail. For now, just focus on the following little example:

```
private void crash_Click(object sender, RoutedEventArgs e) {
    Dispatcher.BeginInvoke(new Action(() => {
        throw new Exception("Oops!"); })
    );
}
```

Here we're scheduling background work through the dispatcher, allowing the event handler for the crash button to return immediately. At some point in the future, this work item will be picked up by the dispatcher, causing the delegate to be called. The call stack at the point of the crash will look roughly like this:

```
WpfApplication1.exe!WpfApplication1.MainWindow.crash_Click.AnonymousMethod__0
...
WindowsBase.dll!System.Windows.Threading.Dispatcher.Run
...
PresentationFramework.dll!System.Windows.Application.Run
WpfApplication1.exe!WpfApplication1.App.Main
```

At the top, we see our anonymous method containing the code passed to BeginInvoke. This was called by the dispatcher somehow, through all the machinery hidden behind the Application.Run call made by the application's Main method. There's no apparent place to handle such an exception. One thing we can do is make sure the delegates posted through BeginInvoke do not crash for avoidable reasons. This is by far the best solution. However, in some cases, it makes