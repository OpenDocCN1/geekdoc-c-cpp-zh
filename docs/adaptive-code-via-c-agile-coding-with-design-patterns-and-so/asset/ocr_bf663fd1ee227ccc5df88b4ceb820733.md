```
{
    get
    {
        return calculateCommand;
    }
}

public event PropertyChangedEventHandler PropertyChanged = delegate {};

private void Calculate(object parameter)
{
    Result = "Processing...";
    component.Process();
    Result = "Finished!";
}

private string result;
private IComponent component;
private RelayCommand calculateCommand;
}
```

By creating an asynchronous decorator, you can instruct the called method to execute on a separate thread. This can be accomplished by delegating the work to a Task class, which becomes a dependency of your decorator, as Listing 5-32 shows.

# LISTING 5-32 An asynchronous decorator for WPF that uses the Dispatcher class.

Click here to view code image

```
public class AsyncComponent : IComponent
{
    public AsyncComponent(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }

    public void Process()
    {
        Task.Run((Action)decoratedComponent.Process);
    }

    private readonly IComponent decoratedComponent;
}
```