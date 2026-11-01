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

> **WARNING** If you do not start the audio player, the voice chat will not work.

You then retrieve a singleton instance of the GKVoiceChatService class and call its startVoiceChatWithParticipantID:error: method to start the voice chat:

```
if (![[GKVoiceChatService defaultVoiceChatService]
    startVoiceChatWithParticipantID:peerID error:&error]) {
    NSLog(@"Error starting startVoiceChatWithParticipantID: %@",
        [error userInfo]);
}
```

Calling the startVoiceChatWithParticipantID:error: method invokes the voiceChatService:sendData:toParticipantID: method (which is defined in the GKVoiceChatClient protocol), which makes use of the current Bluetooth session to send the configuration data to the other connected device:

```
-(void) voiceChatService:(GKVoiceChatService *)voiceChatService
    sendData:(NSData *)data
    toParticipantID:(NSString *)participantID {
    [currentSession sendData:data toPeers:
        [NSArray arrayWithObject:participantID]]
```