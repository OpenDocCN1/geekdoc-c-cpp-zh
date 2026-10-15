The application is now ready to receive push notifications. The tricky part, of course, is actually sending them. From personal experience, having written several applications for the iPhone that receive push notifications and from talking to many developers of push-enabled applications, I can tell you that this part is usually where the iOS developers start cringing. Their blood pressure goes up, the stress level rises, and they start eating antacid drops like they were candy. Needless to say, getting push notifications sent to an iPhone is a very brittle process. It isn’t necessarily difficult, but there are hundreds of tiny little moving parts, and if any of them are not in exactly the right place, nothing works.

Thankfully, the process is a bit easier on Windows Phone 7. An application that you’ve written that resides in the cloud can send a push notification to a specific device using the channel URI that is part of the HttpNotificationChannel instance returned either through construction or the Find static method. This URL will look something like the one that follows:

```
http://sn1.notify.live.net/throttledthirdparty/01.00/
AAEMRpKul9RgTzIGrBGVOqKvAgAAAAADAQAAAAQUZm52OjIzOEQ2NDJDRkI5MEVFMEQ
```

After you have this URL, you can send an HTTP POST to this URL from your application or service. The XML payload that gets sent to this URL for a toast notification looks like this:

```
<?xml version="1.0" encoding="utf-8"?>
<wp:Notification xmlns:wp="WPNotification">
    <wp:Toast>
        <wp:Text1>Toast message 1</wp:Text1>
        <wp:Text2>Toast message 2</wp:Text2>
    </wp:Toast>
</wp:Notification>
```

There is plenty of documentation on how to create these XML messages—what custom headers your service needs to send to deliver toast, tile, or raw notifications. For details on how to deliver a push notification (using C#), see the MSDN documentation at http://msdn.microsoft.com/en-us/library/ff402545(v=VS.92).aspx.

The code that accompanies this chapter includes a full solution that has a WPF test harness application. Using this harness (called UsVsThemConsole), you can send a toast notification to the sample application like the one shown in Figure 12.2.

This is a decent start but, with the code we have at the moment, the application will not properly handle toast notifications that are sent when the application is running in the foreground. To make sure that we handle that case, change the ShellToastNotificationReceived event handler to the following code:

```
void NotificationChannel_ShellToastNotificationReceived(
    object sender, NotificationEventArgs e)
{
    string title = e.Collection.Values.First();
    string message =
```