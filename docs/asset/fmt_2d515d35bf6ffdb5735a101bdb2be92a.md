
```csharp
...
using System.ComponentModel;

namespace Customers
{
    public class ViewModel : INotifyPropertyChanged
    {
        ...
    }
}

public class ViewModel : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;
    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}

public class ViewModel : INotifyPropertyChanged
{
    ...
    public ViewModel()
    {
        ...
    }
}
```

```csharp
private bool _isAtStart;
public bool IsAtStart
{
    get => this._isAtStart;
    set {
        this._isAtStart = value;
        this.OnPropertyChanged(nameof(IsAtStart));
    }
}
```

```csharp
private bool _isAtEnd;
public bool IsAtEnd
{
    get => this._isAtEnd;
    set {
        this._isAtEnd = value;
        this.OnPropertyChanged(nameof(IsAtEnd));
    }
}
```

```csharp
public class ViewModel()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.customers = new List<Customer>
    ...
};
```

```csharp
public class ViewModel : INotifyPropertyChanged
{
    public Customer Current
    {
        ...
    }
}
```

```csharp
private void Next()
{
    if (this.customers.Count - 1 > this.currentCustomer)
    {
        this.currentCustomer++;
        this.OnPropertyChanged(nameof(Current));
        this.IsAtStart = false;
        this.IsAtEnd = (this.customers.Count - 1 == this.currentCustomer);
    }
}
```

```csharp
private void Previous()
{
    if (this.currentCustomer > 0)
    {
        this.currentCustomer--;
        this.OnPropertyChanged(nameof(Current));
        this.IsAtEnd = false;
        this.IsAtStart = (this.currentCustomer == 0);
    }
}
```

```csharp
public class ViewModel : INotifyPropertyChanged
{
    private List<Customer> customers;
    private int currentCustomer;
    public Command NextCustomer { get; private set; }
    public Command PreviousCustomer { get; private set; }
}
```

```csharp
public class ViewModel()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.customers = new List<Customer>
    ...
};
```

()()

    this.    ExecuteExecute

...

 =

Execute;

    }

    this.canExecuteChangedTimer = new DispatcherTimer();

    this.canExecuteChangedTimer.Tick +=

        canExecuteChangedEventTimer_Tick;

    this.canExecuteChangedTimer.Interval = new TimeSpan(0, 0, 1);

    this.canExecuteChangedTimer.Start();

}

...
```

```csharp

...

using System.ComponentModel;

namespace Customers

{

    public class ViewModel : INotifyPropertyChanged

    {

        ...

    }

}

public class ViewModel : INotifyPropertyChanged

{

    ...

    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)

    {

        if (PropertyChanged != null)

        {

            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));

        }

    }

}

public class ViewModel : INotifyPropertyChanged

{

    ...

    public ViewModel()

    {

        ...

    }

}

```

```csharp

private bool _isAtStart;

public bool IsAtStart

{

    get => this._isAtStart;

    set {

        this._isAtStart = value;

        this.OnPropertyChanged(nameof(IsAtStart));

    }

}

```

```csharp

private bool _isAtEnd;

public bool IsAtEnd

{

    get => this._isAtEnd;

    set {

        this._isAtEnd = value;

        this.OnPropertyChanged(nameof(IsAtEnd));

    }

}

```

```csharp

public class ViewModel()

{

    this.currentCustomer = 0;

    this.IsAtStart = true;

    this.IsAtEnd = false;

    this.customers = new List<Customer>

    ...

};

```

```csharp

public class ViewModel : INotifyPropertyChanged

{

    public Customer Current

    {

        ...

    }

}

```

```csharp

private void Next()

{

    if (this.customers.Count - 1 > this.currentCustomer)

    {

        this.currentCustomer++;

        this.OnPropertyChanged(nameof(Current));

        this.IsAtStart = false;

        this.IsAtEnd = (this.customers.Count - 1 == this.currentCustomer);

    }

}

```

```csharp

private void Previous()

{

    if (this.currentCustomer > 0)

    {

        this.currentCustomer--;

        this.OnPropertyChanged(nameof(Current));

        this.IsAtEnd = false;

        this.IsAtStart = (this.currentCustomer == 0);

    }

}

```

```csharp

public class ViewModel : INotifyPropertyChanged

{

    private List<Customer> customers;

    private int currentCustomer;

    public Command NextCustomer { get; private set; }

    public Command PreviousCustomer { get; private set; }

}

```

```xml

<?xml version="1.0" encoding="utf-8"?>

<VoiceCommands xmlns="http://schemas.microsoft.com/expression/2004/03/speech">

  <Command Name="showDetailsOf">

    <Gesture>

      <Sentence>

        show details of

        <val as="customer">customer</val>

      </Sentence>

    </Gesture>

  </Command>

  <Dictionary Name="Customers" lang="en-US">

    <Command Hint="showDetailsOf">

      <Gesture>

        <Sentence>

        show <val as="customer">customer</val>

        </Sentence>

      </Gesture>

    </Command>

  </Dictionary>

</VoiceCommands>

```

```xml

<?xml version="1.0" encoding="utf-8"?>

<VoiceCommands xmlns="http://schemas.microsoft.com/expression/2004/03/speech">

  <Command Name="showDetailsOf">

    <Gesture>

      <Sentence>

        show details of

        <val as="customer">customer</val>

      </Sentence>

    </Gesture>

  </Command>

  <Dictionary Name="Customers" lang="en-US">

    <Command Hint="showDetailsOf">

      <Gesture>

        <Sentence>

        show <val as="customer">customer</val>

        </Sentence>

      </Gesture>

    </Command>

  </Dictionary>

</VoiceCommands>

```

```csharp

    // Ensure the window is active

    try

    {

        var storageFile = await Package.Current.InstalledLocation.GetFileAsync("VoiceCommands.xml");

        await VoiceCommandManager.InstallDefinitionsAsync(storageFile);

    }

    catch (Exception ex)

    {

        Debug.WriteLine($"Installing Commands Failed: {ex.Message}");

    }

}

protected override void OnActivated(IActivatedEventArgs args)

{

    base.OnActivated(args);

}

protected override void OnActivated(IActivatedEventArgs args)

{

    if (args.Kind == ActivationKind.VoiceCommand)

    {

        var commandArgs = args as VoiceCommandEventArgs;

        var speechResult = commandArgs.Result;

        var commandName = speechResult.RulePath.First();

        string customerName = "";

        switch (commandName)

        {

            case "showDetailsOf":

                customerName = speechResult.SemanticInterpretation["customer"].FirstOrDefault();

                break;

            default:

                break;

        }

        Frame rootFrame = Window.Current.Content as Frame;

        if (rootFrame == null)

        {

            rootFrame = new Frame();

            rootFrame.NavigationFailed += OnNavigationFailed;

            Window.Current.Content = rootFrame;

        }

        rootFrame.Navigate(typeof(MainPage), customerName);

    }

}

```

```csharp

public sealed partial class MainPage : Page

{

  public MainPage()

  {

    ...

  }

  protected override void OnNavigatedTo(NavigationEventArgs e)

  {

    string userName = e.Parameter as string;

    if (!string.IsNullOrEmpty(userName))

    {

      ViewModel viewModel = new ViewModel(userName);

      this.DataContext = viewModel;

    }

  }

}

```

```csharp

SpeechRecognitionResult speechRecognitionResult = ...;

string commandMode = speechRecognitionResult.SemanticInterpretation.

    Properties["commandMode"].FirstOrDefault();

protected override void OnActivated(IAActivatedEventArgs args)

{

    if (args.Kind == ActivationKind.VoiceCommand)

    {
