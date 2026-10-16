
different from the lifetime of desktop applications.

## App Lifetime

Windows 8 introduced a new life cycle for apps that is completely different from the life cycle of desktop applications. This changed a little with Windows 8.1, and again with Windows 10. If you’re using Windows 10 and *tablet mode*, the life cycle of the app is different compared to *desktop mode*. With tablet mode, apps are typically full-screen. You can either switch to tablet mode automatically by detaching the keyboard (with tablet devices such as the Microsoft Surface), or by using the Tablet Mode button in the Action Center. When you run an application in tablet mode, the app gets suspended if it moves to the background (the user switches to another app), and it doesn’t get any more CPU utilization. This way the app doesn’t consume any battery. The app just uses memory while it’s in the background and gets activated again as soon as the user switches to this app.

In case memory resources are low, Windows can terminate suspended applications. To terminate an app, the process is killed. No information is sent to the application, so it cannot react to this event. That’s why an application should act on the suspended event and save its state there. Upon termination it is too late to save the state.

When receiving the suspended event, an app should store its state on disk. If the app is started again, the app can present itself to the user as if it was never terminated. You just need to store information about the page stack to navigate the user to the page where he or she left off, allow the user to go back by restoring the page back stack, and initialize the fields to the data the user entered.

The sample app for this section—`ApplicationLifetimeSample`—does exactly this. With this app, multiple pages allow navigation between the pages, and the state can be entered. The page stack is stored and state is stored when the app is suspended, and both are restored when the app is started.

## Application Execution States

States of the application are defined with the ApplicationExecutionState enumeration. This enumeration defines the states NotRunning, Running, Suspended, Terminated, and ClosedByUser. The application needs to be aware of and store its state, as users returning to the application expect to continue where they left it previously.

With the OnLaunched method in the App class, you can get the previous execution state of the application with the PreviousExecutionState property of the LaunchActivatedEventArgs argument. The previous execution state is NotRunning if the application is being started for the first time after installing it, or after a reboot, or when the user stopped the process from the Task Manager. The application is in the Running state if it was already running when the user activated it from a second tile or it’s activated by one of the activation contracts. The PreviousExecutionState property returns Suspended when the application was suspended previously. Usually there’s no need to do anything special in that case as the state is still available in memory. While in a suspended state, the app doesn’t use any CPU cycles, and there’s no disk access.

> NOTE The application can implement one or more activation contracts and then can be activated with one of these. An example of such a contract is share. With this contract, the user can share some data from another application and start a UWP app by using it as a share target. Implementing the share contract is shown later in this chapter in the “Sharing Data” section.

## Navigation Between Pages

The sample application for demonstrating the life cycle of Windows apps (`ApplicationLifetimeSample`) is started with the Blank App template. After creating the project, you add the pages Page1 and Page2 to implement navigation between the pages.

To the `MainPage`, you add two `Button` controls for navigation to Page1 and Page2 and two `TextBox` controls to allow passing data with the navigation (code file `ApplicationLifetimeSample/MainPage.xaml`):

```
<Button Content="Page 1" Click="{x:Bind GotoPage1}" Grid.Row="0" />
<TextBox Text="{x:Bind Parameter1, Mode=TwoWay}" Grid.Row="0" Grid.Column="1" />
<Button Content="Page 2" Click="{x:Bind GotoPage2}" Grid.Row="1" />
<TextBox Text="{x:Bind Parameter2, Mode=TwoWay}" Grid.Row="1" Grid.Column="1" />
```

The code-behind file contains the event handler with navigation code to Page1 and Page2 and properties for the parameters (code file `ApplicationLifetimeSample/MainPage.xaml.cs`):

```
public void GotoPage1()
{
    Frame.Navigate(typeof(Page1), Parameter1);
}

public string Parameter1 { get; set; }

public void GotoPage2()
{
    Frame.Navigate(typeof(Page2), Parameter2);
}

public string Parameter2 { get; set; }
```

The UI elements for Page1 show the data that is received on navigating to this page, a Button to allow the user to navigate to Page2, and a TextBox to allow the user to enter some state information that should be saved when the app is terminated (code file ApplicationLifetimeSample/Page1.xaml):

```
<TextBlock FontSize="30" Text="Page 1" />
<TextBlock Grid.Row="1" Text="{x:Bind ReceivedContent, Mode=OneTime}" />
<TextBox Grid.Row="2" Text="{x:Bind Parameter1, Mode=TwoWay}" />
<Button Grid.Row="3" Content="Navigate to Page 2" Click="{x:Bind GotoPage2, Mode=OneTime}" />
```

Similar to the MainPage, the navigation code for Page1 defines an auto-implemented property for the data that is passed with the navigation and an event handler implementation for navigating to Page2 (code file ApplicationLifetimeSample/Page1.xaml.cs):

```
public void GotoPage2()
{
    Frame.Navigate(typeof(Page2), Parameter1);
}

public string Parameter1 { get; set; }
```

With the code-behind file, the navigation parameter is received in the OnNavigatedTo method override. The received parameter is assigned to the auto-implemented property ReceivedContent (code file ApplicationLifetimeSample/Page1.xaml.cs):

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);
    //...
    ReceivedContent = e.Parameter?.ToString() ?? string.Empty;
    Bindings.Update();
}

public string ReceivedContent { get; private set; }
```

With the implementation of the navigation, Page2 is very similar to Page1, so I’m not repeating its implementation here.

Using the system back button is covered in Chapter 32, “Windows Apps: User Interfaces.” Here, the visibility and handler of the back button is defined in the class BackButtonManager. The implementation of the constructor makes the back button visible if the CanGoBack property of the frame instance returns true. The method OnBackRequested is implemented to go back in the page stack if the stack is available (code file ApplicationLifetimeSample/Utilities/BackButtonManager.cs):

```
public class BackButtonManager: IDisposable
{
    private SystemNavigationManager _navigationManager;
    private Frame _frame;

    public BackButtonManager(Frame frame)
    {
        _frame = frame;
        _navigationManager =
SystemNavigationManager.GetForCurrentView();
        _navigationManager.AppViewBackButtonVisibility =
frame.CanGoBack ?
    AppViewBackButtonVisibility.Visible:
    AppViewBackButtonVisibility.Collapsed;
        _navigationManager.BackRequested += OnBackRequested;
    }

    private void OnBackRequested(object sender,
BackRequestedEventArgs e)
    {
        if (_frame.CanGoBack) _frame.GoBack();
        e.Handled = true;
    }

    public void Dispose()
    {
        _navigationManager.BackRequested -= OnBackRequested;
    }
}
```

With all the pages, the BackButtonManager is instantiated by passing the Frame in the OnNavigatedTo method, and it’s disposed in the OnNavigatedFrom method (code file ApplicationLifetimeSample/MainPage.xaml.cs):

```
private BackButtonManager _backButtonManager;
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);
    _backButtonManager = new BackButtonManager(Frame);
}

protected override void
OnNavigatingFrom(NavigatingCancelEventArgs e)
{
    base.OnNavigatingFrom(e);
    _backButtonManager.Dispose();
}
```

With all this code in place, the user can navigate back and forward between the three different pages. What needs to be done next is to remember the page and the page stack to navigate the app to the page the user accessed most recently.

## Navigation State

To store and load the navigation state, the class NavigationSuspensionManager defines the methods SetNavigationStateAsync and GetNavigationStateAsync. The page stack for the navigation can be represented in a single string. This string is written to a local cache file named as defined by a constant. In case the file already exists from a previous app run, it is just overwritten. You don’t need to remember page navigations between multiple app runs (code file ApplicationLifetimeSample/Utilities/NavigationSuspensionManager.
