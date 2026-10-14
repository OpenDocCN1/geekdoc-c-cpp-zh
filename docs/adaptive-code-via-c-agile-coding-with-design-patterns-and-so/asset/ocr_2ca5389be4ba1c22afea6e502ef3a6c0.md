Note that you could have chosen to implement IStopwatch as a subclass of the System.Diagnostics.Stopwatch class and used the existing Start and Stop methods. However, the Start method acts to resume functionality when a stopwatch is stopped, but what you need to do is to call Reset after you call Stop, and retrieve the ElapsedMilliseconds property value in between. This is another example of the Adapter pattern.

# Asynchronous decorators

Asynchronous methods are those that run on a different thread than the client. This is useful when a method takes a long time to execute because, during synchronous execution, the client is blocked while waiting for a called method to return. In a desktop application using Windows Presentation Foundation (WPF) and the Model-View-ViewModel (MVVM) pattern, for example, the ViewModels are bound to the View, and any commands that are executed are handled synchronously by those ViewModels on the user interface thread. In practice, this means that a long-running command will block the user interface from executing for as long as the command takes to finish its work. Listing 5-31 shows a snippet of this behavior.

**LISTING 5-31** Commands handled on the UI thread will block it, making the UI unresponsive.

[Click here to view code image](#)

```
public class MainWindowViewModel : INotifyPropertyChanged
{
    public MainWindowViewModel(IComponent component)
    {
        this.component = component;
        calculateCommand = new RelayCommand(Calculate);
    }

    public string Result
    {
        get
        {
            return result;
        }
        private set
        {
            if (result != value)
            {
                result = value;
                PropertyChanged(this, new PropertyChangedEventArgs("Result"));
            }
        }
    }

    public ICommand CalculateCommand
```