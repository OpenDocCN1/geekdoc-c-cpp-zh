```
// proxy to my home-grown channel URI registration service
NotificationService.NotificationsClient client =
    new NotificationService.NotificationsClient();
client.RegisterChannelAsync(channelUri);
client.RegisterChannelCompleted +=
    new EventHandler<System.ComponentModel.AsyncCompletedEventArgs>(
        client_RegisterChannelCompleted);
}

void client_RegisterChannelCompleted(object sender,
    System.ComponentModel.AsyncCompletedEventArgs e)
{
    if (e.Error == null)
    {
        Debug.WriteLine(
            "Registered channel URI with notification service.");
    }
}
```

In the preceding code, the NotificationService.NotificationsClient class is created by adding a service reference to the WCF service I’ve written as part of this project. All of this is taken care of for you in the downloadable code sample, but it is helpful to know where all these components come from.

The first thing the application needs to do is look to see whether there is already a notification channel registered by the name we gave it for our application. The HttpNotificationChannel.Find() method performs this task and hides from us the complexity of how Microsoft is keeping track internally of all the notification channels for all the apps.

If the application doesn’t find an existing channel, it creates a new one using the HttpNotificationChannel constructor and then opens this new channel. At this point the code knows that, whether new or previously created, the NotificationChannel property we’ve created now holds a valid instance of a notification channel.

Next, we make a call to the SetupDelegates() method. This method attaches a bunch of event handlers to various events, such as ChannelUriUpdated, HttpNotificationReceived, ShellToastNotificationReceived, and ErrorOccurred.

With the event handlers in place, we can perform the final task in setting the application up to receive toasts: binding. Binding associates a particular notification channel with any of the delivery mechanisms, such as toast notifications or tile notifications. In our case, for this first version of the application, the SubscribeToNotifications method binds only to toast notifications.

At this point the application has all of the following:

+   - A valid HttpNotificationChannel instance with a valid ChannelUri
+   - Event handlers assigned to all of the important events on the channel
+   - Bindings between the notification channel and notification types like toast or tile