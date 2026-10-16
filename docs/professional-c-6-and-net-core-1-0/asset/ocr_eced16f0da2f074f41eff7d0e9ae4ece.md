```
// Place the frame in the current Window
Window.Current.Content = rootFrame;
}

if (rootFrame.Content == null)
{
    rootFrame.Navigate(typeof(MainPage), e.Arguments);
}
Window.Current.Activate();
}
```

# Testing Suspension

Now you can start the application (see Figure 33.1), navigate to another page, and then open other applications to wait until the application is terminated. With the Task Manager, you can see the suspended applications with the Details view if the Status Values option is set to Show Suspended Status. This is not an easy way to test suspension (because it can take a long time before the termination happens), however, and it would be nice to debug the different states.

![](bbox=[0.105, 0.383, 0.895, 0.595])

Figure 33.1

When you use the debugger, everything works differently. If the application would be suspended as soon as it doesn’t have a focus, it would be suspended every time a breakpoint is reached. That’s why suspension is disabled while running under the debugger. So the normal suspension mechanism doesn’t apply. However, it’s easy to simulate. If you open the Debug Location toolbar, there are three buttons for Suspend, Resume, and Suspend and shutdown (see Figure 33.2). If you click Suspend and shutdown and then start the application again, the application continues from the previous state of ApplicationExecutionState.Terminated and thus opens the page the user opened previously.