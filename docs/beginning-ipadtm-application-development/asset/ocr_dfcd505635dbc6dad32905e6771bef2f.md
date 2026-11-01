```
@interface BluetoothViewController : UIViewController
<GKSessionDelegate, GKPeerPickerControllerDelegate> {
    GKSession *currentSession;
    IBOutlet UITextField *txtMessage;
    IBOutlet UIButton *connect;
    IBOutlet UIButton *disconnect;
    GKPeerPickerController *picker;
}
@property (nonatomic, retain) GKSession *currentSession;
@property (nonatomic, retain) UITextField *txtMessage;
@property (nonatomic, retain) UIButton *connect;
@property (nonatomic, retain) UIButton *disconnect;
-(IBAction) btnSend:(id) sender;
-(IBAction) btnConnect:(id) sender;
-(IBAction) btnDisconnect:(id) sender;
@end
```

4. Double-click on BluetoothViewController.xib to edit it in Interface Builder. Add the following views to the View window (see Figure 15-2):

+   - Text Field
+   - Round Rect buttons (name them as Send, Connect, and Disconnect)

5. In the BluetoothViewController.m file, add in the following statements in bold:

```
#import "BluetoothViewController.h"
@implementation BluetoothViewController
@synthesize currentSession;
@synthesize txtMessage;
@synthesize connect;
@synthesize disconnect;
```

6. Back in Interface Builder, perform the following actions:

+   - Control-click on the File’s Owner item and drag and drop it over the Text Field view. Select txtMessage.
+   - Control-click on the File’s Owner item and drag and drop it over the Connect button. Select connect.
+   - Control-click on the File’s Owner item and drag and drop it over the Disconnect button. Select disconnect.
+   - Control-click on the Send button and drag and drop it over the File’s Owner item. Select btnSend:.