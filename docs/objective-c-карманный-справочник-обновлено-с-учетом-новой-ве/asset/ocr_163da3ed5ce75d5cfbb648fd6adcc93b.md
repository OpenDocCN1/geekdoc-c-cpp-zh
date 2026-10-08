address. Various other standard objects implement it in different ways. Collection classes, for example, print their contents in property list format. This example returned a very unhelpful message, but in your code you should try to provide something a bit more helpful.

# Recognizing Memory Problems

```
id pool = [AutoreleasePool new];
MutableString *str = [MutableString stringWith:@
```

From: prematureDealloc.m

One of the most common problems in Objective-C is premature deallocation. If you omit a -retain somewhere, then you hang onto a pointer without increasing its reference count. If something else has a reference to it, or it was autoreleased, then this pointer can remain valid for a long time before suddenly becoming invalid.

When the pointer becomes invalid, you will usually get a crash inside objc_msgSend() with the Mac runtime, or objc_msg_lookup() with the GNU runtime. This happens because the runtime tries to look up the method to handle a