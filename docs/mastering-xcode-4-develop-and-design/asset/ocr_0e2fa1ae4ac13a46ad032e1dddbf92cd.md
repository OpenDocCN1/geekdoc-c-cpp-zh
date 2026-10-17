```
#4  0x00007fff83b4d84e in -[NSNotificationCenter
→ postNotificationName:object:userInfo:] ()
#5  0x00007fff83e3e3d6 in -[NSApplication
→ _postDidFinishNotification] ()
#6  0x00007fff83e3e30b in -[NSApplication
→ _sendFinishLaunchingNotification] ()
#7  0x00007fff83f09305 in -[NSApplication(NSAppleEventHandling)
→ _handleAEOpen:] ()
#8  0x00007fff83f08f81 in -[NSApplication(NSAppleEventHandling)
→ _handleCoreEvent:withReplyEvent:] ()
#9  0x00007fff83b84e42 in -[NSAppleEventManager
→ dispatchRawAppleEvent:withRawReply:handlerRefCon:] ()
#10 0x00007fff83b84c72 in _NSAppleEventManagerGenericHandler ()
#11 0x00007fff88b50323 in aeDispatchAppleEvent ()
#12 0x00007fff88b5021c in dispatchEventAndSendReply ()
#13 0x00007fff88b50123 in aeProcessAppleEvent ()
#14 0x00007fff84e2c619 in AEProcessAppleEvent ()
#15 0x00007fff83e0e04b in _DPSNextEvent ()
#16 0x00007fff83e0d7a9 in -[NSApplication nextEventMatchingMask:
→ untilDate:inMode:dequeue:] ()
#17 0x00007fff83dd348b in -[NSApplication run] ()
#18 0x00007fff83dcc1a8 in NSApplicationMain ()
#19 0x00000001000010c2 in main (argc=1, argv=0x7fff5fbbf670) at
→ /Users/jnozzi/Path/To/TestApp Suite/TestApp/TestApp/main.m:12
```

If you expand the frames under Thread 1 in the Debug navigator and then slide the detail slider all the way to the right (to reveal all stack frames), you'll see that the information truly is the same. It's nowhere near as pretty as what you see in Xcode's UI, but it's helpful when sharing your misery with other developers in hopes that they can help you.