to this page, a Button to allow the user to navigate to Page2, and a TextBox to allow the user to enter some state information that should be saved when the app is terminated (code file ApplicationLifetimeSample/Page1.xaml):

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
```