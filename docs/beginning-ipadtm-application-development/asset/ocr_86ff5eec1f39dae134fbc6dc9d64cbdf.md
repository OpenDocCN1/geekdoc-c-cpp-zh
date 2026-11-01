```
withDataMode:GKSendDataReliable error:nil];
}
```

When it has received the configuration data, the other device starts the Voice Chat service by calling the receivedData:fromParticipantID: method (also defined in the GKVoiceChatClient protocol):

```
- (void) receiveData:(NSData *)data
fromPeer:(NSString *)peer
inSession:(GKSession *)session
context:(void *)context {
    [[GKVoiceChatService defaultVoiceChatService]
    receivedData:data fromParticipantID:peer];
}
```

The GKVoiceChatService uses the configuration information that was exchanged between the two devices and creates its own connection to transfer voice data.

You can mute the microphone by setting the microphoneMuted property to YES:

```
[GKVoiceChatService defaultVoiceChatService].microphoneMuted = YES;
```

# SUMMARY

You have seen how easy it is to connect two iPads (or iPhones and iPod touches) using Bluetooth. Using the concepts shown in this chapter, you can build networked games and other interesting applications easily. You also saw how the Game Kit framework provides the GKVoiceChatService class that makes voice communication between two devices seamless. There is no need for you to know how the voices are transported between two devices — all you need to know is to call the relevant methods to initialize the chat. One important point you need to know, though — voice chat works not just over Bluetooth; it works over any communication channel. In fact, if you have two devices connected using TCP/IP, you can stream the voices over the wire.

# EXERCISES

+   1. What is the class that you can use to locate peer Bluetooth devices?
+   2. Name the object that is responsible for managing the session between two connected Bluetooth devices.
+   3. Name the method from the GKVoiceChatService class that you need to call to establish a voice chat.
+   4. Name the two methods defined in the GKVoiceChatClient protocol that establishes a voice chat channel.
+   
+   Answers to the Exercises can be found in Appendix A.