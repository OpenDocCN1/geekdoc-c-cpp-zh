
```csharp
static void Main(string[] args)

{

    Console

}
```

```csharp
static void Main(string[] args)

{

    Console.WriteLine

}
```

```csharp
static void Main(string[] args)

{

    Console.WriteLine(

}
```

```csharp
static void Main(string[] args)

{

    Console.WriteLine();

}
```

```csharp
static void Main(string[] args)

{

    Console.WriteLine("Hello World!");

}
```

```csharp
Console.ReadLine(); // Wait for the user to press the Enter key
```

```
1>------ Build started: Project: TestHello, Configuration: Debug Any CPU ------
1>  TestHello -> C:\Users\John\Documents\Microsoft Press\Visual CSharp Step By Step\Chapter
1\TestHello\TestHello\bin\Debug\TestHello.exe
========= Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped =========
```

```csharp
using System;

using System.Collections.Generic;

using System.Linq;

using System.Text;

using System.Threading.Tasks;
```

The name `Console` does not exist in the current context.

```csharp
static void Main(string[] args)

{

    System.Console.WriteLine("Hello world!");

}
```

```xml
<TextBlock x:Name="textBlock" HorizontalAlignment="Left" Margin="10,10,0,0"

TextWrapping="Wrap"

Text="TextBlock" VerticalAlignment="Top"/>
```

```csharp
using System;

using System.Collections.Generic;

using System.IO;

using System.Linq;

using System.Runtime.InteropServices.WindowsRuntime;

using Windows.Foundation;

using Windows.Foundation.Collections;

using Windows.UI.Xaml;

using Windows.UI.Xaml.Controls;

using Windows.UI.Xaml.Controls.Primitives;

using Windows.UI.Xaml.Data;

using Windows.UI.Xaml.Input;

using Windows.UI.Xaml.Media;

using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=402352&clcid=0x409

namespace Hello

{

    /// <summary>

    /// An empty page that can be used on its own or navigated to within a Frame.

    /// </summary>

    public sealed partial class MainPage : Page

    {

        public MainPage()

        {

            this.InitializeComponent();

        }

    }

}
```

```csharp
using System;

using System.Collections.Generic;

using System.IO;

using System.Linq;

using System.Runtime.InteropServices.WindowsRuntime;

using Windows.ApplicationModel;

using Windows.ApplicationModel.Activation;

using Windows.Foundation;

using Windows.Foundation.Collections;

using Windows.UI.Xaml;

using Windows.UI.Xaml.Controls;

using Windows.UI.Xaml.Controls.Primitives;

using Windows.UI.Xaml.Data;

using Windows.UI.Xaml.Input;

using Windows.UI.Xaml.Media;

using Windows.UI.Xaml.Navigation;

// The Blank Application template is documented at http://go.microsoft.com/fwlink/?LinkId=402347&clcid=0x409

namespace Hello

{

    /// <summary>

    /// Provides application-specific behavior to supplement the default Application class.

    /// </summary>

    sealed partial class App : Application

    {

        /// <summary>

        /// Allows tracking page views, exceptions and other telemetry through the Microsoft Application Insights service.

        /// </summary>

        public static Microsoft.ApplicationInsights.TelemetryClient TelemetryClient;
```

```csharp
/// <summary>
/// Initializes the singleton application object. This is the first line of authored
/// executed, and as such is the logical equivalent of main() or WinMain().
/// </summary>
public App()
{
    Microsoft.ApplicationInsights.WindowsAppInitializer.InitializeAsync(
    Microsoft.ApplicationInsights.WindowsCollectors.Metadata |
    Microsoft.ApplicationInsights.WindowsCollectors.Session);
    this.InitializeComponent();
    this.Suspending += OnSuspending;
}

/// <summary>
/// Invoked when the application is launched normally by the end user. Other entry
/// will be used such as when the application is launched to open a specific file.
/// </summary>
/// <param name="e">Details about the launch request and process.</param>
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
#if DEBUG
    if (System.Diagnostics.Debugger.IsAttached)
    {
        this.DebugSettings.EnableFrameRateCounter = true;
    }
#endif
    Frame rootFrame = Window.Current.Content as Frame;
    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    if (rootFrame == null)
    {
        // Create a Frame to act as the navigation context and navigate to the first
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;
        if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            //TODO: Load state from previously suspended application
        }
        // Place the frame in the current Window
        Window.Current.Content = rootFrame;
    }
    if (rootFrame.Content == null)
    {
        // When the navigation stack isn’t restored navigate to the first page,
        // configuring the new page by passing required information as a navigation
        // parameter
        rootFrame.Navigate(typeof(MainPage), e.Arguments);
    }
```

```csharp
}
    // Ensure the current window is active
    Window.Current.Activate();
}

/// <summary>
/// Invoked when Navigation to a certain page fails
/// </summary>
/// <param name="sender">The Frame which failed navigation</param>
/// <param name="e">Details about the navigation failure</param>
void OnNavigationFailed(object sender, NavigationFailedEventArgs e)
{
    throw new Exception("Failed to load Page " + e.SourcePageType.FullName);
}

/// <summary>
/// Invoked when application execution is being suspended. Application state is saved
/// without knowing whether the application will be terminated or resumed with the contents
    /// of memory still intact.
/// </summary>
    /// <param name="sender">The source of the suspend request.</param>
    /// <param name="e">Details about the suspend request.</param>
    private void OnSuspending(object sender, SuspendingEventArgs e)
    {
        var deferral = e.SuspendingOperation.GetDeferral();
        //TODO: Save application state and stop any background activity
        deferral.Complete();
    }
}
}
```

```csharp
private void okClick(object sender, RoutedEventArgs e)
{

}
```

```csharp
using System;

...

using Windows.UI.Xaml.Navigation;

using Windows.UI.Popups;
```

```csharp
private void okClick(object sender, RoutedEventArgs e)
{
    MessageDialog msg = new MessageDialog("Hello " + userName.Text);
    msg.ShowAsync();
}
```

```xml
<Button x:Name="ok" ... Click="okClick" />
```

```csharp
Console.WriteLine("Hello, World!");
```

```csharp
int age;
Console.WriteLine(age); // compile-time error
```

```xml
<ListBox x:Name="type" ... SelectionChanged="typeSelectionChanged">
    <ListBoxItem>int</ListBoxItem>
    <ListBoxItem>long</ListBoxItem>
    <ListBoxItem>float</ListBoxItem>
    <ListBoxItem>double</ListBoxItem>
    <ListBoxItem>decimal</ListBoxItem>
    <ListBoxItem>string</ListBoxItem>
    <ListBoxItem>char</ListBoxItem>
    <ListBoxItem>bool</ListBoxItem>
</ListBox>
```

```csharp
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}

private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = intVar.ToString();
}

private void showDoubleValue()
{
    double doubleVar;
    doubleVar = 0.42;
    value.Text = doubleVar.ToString();
}

private void showBoolValue()
{
    bool boolVar;
    boolVar = false;
    value.Text = boolVar.ToString();
}
```

```csharp
long moneyPaidToConsultant;
moneyPaidToConsultant = 750 * 20;
// 编译时错误
Console.WriteLine("Gillingham" - "Forest Green Rovers");
Console.WriteLine("43" + "1");
```

```csharp
private void addValues()
{
    int lhs = int.Parse(lhsOperand.Text);
    int rhs = int.Parse(rhsOperand.Text);
    int outcome = 0;
    // TODO: 将 rhs 加到 lhs 并将结果存储在 outcome 中
    expression.Text = $"{lhsOperand.Text} + {rhsOperand.Text}";
    result.Text = outcome.ToString();
}
```

```csharp
private void addValues()
{
```
