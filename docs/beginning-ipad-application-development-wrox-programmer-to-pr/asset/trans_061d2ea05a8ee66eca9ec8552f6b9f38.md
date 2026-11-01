
```
NSURL *fileURL = [[NSURL alloc]
initFileURLWithPath: soundFilePath];

AVAudioPlayer *audioPlayer =
[[AVAudioPlayer alloc] initWithContentsOfURL:fileURL
error:nil];

[fileURL release];
[audioPlayer play];

NSError *error;
AVAudioSession *audioSession =
[AVAudioSession sharedInstance];

if (![audioSession
setCategory:AVAudioSessionCategoryPlayAndRecord
error:&error]) {
NSLog(
@"Error setting category: %@",
[error localizedDescription]);
}

if (![audioSession setActive: YES error: &error]) {
NSLog(@"Error activating audioSession: %@",
[error description]);
}

[GKVoiceChatService defaultVoiceChatService].client = self;
```

**警告** *如果你不启动音频播放器，语音聊天将无法工作。*

然后，你将获取 `GKVoiceChatService` 类的单例实例，并调用其 `startVoiceChatWithParticipantID:error:` 方法来启动语音聊天：

```
if (![[GKVoiceChatService defaultVoiceChatService]
startVoiceChatWithParticipantID:peerID error:&error]) {
NSLog(@"Error starting startVoiceChatWithParticipantID: %@",
[error userInfo]);
}
```

调用 `startVoiceChatWithParticipantID:error:` 方法会调用 `voiceChatService:sendData:toParticipantID:` 方法（该方法在 `GKVoiceChatClient` 协议中定义），后者利用当前蓝牙会话将配置数据发送到另一台连接的设备：

```
-(void) voiceChatService:(GKVoiceChatService *)voiceChatService
sendData:(NSData *)data
toParticipantID:(NSString *)participantID {
[currentSession sendData:data toPeers:
[NSArray arrayWithObject:participantID]
}
```

## 本章所学内容

| 主题 | 关键概念 |
|---|---|
| 查找对等蓝牙设备 | 使用 `GKPeerPickerController` 类 |
| 在两个蓝牙设备之间通信 | 使用 `GKSession` 类。 |
| 建立语音聊天 | 调用 `GKVoiceChatService` 类中的 `startVoiceChatWithParticipantID:error:` 方法<br>在发起方，调用 `GKVoiceChatClient` 协议中定义的 `voiceChatService:sendData:toParticipantID:` 方法<br>在接收方，调用 `GKVoiceChatClient` 协议中定义的 `receivedData:fromParticipantID:` 方法 |
| 将麦克风静音 | `[GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;` |

![](img/744c5ec15e15ca7891c98be71dc25d13_441_0.png)

图 16-1

3. 在 BonjourViewController.h 文件中，添加以下粗体语句：

```
#import <UIKit/UIKit.h>
@interface BonjourViewController : UIViewController {
    //---outlets---
    IBOutlet UITableView *tbView;
    IBOutlet UITextView *debug;
}

//---expose the outlets as properties---
@property (nonatomic, retain) UITableView *tbView;
@property (nonatomic, retain) UITextView *debug;

@end
```

4. 在 BonjourViewController.xib 窗口中，执行以下连接：

-   按住 Control 键单击 File's Owner 项，然后将其拖放到 Table view 上。选择 `tbView`。
-   按住 Control 键单击 File's Owner 项，然后将其拖放到 Text view 上。选择 `debug`。
-   在 Table view 上右键单击，然后将 `dataSource` 插座连接到 File's Owner 项。
-   在 Table view 上右键单击，然后将 `delegate` 插座连接到 File's Owner 项。

5. 要验证所有连接是否正确，请右键单击 File's Owner 项并查看其连接（参见图 16-2）。

![](img/744c5ec15e15ca7891c98be71dc25d13_442_0.png)

### 工作原理

因为将使用 Table view 显示网络上发现的用户列表，所以需要将 `dataSource` 和 `delegate` 插座设置为 File's Owner 项。TextView 将用于显示后台发生的各种情况。这对于调试你的应用，以及理解网络中接连发现服务时发生的事情非常有用。

## 发布服务

连接好所有视图和插座后，就可以使用 `NSNetService` 类发布服务了。下面的“试一试”将演示具体做法。

### 试一试  在网络上发布服务

1. 使用上一节创建的同一个项目，在 BonjourAppDelegate.h 文件中添加以下粗体语句：

```
#import <UIKit/UIKit.h>

@class BonjourViewController;

@interface BonjourAppDelegate : NSObject <UIApplicationDelegate> {
    UIWindow *window;
    BonjourViewController *viewController;

    //---use this to publish a service---
    NSNetService *netService;
}
@property (nonatomic, retain) IBOutlet UIWindow *window;
@property (nonatomic, retain) IBOutlet BonjourViewController *viewController;

@end
```

2. 在 BonjourAppDelegate.m 文件中，添加以下粗体语句：

```
#import "BonjourAppDelegate.h"
#import "BonjourViewController.h"

@implementation BonjourAppDelegate

@synthesize window;
@synthesize viewController;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after app launch
    [window addSubview:viewController.view];
    [window makeKeyAndVisible];

    //---publish the service---
    netService = [[NSNetService alloc]
        initWithDomain:@""
        type:@"_MyService._tcp."
        name:@""
        port:9876];
    netService.delegate = self;
    [netService publish];
    return YES;
}
-(void)netService:(NSNetService *)aNetService didNotPublish:(NSDictionary *)dict {
    NSLog(@"Service did not publish: %@", dict);
}
-(void)applicationWillTerminate:(UIApplication *)application {
    //---stop the service when the application is terminated---
    [netService stop];
}
-(void)dealloc {
    [netService release];
    [viewController release];
    [window release];
    [super dealloc];
}
@end
```

### 工作原理

要在网络上发布服务，你可以使用 `NSNetService` 类来通告你在网络上的存在。

```
NSNetService *netService;
```

在这里，当应用程序完成启动（`application:DidFinishLaunchingWithOptions:`）时，你通过发布网络服务来通告你在网络上的存在。通过向 `NSNetService` 类传递几个参数来发布网络服务：

```
netService = [[NSNetService alloc]
initWithDomain:@""
type:@"_MyService._tcp."
name:@""
port:9876];
```

第一个参数指定服务的域。使用 `@""` 表示默认域。第二个参数表示服务类型和传输层。在此示例中，你将服务命名为 MyService，并使用 TCP 作为协议。注意，你需要为服务名称和协议加上下划线 (_) 前缀，并让协议以句点 (.) 结尾。第三个参数指定服务的名称——在此情况下你使用了空字符串。最后，通过第四个参数指定发布服务所使用的端口号。

若要发布服务，请使用 `NSNetService` 类的 publish 方法：

`[netService publish];`

你还实现了 `netService:didNotPublish:` 方法，这样，如果服务未能成功发布，你就可以向调试器控制台写入一条消息（或者向用户显示一个提醒）。

当应用程序退出（applicationWillTerminate:）时，你将停止发布服务：

```
- (void)applicationWillTerminate:(UIApplication *)application {
    //---stop the service when the application is terminated---
    [netService stop];
}
```

## 浏览服务

现在你已经了解了如何发布服务，下面来看看如何浏览已在网络上发布的服务。你将使用 `NSNetServiceBrowser` 类来发现网络上发布的服务。

### 试一试  浏览网络上的服务

1. 使用上一个“试一试”中的 Bonjour 项目，在 BonjourViewController.h 文件中添加以下粗体语句：

```
#import <UIKit/UIKit.h>

@interface BonjourViewController : UIViewController {
    IBOutlet UITableView *tbView;
    IBOutlet UITextView *debug;

    //---use for browsing services---
    NSNetServiceBrowser *browser;
    NSMutableArray *services;
}

- (void) resolveIPAddress:(NSNetService *)service;
- (void) browseServices;

@property (nonatomic, retain) UITableView *tbView;
@property (nonatomic, retain) UITextView *debug;

@property (readwrite, retain) NSNetServiceBrowser *browser;
@property (readwrite, retain) NSMutableArray *services;

@end
```

2. 在 BonjourViewController.m 文件中，添加以下粗体语句：

```
#import "BonjourViewController.h"

#import <netinet/in.h>
#import <arpa/inet.h>
@implementation BonjourViewController

@synthesize tbView;
@synthesize debug;
```
