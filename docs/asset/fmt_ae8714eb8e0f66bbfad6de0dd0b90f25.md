
```
this.NextCustomer = new Command(this.Next, () =>
    { return this.customers.Count > 1 && !this.IsAtEnd; });

this.PreviousCustomer = new Command(this.Previous, () =>
    { return this.customers.Count > 0 && !this.IsAtStart; });

...
}
```

```
<Page.TopAppBar>
    <CommandBar>
        <AppBarButton x:Name="previousCustomer" Icon="Previous" Label="Previous" Command="{Binding Path=PreviousCustomer}"/>
        <AppBarButton x:Name="nextCustomer" Icon="Next" Label="Next" Command="{Binding Path=NextCustomer}"/>
    </CommandBar>
</Page.TopAppBar>
</Page>
```

```
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands xmlns="http://schemas.microsoft.com/voicecommands/1.2">
    <CommandSet xml:lang="en-us" Name="CustomersCommands">
        <CommandPrefix>Customers</CommandPrefix>
        <Example>Show details of John Sharp</Example>
    </CommandSet>
</VoiceCommands>
```

```
<?xml version="1.0" encoding="utf-8"?>
<VoiceCommands xmlns="http://schemas.microsoft.com/voicecommands/1.2">
    <CommandSet xml:lang="en-us" Name="CustomersCommands">
        <CommandPrefix>Customers</CommandPrefix>
        <Example>Show details of John Sharp</Example>
        <Command Name="showDetailsOf">
            <Example>show details of John Sharp</Example>
            <ListenFor RequireAppName="BeforeOrAfterPhrase">
                show details of {customer}
            </ListenFor>
            <ListenFor RequireAppName="BeforeOrAfterPhrase">
                show details for {customer}
            </ListenFor>
            <ListenFor RequireAppName="BeforeOrAfterPhrase">
                search for {customer}
            </ListenFor>
            <Feedback>Looking for {customer}</Feedback>
            <Navigate/>
        </Command>
        <PhraseTopic Label="customer" Scenario="Search">
            <Subject>Person Names</Subject>
        </PhraseTopic>
    </CommandSet>
</VoiceCommands>
```

```
using Windows.Storage;
using Windows.ApplicationModel.VoiceCommands;
using System.Diagnostics;
```

```
protected async override void OnLaunched(LaunchActivatedEventArgs e)
{
    ...
}
```

```
protected async override void OnLaunched(LaunchActivatedEventArgs e)
{
    ...
    // Ensure the current window is active
    Window.Current.Activate();
    try
    {
        var storageFile = await Package.Current.
            InstalledLocation.GetFileAsync(@"CustomerVoiceCommands.xml");
        await VoiceCommandDefinitionManager.
            InstallCommandDefinitionsFromStorageFileAsync(storageFile);
    }
    catch (Exception ex)
    {
        Debug.WriteLine(
            $"Installing Voice Commands Failed: {ex.ToString()}");
    }
}
```

```
protected override void OnActivated(IActivatedEventArgs args)
{
    base.OnActivated(args);
}
```

```
protected override void OnActivated(IActivatedEventArgs args)
{
    base.OnActivated(args);
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        var commandArgs = args as VoiceCommandActivatedEventArgs;
        var speechRecognitionResult = commandArgs.Result;
        var commandName = speechRecognitionResult.RulePath.First();
    }
}
```

```
if (args.Kind == ActivationKind.VoiceCommand)
{
    ...
    var commandName = speechRecognitionResult.RulePath.First();
    string customerName = "";
    switch (commandName)
    {
        case "showDetailsOf":
            customerName = speechRecognitionResult.SemanticInterpretation.Properties["customer"].FirstOrDefault();
            break;
        default:
            break;
    }
}
```

```
protected override void OnActivated(IActivatedEventArgs args)
{
    ...
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        ...
        switch (commandName)
        {
            ...
        }
    }
    Frame rootFrame = Window.Current.Content as Frame;
    if (rootFrame == null)
    {
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;
        Window.Current.Content = rootFrame;
    }
    rootFrame.Navigate(typeof(MainPage), customerName);
    Window.Current.Activate();
}
```

```
public ViewModel()
{
    _initializeState();
    this.customers = DataSource.Customers;
}
private void _initializeState()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.NextCustomer = new Command(this.Next, () =>
        { return this.customers.Count > 1 && !this.IsAtEnd; });
    this.PreviousCustomer = new Command(this.Previous, () =>
        { return this.customers.Count > 0 && !this.IsAtStart; });
}
```

```
public ViewModel(string customerName)
{
    _initializeState();
    string[] names = customerName.Split(new[] {' '}, 2,
        StringSplitOptions.RemoveEmptyEntries);
    this.customers =
        (from c in DataSource.Customers
        where string.Compare(c.FirstName.ToUpper(), names[0].ToUpper()) == 0 &&
        (names.Length > 1 ?
            string.Compare(c.LastName.ToUpper(), names[1].ToUpper()) == 0 : true)
        select c).ToList();
}
```

```
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        ...
    }
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        string customerName = e.Parameter as string;
        if (!string.IsNullOrEmpty(customerName))
        {
            ViewModel viewModel = new ViewModel(customerName);
            this.DataContext = viewModel;
        }
    }
}
```

```
SpeechRecognitionResult speechRecognitionResult = ...;
string commandMode = speechRecognitionResult.SemanticInterpretation.Properties["commandMode"].FirstOrDefault();
```

```
protected override void OnActivated(IActivatedEventArgs args)
{
    ...
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        var commandArgs = args as VoiceCommandActivatedEventArgs;
        var speechRecognitionResult = commandArgs.Result;
        var commandName = speechRecognitionResult.RulePath.First();
        string commandMode = speechRecognitionResult.SemanticInterpretation.Properties["commandMode"].FirstOrDefault();
        string customerName = "";
        ...
    }
}
```

```
protected override void OnActivated(IActivatedEventArgs args)
{
    ...
    if (args.Kind == ActivationKind.VoiceCommand)
    {
        ...
        switch (commandName)
        {
            ...
        }
        ...
        rootFrame.Navigate(typeof(MainPage),
            new NavigationArgs(customerName, commandMode));
        Window.Current.Activate();
    }
}
```

```
internal class NavigationArgs
{
    internal string commandMode { get; }
    internal string customerName { get; }
    public NavigationArgs(string customerName, string commandMode)
    {
        this.customerName = customerName;
        this.commandMode = commandMode;
    }
}
```

```
protected override async void OnNavigatedTo(NavigationEventArgs e)
{
    NavigationArgs args = e.Parameter as NavigationArgs;
    if (args != null)
    {
        string customerName = args.customerName;
        ViewModel viewModel = new ViewModel(customerName);
        this.DataContext = viewModel;
        if (args.commandMode == "voice")
        {
            if (viewModel.Current != null)
            {
                await Say($"Here are the details for {customerName}");
            }
            else
            {
                await Say($"{customerName} was not found");
            }
        }
    }
}
```

```
using Windows.Media.SpeechSynthesis;
using System.Threading.Tasks;
```

```
private async Task Say(string message)
{
    MediaElement mediaElement = new MediaElement();
    var synth = new SpeechSynthesizer();
    SpeechSynthesisStream stream =
        await synth.SynthesizeTextToStreamAsync(message);
    mediaElement.SetSource(stream, stream.ContentType);
```
