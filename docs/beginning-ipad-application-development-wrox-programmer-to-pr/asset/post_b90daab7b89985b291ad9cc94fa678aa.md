
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

**WARNING** *If you do not start the audio player, the voice chat will not work.*

You then retrieve a singleton instance of the GKVoiceChatService class and call its `startVoiceChatWithParticipantID:error:` method to start the voice chat:

```
if (![[GKVoiceChatService defaultVoiceChatService]
startVoiceChatWithParticipantID:peerID error:&error]) {
NSLog(@"Error starting startVoiceChatWithParticipantID: %@",
[error userInfo]);
}
```

Calling the `startVoiceChatWithParticipantID:error:` method invokes the `voiceChatService:sendData:toParticipantID:` method (which is defined in the GKVoiceChatClient protocol), which makes use of the current Bluetooth session to send the configuration data to the other connected device:

```
-(void) voiceChatService:(GKVoiceChatService *)voiceChatService
sendData:(NSData *)data
toParticipantID:(NSString *)participantID {
[currentSession sendData:data toPeers:
[NSArray arrayWithObject:participantID]
}
```

## WHAT YOU LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Looking for peer Bluetooth devices | Use the `GKPeerPickerController` class |
| Communicating between two Bluetooth devices | Use the `GKSession` class. |
| Establishing a voice chat | Call the `startVoiceChatWithParticipantID:error:` method from the `GKVoiceChatService` class<br>On the initiator, call the `voiceChatService:sendData:toParticipantID:` method defined in the `GKVoiceChatClient` protocol<br>On the receiver, call the `receivedData:fromParticipantID:` method defined in the `GKVoiceChatClient` protocol |
| Muting the microphone | `[GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;` |

![](img/744c5ec15e15ca7891c98be71dc25d13_441_0.png)

FIGURE 16-1

3. In the BonjourViewController.h file, add the following bold statements:

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

4. In the BonjourViewController.xib window, perform the following connections:

- Control-click the File's Owner item and drag and drop it over the Table view. Select `tbView`.
- Control-click the File's Owner item and drag and drop it over the Text view. Select `debug`.
- Right-click on the Table view and connect the `dataSource` outlet to the File's Owner item.
- Right-click on the Table view and connect the `delegate` outlet to the File's Owner item.

5. To verify that all the connections are made correctly, right-click on the File's Owner item and view its connections (see Figure 16-2).

![](img/744c5ec15e15ca7891c98be71dc25d13_442_0.png)

### How It Works

Because you'll use the Table view to display the list of users discovered on the network, you need to set the `dataSource` and `delegate` outlets to the File's Owner item. The TextView will be used to show the various things happening in the background. This is very useful for debugging your application and understanding what happens as services are discovered on the network.

## PUBLISHING A SERVICE

With all the views and outlets wired up, you can publish a service using the NSNetService class.
The following Try It Out shows you how.

### TRY IT OUT  Publishing a Service on the Network

1. Using the same project created in the previous section, add the following bold statements to the BonjourAppDelegate.h file:

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

2. In the BonjourAppDelegate.m file, add the following statements in bold:

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

### How It Works

To publish a service on the network, you use the `NSNetService` class to advertise your presence on the network.

```
NSNetService *netService;
```

Here, you advertise your presence on the network by publishing a network service when your application has finished launching (`application:DidFinishLaunchingWithOptions:`). You publish a network service by passing several parameters to the `NSNetService` class:

```
netService = [[NSNetService alloc]
initWithDomain:@""
type:@"_MyService._tcp."
name:@""
port:9876];
```

The first argument specifies the domain for the service. You use @"" to denote the default domain. The second argument indicates the service type and transport layer. In this example, you named the service as MyService and it uses TCP as the protocol. Note that you need to prefix the service name and protocol with an underscore (_) and end the protocol with a period (.). The third argument specifies the name of the service — you have used an empty string in this case. Finally, specify the port number on which the service is published via the fourth argument.

To publish the service, you use the publish method of the `NSNetService` class:

`[netService publish];`

You also implemented the `netService:didNotPublish:` method so that in the event the service is not published successfully, you will write a message to the debugger console (or perhaps display an alert to the user).

When the application exits (applicationWillTerminate:) you will stop publishing the service:

```
- (void)applicationWillTerminate:(UIApplication *)application {
    //---stop the service when the application is terminated---
    [netService stop];
}
```

## BROWSING FOR SERVICES

Now that you have seen how to publish a service, let's see how you can browse for services that have been published on the network. You will use the NSNetServiceBrowser class to discover services published on the network.

### TRY IT OUT  Browsing for Services on the Network

1. Using the Bonjour project from the previous Try it Out, add the following bold statements to the BonjourViewController.h file:

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

2. In the BonjourViewController.m file, add the following bold statements:

```
#import "BonjourViewController.h"

#import <netinet/in.h>
#import <arpa/inet.h>
@implementation BonjourViewController

@synthesize tbView;
@synthesize debug;
```
