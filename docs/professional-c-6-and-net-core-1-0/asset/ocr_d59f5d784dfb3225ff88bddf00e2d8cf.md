```
TimeSpan.FromSeconds(2), TimeSpan.FromSeconds(3))
{
    Task.Delay(15000).Wait();
}
}
```

```
private static void TimeAction(object o)
{
    WriteLine($"System.Threading.Timer {DateTime.Now:T}");
}
```

The DispatcherTimer from the namespaces System.Windows.Threading (for Windows Desktop applications with WPF) and Windows.UI.Xaml (for Windows apps) is a timer for XAML-based apps where the event handler is called within the UI thread, thus it is possible to directly access user interface elements.

The sample application to demonstrate the DispatcherTimer is a Windows app that shows the hand of a clock to switch every second. The following XAML code defines the commands that enable you to start and stop the clock (code file WinAppTimer/MainPage.xaml):

```
<Page.TopAppBar>
    <CommandBar IsOpen="True">
        <AppBarButton Icon="Play" Click="{x:Bind OnTimer}" />
        <AppBarButton Icon="Stop" Click="{x:Bind OnStopTimer}" />
    </CommandBar>
</Page.TopAppBar>
```

The hand of the clock is defined using the shape Line. To rotate the line, you use a RotateTransform element:

```
<Canvas Width="300" Height="300">
    <Ellipse Width="10" Height="10" Fill="Red" Canvas.Left="145" Canvas.Top="145" />
    <Line Canvas.Left="150" Canvas.Top="150" Fill="Green" StrokeThickness="3" Stroke="Blue" X1="0" Y1="0" X2="120" Y2="0" >
        <Line.RenderTransform>
            <RotateTransform CenterX="0" CenterY="0" Angle="270" x:Name="rotate" />
        </Line.RenderTransform>
    </Line>
</Canvas>
```

> NOTE XAML shapes are explained in Chapter 30, “Styling XAML Apps.”

The DispatcherTimer object is created in the MainPage class. In the constructor, the handler method is assigned to the Tick event, and the Interval is specified to be one second. The timer is started in the OnTimer method—the method that gets called when the user clicks the Play button in the CommandBar (code file WinAppTimer/MainPage.xaml.cs):

```
private DispatcherTimer _timer = new DispatcherTimer();
public MainPage()
{
```