This declares an instance method named `initWithName:`. The method takes a pointer to an NSString named `newName` as its only argument.

The return type of initWithName: is id. We use id to mean a pointer to any type when we don’t want to specify exactly what that type is. In other words, id is what we use in Objective-C to point to an instance of a class. We used id in Section 3.3, *Methods with Arguments*, on page 53 as a parameter type.

+   - `(IBAction) goBack:(id) sender`

This was the message sent to the WebView when the Back button was clicked.² The way we wired it up, the sender of the message was an NSButton *. We could have introduced a completely different element and used it to initiate the goBack: message, so the type of the sender would have been different. We capture this need for flexibility by setting the type of the sender to be id.

You don’t write id * because id is a pointer. This can be confusing because id stands in for pointers like NSButton * and NSString *. But id appears without the asterisk.

In our example, we use id as the return type for any init name (including our own initWithName: and others), as described in Apple’s *The Objective-C Programming Language* [App09].

# 5.2  Working with Nonobject Types

Objective-C sits on top of C, so you can use the primitive C types such as int, long and float, and so on. But you also come across other types that aren’t primitives but also are not first-class objects.

For example, if you look at the first line of the labelWithText: method in HelloWorldAppDelegate.m, you’ll see this:

```
NSRect labelFrame = NSMakeRect(20, 20, 540, 50);
```

You probably didn’t think much about this when we first typed it in, but now it looks as if it might be missing its *. It’s not. If you check the docs, you’ll see that an NSRect is a struct consisting of an NSPoint and an NSSize. These are each in turn defined to be structs consisting of two CGFloats. Follow the docs one more step, and you see that CGFloat is

2. We’ll look at the IBAAction return type in Chapter 7, *Outlets and Actions*, on page 124. An IBAction is the same as a void except that Interface Builder is able to expose some information to us. Check in the docs, and you’ll see that IBAction is #defined to void.