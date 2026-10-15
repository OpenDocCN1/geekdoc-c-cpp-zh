```
response.Headers["X-NotificationStatus"];
string notificationChannelStatus =
    response.Headers["X-SubscriptionStatus"];
string deviceConnectionStatus =
    response.Headers["X-DeviceConnectionStatus"];
}
}
```

There is one last point to make about push notifications that is more of a design pattern than anything else. If you have been paying close attention to the samples (or you’ve looked at the code download already), you might have noticed that whenever the application starts, it sends its notification channel URL to the registry service. This information is sent without any other identifying information. This means that the service won’t know the difference between new registrations and duplicate registrations. Additionally, if your application requires that different applications be sent different notifications, in contrast to a single mass broadcast, the model shown so far in this chapter won’t work.

In this case, I recommend creating an application ID the first time the application starts. This ID will remain constant and persist with the application for the rest of the time the application is installed on the user’s device. Every time the application gets a notification channel URI from Microsoft’s push notification infrastructure, it then sends that URI plus the application’s constant ID to the registry server. This not only prevents the same application from registering multiple notification channel URIs, but it also allows for single applications to be the target of specific push notifications. Later in the book, you will see how to store application configuration, settings, and user data (such as an application GUID) in something called isolated storage. Until then, remember that the service registry shown in this chapter was only complex enough to support the demonstration code and is by no means a design you should mimic in your production application.

# Summary

In today’s age of smartphones, typical users want to spend as little time as possible actually using the phone, unless they are playing a game, reading a book, and so on. Users have grown so accustomed to tailored alerts that they expect their phone to tell them when something important enough to warrant their attention has happened—whether that means they got an email, a friend wrote on their wall on their favorite social network, or the zombies have taken over a nearby town during the apocalypse.

This chapter provided you with the information, tools, and sample code to get you going building your own applications that can support push notifications in the form of tile changes, toasts, or even sending arbitrary, raw binary payloads that contain application-specific data such as stock price updates or changes in zombie population.

As you progress throughout the rest of the book, you will build on this knowledge and have push notifications in your tool belt filled with techniques for building powerful, compelling, highly engaging applications.