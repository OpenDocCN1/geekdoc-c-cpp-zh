

xxxxxxx. 记录此设备令牌（你可能需要将其剪切并粘贴到文本文件中）。稍后在你的提供方应用程序中，你将需要它来唯一标识将接收推送通知的设备。

## 工作原理

要接收推送通知，你首先需要使用之前创建的 App ID 配置应用程序。然后，你需要将应用程序配置为使用与开发证书关联的正确配置文件进行签名。

要为你的应用程序注册推送通知，请使用 `UIApplication` 类的 `registerForRemoteNotificationTypes:` 方法：

```objc
[[UIApplication sharedApplication]
registerForRemoteNotificationTypes:
(UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge |
UIRemoteNotificationTypeSound)];
```

这会为你的应用程序注册三种类型的通知——提示、标记和声音。

如果注册成功，将调用 `application:didRegisterForRemoteNotificationsWithDeviceToken:` 事件：

```objc
- (void)application:(UIApplication *)app
didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    NSString *str = [NSString
        stringWithFormat:@"Device Token=%@",deviceToken];
    NSLog(str);
}
```

此时，你可以打印出设备令牌。在实际应用程序中，你应该以编程方式将设备令牌发送回提供方应用程序，以便其维护需要接收通知的设备列表。事实上，Apple 建议你的应用程序每次启动时都将设备令牌发送给提供方应用程序，以告知提供方该应用程序仍在使用中。

当注册失败时，将调用 `application:didFailToRegisterForRemoteNotificationsWithError:` 事件：

```objc
- (void)application:(UIApplication *)app
didFailToRegisterForRemoteNotificationsWithError:(NSError *)err {
    NSString *str = [NSString stringWithFormat: @"Error: %@", err];
    NSLog(str);
}
```

如果应用程序在收到推送通知时正在运行，将调用 `application:didReceiveRemoteNotification:` 事件：

```objc
- (void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo {
    for (id key in userInfo) {
        NSLog(@"key: %@, value: %@", key, [userInfo objectForKey:key]);
    }
}
```

在这里，你可以检查收到的消息内容。如果应用程序在收到推送通知时未运行，则用户将看到类似图 17-24 的提示。

单击“视图”按钮会启动应用程序并触发 `application:didReceiveRemoteNotification:` 事件。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_471_0.png)

图 17-24

## 创建推送通知提供方

推送通知提供方是由应用程序开发人员编写的一个应用程序，用于通过 APNs 向 iPad 应用程序发送推送通知。

以下是通过 APNs 服务器向你的应用程序发送推送通知的基本步骤：

-   使用你之前创建的 SSL 证书与 APNs 服务器通信。
-   构造要发送消息的负载（payload）。
-   将包含负载的推送通知发送到 APNs。

APNs 是一个流式 TCP 套接字，你的提供方可以使用 SSL 安全通信通道与之通信。你以二进制流形式发送推送通知（包含负载）。连接到 APNs 后，请保持连接，并可在连接持续时间内发送任意数量的推送通知。

> **注意** 不要为每条要发送的推送通知反复打开和关闭到 APNs 的连接。快速打开和关闭与 APNs 的连接将被视为拒绝服务（DOS）攻击，并可能阻止你的提供方将推送通知发送到你的应用程序。

推送通知消息的格式如图 17-25 所示（图来自 Apple 文档）：

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_471_1.png)

图 17-25

> **注意** 有关更多详细信息，请参阅 Apple Push Notification Service 编程指南。该指南的完整路径是 http://developer.apple.com/iphone/library/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction/Introduction.html。

负载是一个 JSON 格式的字符串（最大 256 字节），携带你想要发送到应用程序的信息。负载示例如下：

```json
{
  "aps": {
    "alert" : "You got a new message!",
    "badge" : 5,
    "sound" : "beep.wav"},
  "acme1" : "bar",
  "acme2" : 42
}
```

为了避免从零开始开发推送通知提供方的麻烦，你可以使用由 Stefan Hafenegger 编写的 PushMeBaby 应用程序（适用于 Mac OS X）（获取地址：http://stefan.hafenegger.name/download/PushMeBabySource.zip）。

下面的“试一试”展示了如何修改 PushMeBaby 应用程序以向你的应用程序发送通知。

## 试一试 修改提供方应用程序

-   1. 下载 PushMeBaby 应用程序的源代码，然后在 Xcode 中打开它。
-   2. 在 Xcode 中右键单击 Resources 文件夹，然后选择“添加现有文件”。选择你之前下载的 aps_developer_identity.cer 文件（参见图 17-26）。
-   3. 在 ApplicationDelegate.m 文件中，按粗体所示修改代码，将 xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx 替换为你之前获取的实际设备令牌：

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_472_0.png)

```objc
- (id)init {
    self = [super init];
    if(self != nil) {
        self.deviceToken = @"xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx xxxxxxxx";

        self.payload = @"{\"aps\":{\"alert\":\"You got a new message!\",\"badge\":5,\"sound\":\"beep.wav\"},\"acme1\":\"bar\",\"acme2\":42}";

        self.certificate = [[NSBundle mainBundle]
            pathForResource:@"aps_developer_identity" ofType:@"cer"];
    }
    return self;
}
```

-   4. 按 Command-R 测试应用程序。系统会要求你授予证书访问权限。点击“始终允许”（参见图 17-27）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_473_0.png)

图 17-27

-   5. 在 iPad 上，确保 ApplePushNotification 应用程序未在运行。要向设备发送消息，请点击“推送”按钮。服务器基本上会向 APNs 发送以下消息：

```json
{
  "aps": {
    "alert" : "You got a new message!",
    "badge" : 5,
    "sound" : "beep.wav"},
  "acme1" : "bar",
  "acme2" : 42
}
```

-   6. 如果消息推送正确，你将看到如图 17-28 所示的通知。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_473_1.png)

图 17-28

-   7. 按 Command-R 调试 ApplePushNotification 应用程序，并从 PushMeBaby 应用程序发送推送消息；调试器控制台窗口将显示以下输出：

```text
2010-03-24 21:11:49.182 ApplePushNotification[1461:207]
key: acme1, value: bar
2010-03-24 21:11:49.187 ApplePushNotification[1461:207]
key: aps, value: {
  alert = "You got a new message!";
  badge = 5;
  sound = "beep.wav";
}
2010-03-24 21:11:49.191 ApplePushNotification[1461:207]
key: acme2, value: 42
```

## 工作原理

基本上，提供方的角色是向 APNs 服务器发送通知，由其转发到设备。因此，你发送的消息格式如下：

```json
{
  "aps": {
    "alert" : "You got a new message!" ,
    "badge" : 5,
    "sound" : "beep.wav"},
  "acme1" : "bar",
  "acme2" : 42
}
```

本质上，beep.wav 文件名告知客户端在收到通知时播放 beep.wav 文件。

## 总结

在本章中，你了解了构建使用 Apple Push Notification 服务的 iPad 应用程序所需的各种步骤。请花些时间逐步完成获取开发证书和配置文件的过程，因为这些步骤常常让开发人员措手不及。但一旦你成功运行，付出是值得的！

## 练习

-   1. 说出使用 Apple Push Notification 服务需要生成的两种证书。
-   2. 为什么建议在“钥匙串访问”应用程序中备份开发证书？
-   3. 说出注册推送通知的方法。
-   4. 设备令牌的用途是什么？
-   5. 说出可以获取推送到设备上的通知的事件。

练习的答案可在附录 A 中找到。

