```
protected virtual void OnPropertyChanged(
    [CallerMemberName] string propertyName = null)
{
    PropertyChanged?.Invoke(this, new
PropertyChangedEventArgs(propertyName));
}

// etc.
}
```

> NOTE The interface INotifyPropertyChanged is discussed in Chapter 31, “Patterns with XAML Apps,” to implement change notifications.

# Overriding Page Class Navigation

The Page class that is the base class of BasePage (and the base class of XAML pages) defines methods that are used on navigation. The method OnNavigatedTo is invoked when the page is navigated to. Within this page you can read how the navigation was done (NavigationMode property) and parameters for the navigation. The method OnNavigatingFrom is the first method that is invoked when you navigate away from the page. Here, the navigation can be cancelled. The method OnNavigatedFrom is finally invoked when you navigate away from this page. Here, you should do some cleanup of resources that have been allocated with the OnNavigatedTo method (code file PageNavigation/App.xaml.cs):

```
public abstract class BasePage : Page, INotifyPropertyChanged
{
    // etc.
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        base.OnNavigatedTo(e);

        NavigationMode = $"Navigation Mode: {e.NavigationMode}";
        // etc.
    }

    protected override void
OnNavigatingFrom(NavigatingCancelEventArgs e)
    {
        base.OnNavigatingFrom(e);
    }

    protected override void OnNavigatedFrom(NavigationEventArgs e)
    {
        base.OnNavigatedFrom(e);
        // etc.
    }
}
```

# Navigating Between Pages

Let’s implement the three pages. For using the BasePage class, the code-behind file needs to be modified to use the BasePage as a base class