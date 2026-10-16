![](bbox=[0.105, 0.062, 0.895, 0.352])

# Figure 20.6

You need to set the Build action of this file to Content, and you need to copy the file to the output directory (just set the corresponding properties in the Property window).

Next, you initialize Application Insights by invoking the InitializeAsync method of the WindowsAppInitializer class (namespace Microsoft.ApplicationInsights). This method enables you to define what Windows collectors should be used; by default the metadata, session, page view, and unhandled exception collectors are configured (code file winAppInsights/App.xaml.cs):

```
public App()
{

WindowsAppInitializer.InitializeAsync(WindowsCollectors.Metadata |
    WindowsCollectors.Session | WindowsCollectors.PageView |
    WindowsCollectors.UnhandledException);

    this.InitializeComponent();
    this.Suspending += OnSuspending;
}
```

> NOTE The InitializeAsync method by default reads the instrumentation key from the file applicationinsights.config. You can also use an overload of this method to pass the instrumentation key with the first parameter.

# Using Collectors

Without doing anything more, you’re getting good information out of Application Insights. Just start the application; the collectors defined by the InitializeAsync methods do their jobs. After you run the app,