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