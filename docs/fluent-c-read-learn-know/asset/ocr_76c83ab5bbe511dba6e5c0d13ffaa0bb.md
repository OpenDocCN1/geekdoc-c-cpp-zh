# EXPLORING ROUTEDEVENTARGS

In reality, you won't have to use the Sender parameter and source properties all that often, but when you need them, you really need them, so let's spend a little time playing with them. To test your new and improved version of the method:

# CREATE A WPF PROJECT

You can call it anything you like.

# CREATE AN EVENT HANDLER

We'll start by building a routine that will display the three parameters. Here's my version, but you can do something fancier. If you're feeling inspired, you might try building a Window to display the values in TextBox elements. The important thing is that your method has the same signature as mine. (This is the standard signature for any routed event handler.)

```
private void ShowArguments(object sender, RoutedEventArgs e)
{
    StringBuilder eventDetailsSB = new StringBuilder();
    eventDetailsSB.AppendLine("Event: " + e.RoutedEvent.Name);
    eventDetailsSB.AppendLine("Sender: " + sender.GetType().ToString());
    eventDetailsSB.AppendLine("Source: " + e.Source.GetType().ToString());
    eventDetailsSB.AppendLine("Original: " + e.OriginalSource.GetType().
    ToString());

    MessageBox.Show(eventDetailsSB.ToString());
}
```

# TRIGGER THE EVENT

We'll look at different ways to trigger events in a minute, but for now, just set the Loaded event property of your main window (in the Events section of the Properties window in XAML view) to the name of your method.

# TEST IT

Run the application to make sure everything you've done so far is working properly. The Sender, Source and OriginalSource should all be the name of your Window class.