# Using Raw Notifications

Raw notifications sent to WP7 applications are just that—raw. When a server or service sends a raw notification, it sends a blob of binary data. This data doesn't need to conform to any specific shape or size, so long as both the server sending the data and the WP7 application receiving the data can agree on that shape. This is an ideal situation for C# binary serialization. As you'll see in the code sample, no XML serialization is available for Silverlight on WP7, so we're left with using binary serialization using the WCF DataContractSerializer class as the easiest option for going from raw data to something usable by the application.

Before looking at the code, another thing worth pointing out is that raw notifications can be sent only to applications currently running in the foreground. When you send a toast notification, it is delivered to the start screen if the application isn't running. If the application is running, the toast notification is delivered directly to the application using an event handler. If a raw notification is sent to an application that is not currently running in the foreground, the notification is discarded as if it never happened.

For this reason, a very common design pattern in push notifications is to tell the registry service when the application is running and when the application shuts down. This lets the registry service know when the app can receive raw notifications versus receiving tile updates and toasts, which can be received at any time.

The following code handles the reception of a raw HTTP notification:

```
void NotificationChannel_HttpNotificationReceived(object sender,
    HttpNotificationEventArgs e)
{
    if (e.Notification.Body != null && e.Notification.Headers != null)
    {
        // Thanks to Daniel Vaughn (WP7 Unleashed by SAMS Press)
        // for this tidbit on having to remove nulls from the serialized
        // data contract sent from the push app/service
        using (BinaryReader reader =
            new BinaryReader(e.Notification.Body))
        {
            byte[] bodyBytes =
                reader.ReadBytes((int)e.Notification.Body.Length);

            int lengthWithoutNulls = bodyBytes.Length;
            for (int i = bodyBytes.Length - 1;
                i >= 0 && bodyBytes[i] == '\0';
                i--, lengthWithoutNulls--)
            {
                /* Intentionally left blank. */
            }

            byte[] cleanedBytes = new byte[lengthWithoutNulls];
            Array.Copy(bodyBytes, cleanedBytes, lengthWithoutNulls);
```