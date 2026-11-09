# Cocoa messaging and notifications

Cocoa includes a separate messaging system with more sophisticated features. *Notifications* are like an internal e-mail or chat service. You can use them to pass information between applications or between objects within an application. Objects can sign up to receive notifications and can post them through a notification center. Notifications can include complex data. They’re a system-level feature, while Objective-C messaging is a language-level feature. The two messaging systems are unrelated and are used in different ways.

# Objective-C syntax

Now that you’ve seen some of the ways in which messaging is used in Cocoa, you may be curious about messaging code. Objective-C uses square brackets to indicate messages. For example:

```
```objective-c
[anObject doSomething];
```
```

triggers the `doSomething` method in anObject.

The messaging syntax can pass parameters.

```
```objective-c
[anObject doSomethingWith: anInt];
```
```

triggers `doSomethingWith:` and passes it an int. Parameter fields can have descriptive name strings. For example, in

```
```objective-c
[anObject doSomethingWith: anInt andABoolToo: YES];
```
```

`doSomethingWith:` and `andABoolToo:` are part of the message syntax. They’re effectively code-based tooltips, included for clarity and legibility, and they don’t affect execution.

![](bbox=[0.103, 0.594, 0.172, 0.651])

> **CAUTION**
> 
> Objective-C treats `aMethod` and `aMethod:` `thatTakesAParameter` as completely different entities. It’s good practice in your own code to keep method names as distinct as possible. Some Cocoa method names don’t do this; you’ll occasionally see an identical method name followed by a number of different parameter groupings. Objective-C understands the difference, but you may find it harder to remember.

This idiom is often used in Cocoa classes to include hints about the purpose of each field. For example

```
```objective-c
[aWindow setHasShadow: YES];
```
```

enables a drop shadow effect for aWindow. Replacing YES with NO turns off the drop shadow. This feature helps make Cocoa code easy to read. But sometimes it gets out of hand. Objective-C is chatty rather than terse, and some Cocoa methods have very long names. The full syntax for the `dragImage:` method built into Cocoa’s `NSWindow` window object is

```
```objective-c
[aWindow dragImage: anImage
          at:aPoint
          offset:anOffset
```
```