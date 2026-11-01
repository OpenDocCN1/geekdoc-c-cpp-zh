```
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
    [[GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;
}
-(IBAction) btnUnmute:(id) sender {
    //---unmute the voice chat---
    [[GKVoiceChatService defaultVoiceChatService].microphoneMuted = NO;
}
```