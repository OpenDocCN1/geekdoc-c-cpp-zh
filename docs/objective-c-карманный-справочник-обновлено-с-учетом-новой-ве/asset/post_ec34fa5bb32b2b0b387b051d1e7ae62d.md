
# Testing If an Object Understandstands a Method

```
$ gcc -framework Foundation -g -std=c99 weakClass.m && ./a.out
a.out[53194:903] Not linked against AppKit
$ gcc -framework Cocoa -g -std=c99 weakClass.m && ./a.out
a.out[53184:903] View: <NSView: 0x1001163b0>
```

Output from: weakClass

Note the difference in outputs when this example is linked against Cocoa (which links against AppKit and Foundation) and just Foundation. If the NSView class is present, it creates an instance of it. If it isn't, then it just logs a message.
You can also use this in code that must be backwards-compatible with old versions of a framework. If you look up new classes using this mechanism then you get a Nil value that you can handle when they are not present.

# Testing If an Object Understands a Method

```objc
SEL sel = @selector(delegateMethod);
if ([delegate respondsToSelector:sel]) {
    [delegate delegateMethod:self];
}
```

From: respondsToSelector.m

Objective-C code tends to make use of informal protocols. These are groups of messages that a delegate may, optionally, implement.
When you write code that uses them, you need to test whether the class actually implements the method before sending it.

**Note:** This isn't quite true. You can just send the message in an `@try` block and catch the exception that's thrown if it doesn't understand the method. Given the cost of throwing exceptions, however, this is not a recommended approach.

Fortunately, this is very simple to do. NSObject implements a `-respondsToSelector:` method that tests whether the receiver can handle messages with a given selector.

This method is not just implemented by NSObject, it's also part of the NSObject protocol. Other root classes will also implement it. This is very important for forwarding.
This method, in NSObject, calls the `class_respondsToSelector()` runtime function. In other classes, the implementation is different. If you use the runtime functions directly, then you will have quite fragile code.

Most of the time, you want to know whether the object that you are going to send the message can handle the message, not whether it has a method that handles the message. These are the same in some languages, such as C++, but in Objective-C they are very different concepts.

When you send a -respondsToSelector: message to a proxy, it will test whether the real object has a method for that selector. The object wrapped by the proxy might be yet another proxy, which will then forward the request.
You can also test for protocol conformance by sending a -conformsToProtocol: message to a class. Note that this only tests whether the class was declared as adopting the protocol. Classes can adopt protocols without implementing all of their methods (although they shouldn't), but more commonly classes can implement all of the methods in a protocol without explicitly conforming to the protocol.

CHAPTER 19: The Objective-C Runtime

# Forwarding Messages

```objc
@interface Facade : NSObject{
  id delegate;
}
@implementation Facade
-(id)forwardingTargetForSelector:(SEL)aSel {
  return delegate;
}
-(void)forwardInvocation:(NSInvocation*)anInv {
  [anInv invokeWithTarget:delegate];
}
@end```
```

From: forward.m

Messages in Objective-C messages are intended to be similar to Smalltalk messages, rather than C functions. They are late-bound and can be introspected. At the lowest level, they are implemented using C functions, but this is an implementation detail. You can pretend that messages are objects that are passed between other objects, introspected, and then handled by methods.

When you send a message to an object that does not correspond to a method on that object, there are still some ways for the object to handle it. These have evolved a lot over the life of Objective-C.

In old Objective-C code, the object's -forward::: method was called. This was a variadic method and required the receiver to know the structure of the stack frame. NeXT replaced this with -forwardInvocation:. This method is passed an object that encapsulates the message send. The -forwardInvocation: mechanism is very flexible, but it does not have particularly good performance. Creating the object and deconstructing the stack frame costs several hundred times more than a normal message send, meaning that you shouldn't use this mechanism in anything even vaguely performance-critical.

If you use this forwarding mechanism, then you must implement a -methodSignatureForSelector: method. This returns an object that represents the structure of the call frame associated with the message. The NSInvocation class will use this when creating an object encapsulating the message.

With 10.5, Apple introduced a new, faster, forwarding mechanism. If your object implements a -forwardingTargetForSelector: method, this will be called with the selector for the missing method. It can then return an object, and the message will be delivered to that object instead.

This makes things like the façade pattern very easy. You can quickly delegate any method that you don't understand to your delegate. If you need to do some extra handling before or after calling a delegate method, then just implement that method and call the delegate method explicitly.

Note: The two-stage message-sending mechanism used by the GNU runtime does not support this new mechanism, and neither do old versions of the Apple runtime. If you use it, it is a good idea to provide fallback code using --forwardInvocation:. If you are using a recent Apple runtime, or the GNUStep runtime with the non-fragile ABI, you will get the benefit of extra speed. If not, then your code will still work, it will just be slow.

# Finding Classes

```objc
int classCount = objc_getClassList(NULL, 0);
Class *classList = calloc(classCount, sizeof(Class));
objc_getClassList(classList, classCount);
for (int i=0; i<classCount ; i++) {
  [classes addObject:NSStringFromClass(classList[i])];
}
free(classList);
[classes sortUsingSelector:@selector(compare:)];
```

From: classTree

There are two ways of finding an Objective-C class. If you know the name, then you can just use the NSStringFromString() function. This takes a string object as the argument and returns the class, or Nil if there is no registered class with that name.

If you don't know the name of the class, then you need to do something different. There are a few cases when you might want to know a class but do not already know its name.. For example, if you have a plugin architecture, then you might allow the user to specify bundles to load and then want to collect all of the subclasses of a particular class, or all of the classes that conform to a given protocol.

**Note:** When you are testing classes for protocol conformance, it's a good idea to use the runtime functions, rather than sending them a +conformsToProtocol: message. Lots of classes use +initialize for lazy initialization, and sending them a message will cause this code to be run even if you aren't actually using the class.

The objc_getClassList() function will give you an array of classes. This takes two pointers as arguments, one is the array that will be used to return the classes, the other is the size of the buffer. If you call it with NULL as the first argument, then it won't return any classes, but it will let you know how many there are.

Once you have this array, you can iterate over it and inspect the classes. In this example, I just store the class names in an array and then sort it. In the next section, you'll see how to take the class names and print the instance variables and methods for each class.

If you were searching for classes that conform to a specific protocol, then you would instead use the class_conformsToProtocol() function. This will tell you whether the class conforms to the specified protocol. If it does, then you can add it to the list of loaded plugins.
