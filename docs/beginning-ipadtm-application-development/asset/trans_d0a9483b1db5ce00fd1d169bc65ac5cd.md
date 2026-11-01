

[disconnect setHidden:YES];

[super viewDidLoad];
}

-(IBAction) btnConnect:(id) sender {
    //---Select a nearby Bluetooth device---
    picker = [[GKPeerPickerController alloc] init];
    picker.delegate = self;
    picker.connectionTypesMask = GKPeerPickerConnectionTypeNearby;

    [connect setHidden:YES];
    [disconnect setHidden:NO];

    [picker show];
}

-(IBAction) btnDisconnect:(id) sender {
    //---disconnected from the other device---
    [self.currentSession disconnectFromAllPeers];
    [self.currentSession release];
    currentSession = nil;

    [connect setHidden:NO];
    [disconnect setHidden:YES];
}

-(void) peerPickerController:(GKPeerPickerController *)pk
      didConnectPeer:(NSString *)peerID
      toSession:(GKSession *) session {
    self.currentSession = session;
    session.delegate = self;
    [session setDataReceiveHandler: self withContext:nil];
    picker.delegate = nil;
    [picker dismiss];
    [picker autorelease];
}

-(void) peerPickerControllerDidCancel:(GKPeerPickerController *)pk {
    picker.delegate = nil;
    [picker autorelease];

    [connect setHidden:NO];
    [disconnect setHidden:YES];
}

-(IBAction) btnMute:(id) sender {
    //---mute the voice chat---
    [GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;
}

-(IBAction) btnUnmute:(id) sender {
    //---unmute the voice chat---
    [GKVoiceChatService defaultVoiceChatService].microphoneMuted = NO;
}

```objc
//---returns a unique ID that identifies the local user---
-(NSString *) participantID {
    return currentSession.peerID;
}

-(void) voiceChatService:(GKVoiceChatService *) voiceChatService
    sendData:(NSData *) data
    toParticipantID:(NSString *)participantID {

    [currentSession sendData:data toPeers:
        [NSArray arrayWithObject:participantID]
        withDataMode:GKSendDataReliable error:nil];
}

-(void) session:(GKSession *)session
    peer:(NSString *)peerID
    didChangeState:(GKPeerConnectionState)state {

    switch (state) {
    case GKPeerStateConnected: {
        //---plays an audio file---
        NSString *soundFilePath = [[NSBundle mainBundle]
            pathForResource:@"beep" ofType:@"wav"];

        NSURL *fileURL = [[NSURL alloc]
            initFileURLWithPath: soundFilePath];

        AVAudioPlayer *audioPlayer=
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

        //---initiating the voice chat---
```
if (![[GKVoiceChatService defaultVoiceChatService] startVoiceChatWithParticipantID:peerID error:&error]) {
    NSLog(@"Error starting startVoiceChatWithParticipantID: %@", [error userInfo]);
}
} break;

case GKPeerStateDisconnected: {
[[GKVoiceChatService defaultVoiceChatService]
stopVoiceChatWithParticipantID:peerID];

[self.currentSession release];
currentSession = nil;

[connect setHidden:NO];
[disconnect setHidden:YES];
} break;
}
```

```
-(void) receiveData:(NSData *)data
fromPeer:(NSString *)peer
inSession:(GKSession *)session
context:(void *)context {
//---start the voice chat when initiated by the client---
[[GKVoiceChatService defaultVoiceChatService]
receivedData:data fromParticipantID:peer];
}
```

```
-(void)dealloc {
    if (currentSession) [currentSession release];
    [connect release];
    [disconnect release];

    [super dealloc];
}

@end
```

10. 要测试应用程序，请将应用程序部署到两台设备上。（对于 iPod touch，您需要将其连接到外部麦克风，因为它本身不带麦克风。）然后运行应用程序并按下“连接”按钮，使用蓝牙相互连接。一旦两台设备连接成功，您就可以开始聊天了！要暂时静音对话，请按住“静音”按钮。松开后，对话将恢复。祝您玩得开心！

## 工作原理

当两台蓝牙设备连接时，您首先播放蜂鸣声并启动音频会话（通过 session:peer:didChangeState: 方法）：

```
//---plays an audio file---
NSString *soundFilePath = [[NSBundle mainBundle]
pathForResource:@"beep" ofType:@"wav"];
```

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
    NSLog(@"Error setting category: %@",
        [error localizedDescription]);
}

if (![audioSession setActive: YES error: &error]) {
    NSLog(@"Error activating audioSession: %@",
        [error description]);
}

[GKVoiceChatService defaultVoiceChatService].client = self;
```

> **警告** 如果您不启动音频播放器，语音聊天将无法工作。

然后您检索 GKVoiceChatService 类的单例实例并调用其 startVoiceChatWithParticipantID:error: 方法来启动语音聊天：

```
if (![[GKVoiceChatService defaultVoiceChatService]
    startVoiceChatWithParticipantID:peerID error:&error]) {
    NSLog(@"Error starting startVoiceChatWithParticipantID: %@",
        [error userInfo]);
}
```

调用 startVoiceChatWithParticipantID:error: 方法会调用 voiceChatService:sendData:toParticipantID: 方法（该方法在 GKVoiceChatClient 协议中定义），该方法利用当前的蓝牙会话将配置数据发送到另一台已连接设备：

```
-(void) voiceChatService:(GKVoiceChatService *)voiceChatService
    sendData:(NSData *)data
    toParticipantID:(NSString *)participantID {
    [currentSession sendData:data toPeers:
        [NSArray arrayWithObject:participantID]
        withDataMode:GKSendDataReliable error:nil];
}
```

当接收到配置数据后，另一台设备通过调用 receivedData:fromParticipantID: 方法（也在 GKVoiceChatClient 协议中定义）启动 Voice Chat 服务：

```
- (void) receiveData:(NSData *)data
fromPeer:(NSString *)peer
inSession:(GKSession *)session
context:(void *)context {
    [[GKVoiceChatService defaultVoiceChatService]
    receivedData:data fromParticipantID:peer];
}
```

GKVoiceChatService 使用在两台设备之间交换的配置信息并创建自己的连接来传输语音数据。

您可以通过将 microphoneMuted 属性设置为 YES 来静音麦克风：

```
[GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;
```

## 总结

您已经看到使用蓝牙连接两台 iPad（或 iPhone 和 iPod touch）是多么容易。使用本章介绍的概念，您可以轻松构建联网游戏和其他有趣的应用程序。您还看到了 Game Kit 框架如何提供 GKVoiceChatService 类，使两台设备之间的语音通信变得无缝。您无需知道语音如何在两台设备之间传输——您需要知道的只是调用相关方法来初始化聊天。不过有一个重要点需要注意——语音聊天不仅仅适用于蓝牙；它适用于任何通信通道。事实上，如果您使用 TCP/IP 连接两台设备，您可以通过线路传输语音。

## 练习

- 1. 您可以使用哪个类来定位对等蓝牙设备？
- 2. 名称负责管理两个已连接蓝牙设备之间会话的对象。
- 3. 从 GKVoiceChatService 类中命名您需要调用以建立语音聊天的方法。
- 4. 命名在 GKVoiceChatClient 协议中定义的建立语音聊天通道的两个方法。
- 
- 练习的答案可在附录 A 中找到。

