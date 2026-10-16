![](bbox=[0.285, 0.062, 0.715, 0.51])

# Figure 32.10

The sample application, which uses the SplitView and hamburger button, adds some more features. When navigating between multiple pages using a menu, it’s a good idea to have the menu available in all the pages. Navigation works using methods of the Frame class, as you’ve seen in the “Navigation” section earlier in this chapter. You can create a page and use it as an application shell, and you can add a frame in the content of the SplitView. The AppShellSample app demonstrates how you can do this.

With the template-generated code, in the OnLaunched method of the App class a Frame object is created, and the frame navigates to the MainPage. This code is changed to create an AppShell and use the frame from within the AppShell (shell.AppFrame) to navigate to the MainPage (code file AppShellSample/App.xaml.cs):

```
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    AppShell shell = Window.Current.Content as AppShell;

    if (shell == null)
    {
        shell = new AppShell();
        shell.Language = ApplicationLanguages.Languages[0];
        shell.AppFrame.NavigationFailed += OnNavigationFailed;
```