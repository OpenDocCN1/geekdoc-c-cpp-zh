different from the lifetime of desktop applications.

# App Lifetime

Windows 8 introduced a new life cycle for apps that is completely different from the life cycle of desktop applications. This changed a little with Windows 8.1, and again with Windows 10. If you’re using Windows 10 and *tablet mode*, the life cycle of the app is different compared to *desktop mode*. With tablet mode, apps are typically full-screen. You can either switch to tablet mode automatically by detaching the keyboard (with tablet devices such as the Microsoft Surface), or by using the Tablet Mode button in the Action Center. When you run an application in tablet mode, the app gets suspended if it moves to the background (the user switches to another app), and it doesn’t get any more CPU utilization. This way the app doesn’t consume any battery. The app just uses memory while it’s in the background and gets activated again as soon as the user switches to this app.

In case memory resources are low, Windows can terminate suspended applications. To terminate an app, the process is killed. No information is sent to the application, so it cannot react to this event. That’s why an application should act on the suspended event and save its state there. Upon termination it is too late to save the state.

When receiving the suspended event, an app should store its state on disk. If the app is started again, the app can present itself to the user as if it was never terminated. You just need to store information about the page stack to navigate the user to the page where he or she left off, allow the user to go back by restoring the page back stack, and initialize the fields to the data the user entered.

The sample app for this section—`ApplicationLifetimeSample`—does exactly this. With this app, multiple pages allow navigation between the pages, and the state can be entered. The page stack is stored and state is stored when the app is suspended, and both are restored when the app is started.

# Application Execution States

States of the application are defined with the ApplicationExecutionState enumeration. This enumeration defines the states NotRunning, Running, Suspended, Terminated, and ClosedByUser. The application needs to be aware of and store its state, as users returning to the application expect to continue where they left it previously.

With the OnLaunched method in the App class, you can get the previous execution state of the application with the PreviousExecutionState property of the LaunchActivatedEventArgs argument. The previous execution state is NotRunning if the application is being started for the first time after installing it, or after a