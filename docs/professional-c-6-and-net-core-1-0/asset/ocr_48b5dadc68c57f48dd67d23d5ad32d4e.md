message written. You can also specify to just write information messages—which also include errors—or to write errors only.

```
private static void InitListener(IEnumerable<EventSource>
sources)
{
    listener = new MyEventListener();
    foreach (var source in sources)
    {
        listener.EnableEvents(source, EventLevel.LogAlways);
    }
}
```

When you run the application, you see events of the `FrameworkEventSource` and the `Wrox-SampleEventSource` written to the console. Using a custom event listener like this, you can easily write events to Application Insights, which is a cloud-based telemetry service that’s explained in the next section.

# Working with Application Insights

Application Insights is a Microsoft Azure technology that allows monitoring usage and performance of applications, no matter where they are used. You can get reports of users having issues with your application—for example, you can find out about exceptions—and you can also find out the features users are using from your application. For example, let’s say you have added a new feature to your app. Are users finding the button to activate the feature?

When you use Application Insights, it’s easy to identify issues that users are having with the app. There’s a good reason Microsoft makes it easy to integrate Application Insights with all kinds of applications (both web and Windows apps).