```
e.Collection.Values.Skip(1).FirstOrDefault() ?? string.Empty;
Deployment.Current.Dispatcher.BeginInvoke(
() => MessageBox.Show(message, title, MessageBoxButton.OK));
}
```

![](bbox=[0.32, 0.21, 0.6, 0.56])

Figure 12.2 Receiving a sample toast notification.

This code cracks open the incoming toast notification and then displays a message box with the contents. Note again that we're using the BeginInvoke method of the current deployment dispatcher. This is because we need to forward any UI changes that occur as a result of background thread changes onto the foreground UI thread. Figure 12.3 shows what a sample message box looks like in response to a delivered toast notification.

![](bbox=[0.29, 0.73, 0.63, 0.85])

Figure 12.3 Getting a toast notification with application running.