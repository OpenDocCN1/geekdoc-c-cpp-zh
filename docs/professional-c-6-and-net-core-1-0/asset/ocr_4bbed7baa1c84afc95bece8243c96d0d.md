# NuGet Packages

```
Microsoft.AspNet.SignalR.Client
Microsoft.Extensions.DependencyInjection
Newtonsoft.Json
```

# Namespaces

```
Microsoft.AspNet.SignalR.Client
Microsoft.Extensions.DependencyInjection
System
System.Collections.ObjectModel
System.Net.Http
System.Windows
```

The user interface of the WPF application defines two TextBox, two Button, and one ListBox element to enter the name and message, to connect to the service hub, and to show a list of received messages (code file WPFChatClient/MainWindow.xaml):

```
<TextBlock Text="Name" />
<TextBox Text="{Binding ViewModel.Name, Mode=TwoWay}" />
<Button Content="Connect" Command="{Binding ViewModel.ConnectCommand}" />
<TextBlock Text="Message" />
<TextBox Text="{Binding ViewModel.Message, Mode=TwoWay}" />
<Button Content="Send" Command="{Binding ViewModel.SendCommand, Mode=OneTime}" />
<ListBox ItemsSource="{Binding ViewModel.Messages, Mode=OneWay}" />
```

In the startup code of the application, the dependency injection container is defined, and services as well as view models are registered (code file WPFChatClient/App.xaml.cs):

```
public partial class App: Application
{
    protected override void OnStartup(StartupEventArgs e)
    {
        base.OnStartup(e);
        IServiceCollection services = new ServiceCollection();
        services.AddTransient<ChatViewModel>();
        services.AddTransient<GroupChatViewModel>();
        services.AddSingleton<IMessagingService, MessagingService>();
        Container = services.BuildServiceProvider();
    }
    public IServiceProvider Container { get; private set; }
}
```

Within the code-behind file of the view, the ChatViewModel is assigned to the ViewModel property using the dependency injection container (code file WPFChatClient/MainWindow.xaml.cs):