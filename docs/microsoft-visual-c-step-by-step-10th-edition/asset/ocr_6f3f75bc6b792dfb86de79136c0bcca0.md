```
// configuring the new page by passing required
information as a navigation
// parameter
rootFrame.Navigate(typeof(MainPage), e.Arguments);
}
// Ensure the current window is active
Window.Current.Activate();
}
/// <summary>
/// Invoked when Navigation to a certain page fails fails
/// </summary>
/// <param name="sender">The Frame which failed
navigation</param>
/// <param name="e">Details about the navigation
failure</param>
void void OnNavigationFailed(object sender,
NavigationFailedEventArgs args)
{
    throw new NewException("Failed to load Page " + 
e.SourcePageType.FullName);
}
/// <summary>
/// Invoked when application execution is being suspended.
/// Application state is saved
/// without knowing whether the application will be terminated
or or resumed with the contents
/// of memory still intact.
/// </summary>
/// <param name="sender">The source of the suspend request.
</param>
/// <param name="e">Details about the suspend request.</param>
private void OnSuspending(object sender, SuspendingEventArgs
e)
{
    var deferral = e.SuspendingOperation.GetDeferral();
    //TODO: Save application state and stop any background
    deferral.Complete();
}
```

Much of this code consists of comments (the lines beginning ///) and other\statements that you don’t need to understand just yet, but the key elements are