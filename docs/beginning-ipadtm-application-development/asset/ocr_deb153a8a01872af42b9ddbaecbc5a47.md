```
[alert show];
[alert release];
}
```

Here, the received data is in the NSData format. To display it using the UIAlertView class, you convert it to an NSString object.

# IMPLEMENTING VOICE CHATTING

Another cool feature of the Game Kit framework is the support for voice chat.

The Voice Chat service in the Game Kit allows two devices to establish a voice chat. The voice chat takes place over either an Internet or Bluetooth connection. This section shows you how to implement voice chatting over a Bluetooth communication channel.

# TRY IT OUT Bluetooth Voice Chatting

codefile BluetoothChat.zip available for download at Wrox.com

+   1. Using Xcode, create a new View-based Application project and name it BluetoothChat.
+   2. Add the GameKit and AVFoundation frameworks to the Frameworks folder of the project (see Figure 15-8).
+   3. Add the following bold statements to the BluetoothChatViewController.h file:

```
#import <UIKit/UIKit.h>

#import <GameKit/GameKit.h>
#import <AVFoundation/AVFoundation.h>

@interface BluetoothChatViewController : UIViewController <GKVoiceChatClient>

GKSession *currentSession;

IBOutlet UIButton *connect;
IBOutlet UIButton *disconnect;

GKPeerPickerController *picker;

@end

@property (nonatomic, retain) GKSession *currentSession;
@property (nonatomic, retain) UIButton *connect;
@property (nonatomic, retain) UIButton *disconnect;

- (IBAction) btnMute:(id) sender;
- (IBAction) btnUnmute:(id) sender;
- (IBAction) btnConnect:(id) sender;
```