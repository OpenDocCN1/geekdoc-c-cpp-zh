

```
e.Collection.Values.Skip(1).FirstOrDefault() ?? string.Empty;
Deployment.Current.Dispatcher.BeginInvoke(
() => MessageBox.Show(message, title, MessageBoxButton.OK));
}
```

![](img/04a00d46bb1059867d95707babd62ee7_173_0.png)

Figure 12.2 Receiving a sample toast notification.

这段代码打开了传入的 toast 通知，然后用其内容显示一个消息框。再次注意，我们使用了当前部署调度器的 BeginInvoke 方法。这是因为我们需要将由于后台线程更改而产生的任何 UI 更改转发到前台 UI 线程。图 12.3 显示了在收到 toast 通知后样本消息框的外观。

![](img/04a00d46bb1059867d95707babd62ee7_173_1.png)

Figure 12.3 Getting a toast notification with application running.

## Using Raw Notifications

发送给 WP7 应用的原始通知就是原始的。当服务器或服务发送原始通知时，它发送的是二进制数据的 blob。该数据不需要符合任何特定的形状或大小，只要发送数据的服务器和接收数据的 WP7 应用能够就该形状达成一致即可。这对于 C# 二进制序列化来说是一个理想的情况。正如你在代码示例中看到的，Silverlight 在 WP7 上没有可用的 XML 序列化，因此我们只能使用 WCF DataContractSerializer 类进行二进制序列化，这是将原始数据转换为应用可用的东西的最简单选择。

在查看代码之前，还有一件值得指出的事情是，原始通知只能发送给当前在前台运行的应用。当你发送 toast 通知时，如果应用未运行，它会被发送到开始屏幕。如果应用正在运行，toast 通知会通过事件处理程序直接发送到应用。如果原始通知发送给当前不在前台运行的应用，该通知将被丢弃，就像它从未发生过一样。

因此，在推送通知中，一个非常常见的设计模式是告诉注册服务应用何时正在运行以及应用何时关闭。这让注册服务知道应用何时可以接收原始通知，而瓦片更新和 toast 则可以在任何时候接收。

以下代码处理原始 HTTP 通知的接收：

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

```
DataContractSerializer ser =
    new DataContractSerializer(typeof(ZombiePopulationPayload));
using (MemoryStream stream = new MemoryStream(cleanedBytes))
{
    ZombiePopulationPayload zombiePopulation =
        (ZombiePopulationPayload)ser.ReadObject(stream);
    Deployment.Current.Dispatcher.BeginInvoke(
        () =>
            MessageBox.Show(
                string.Format("Us:{0} Them:{1}",
                    zombiePopulation.Humans,
                    zombiePopulation.Zombies),
                "Population Update", MessageBoxButton.OK)
        );
    }
}
```

当我们运行代码并发送原始通知时，对该通知的响应看起来与图 12.4 中的对话框类似。 （完整的通知示例，包括注册服务和推送通知模拟器，可在本书随附代码中第 12 章解决方案中找到。）

![](img/04a00d46bb1059867d95707babd62ee7_175_0.png)

Figure 12.4 Receiving a raw notification with custom data.

代码首先做的第一件事是打开 e.Notification.Body 中包含的流。通知工具发送的二进制数据（它取代了云中的服务器）被 WP7 推送通知基础设施用末尾的一堆 null 填充，因此我们需要做的下一件事是在尝试将二进制反序列化为 C# 类之前去掉所有多余的 null。Sams Publishing 出版的《WP7 Unleashed》的作者 Daniel Vaughan 最近发表了一篇博文说明了这一现象。

在二进制数据准备好并去掉多余的 null 之后，它就可以使用 DataContractSerializer 类转换为类。最后，有一个完整的 ZombiePopulationPayload 类实例，我们可以使用 Dispatcher 将 MessageBox 显示请求转发到前台线程。

如果你好奇服务器端方面的内容，以下代码将向 Microsoft 的推送通知基础设施发送原始通知（此代码也包含在章节中）：

```
private void sendRawButton_Click(object sender, RoutedEventArgs e)
{
    ZombiePopulationPayload zombiePopulation =
        new ZombiePopulationPayload() { Humans = 5.25m, Zombies = 8.23m };
    DataContractSerializer ser =
        new DataContractSerializer(typeof(ZombiePopulationPayload));
    MemoryStream ms = new MemoryStream();
    ser.WriteObject(ms, zombiePopulation);
    ms.Seek(0, SeekOrigin.Begin);
    byte[] zombieBytes = ms.GetBuffer();

    // instantiate proxy to our custom notification registry svc
    NotificationService.NotificationsClient client =
        new NotificationService.NotificationsClient();
    string[] uris = client.GetRegisteredChannels();

    Console.WriteLine("About to send raw data to the following URIs:");

    foreach (string uri in uris)
    {
        HttpWebRequest sendNotificationRequest =
            (HttpWebRequest)WebRequest.Create(uri);

        sendNotificationRequest.Method = "POST";
        sendNotificationRequest.Headers.Add("X-NotificationClass", "3");

        sendNotificationRequest.ContentLength = zombieBytes.Length;

        using (Stream requestStream =
            sendNotificationRequest.GetRequestStream())
        {
            requestStream.Write(zombieBytes, 0, zombieBytes.Length);
        }

        HttpWebResponse response =
            (HttpWebResponse)sendNotificationRequest.GetResponse();
        // Troubleshooting information returned by WP7 push server
        string notificationStatus =
            response.Headers["X-NotificationStatus"];
        string notificationChannelStatus =
            response.Headers["X-SubscriptionStatus"];
```

以下代码向已注册的通知通道 URL 发送 XML 有效负载，以更改应用的瓦片图像、徽章计数和标题文本：

```
private void SendTile(string[] uriTargets, string backgroundImage,
    int count, string title)
{
    Console.WriteLine("About to send tile to the following URIs:");

    foreach (string uri in uriTargets)
    {
        Console.WriteLine(uri);
        HttpWebRequest sendNotificationRequest =
            (HttpWebRequest)WebRequest.Create(uri);

        sendNotificationRequest.Method = "POST";
        sendNotificationRequest.ContentType = "text/xml";
        sendNotificationRequest.Headers.Add("X-WindowsPhone-Target",
            "token");
        sendNotificationRequest.Headers.Add("X-NotificationClass", "1");

        string payloadString =
            string.Format("<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                "<wp:Tile>" +
                "<wp:BackgroundImage>{0}</wp:BackgroundImage>" +
                "<wp:Count>{1}</wp:Count>" +
                "<wp:Title>{2}</wp:Title>" +
                "</wp:Tile>" +
                "</wp:Notification>", backgroundImage,
                count.ToString(), title);

        byte[] notificationMessage =
            System.Text.UTF8Encoding.UTF8.GetBytes(payloadString);
        sendNotificationRequest.ContentLength =
            notificationMessage.Length;

        using (Stream requestStream =
            sendNotificationRequest.GetRequestStream())
        {
            requestStream.Write(notificationMessage, 0,
                notificationMessage.Length);
        }

        // Sends the notification and gets the response.
        HttpWebResponse response =
            (HttpWebResponse)sendNotificationRequest.GetResponse();
        string notificationStatus =
```
