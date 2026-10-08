features of the language. It keeps track of all of the class and protocol metadata and exposes this to programmers.

When you use key-value coding, you are (indirectly) using Objective-C runtime functions to look up methods and instance variables on the receiver.

# Sending Messages by Name

```
id obj = [NSObject new];
sel = NSSelectorFromString("release");
IMP release = [obj methodForSelector:sel];
release(obj, sel);
```

From: methodName.m
Objective-C methods are C functions that are called via an ind layer. Exactly how this is implemented varies a bit between runtimes. With the NeXT and Apple runtimes, simple message sends are implemented using the objc_msgSend() function.

Unfortunately, this is not the only function that you need. This function is declared as returning an id and will work with any kind of method that has the same calling convention. On Darwin/x86, for example, object pointers are returned in the eax register. If you return a floating point value, it is returned in a floating point register. If you return a structure, space for it is allocated in the caller and a pointer is