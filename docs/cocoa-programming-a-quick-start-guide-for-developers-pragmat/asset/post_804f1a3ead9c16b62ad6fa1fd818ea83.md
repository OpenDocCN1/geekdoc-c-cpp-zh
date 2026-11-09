
## Chapter 6 Memory

You’ve learned how to create objects in Interface Builder and in code. You’ve seen how to send messages to objects, and you’ve used properties to change the state of some of your objects. In this chapter, you’ll learn the rules for managing memory in your Cocoa applications.

Whenever you create an object, you’re using a small chunk of memory. If, at some point later, you’re no longer using that object, you want to make sure that memory chunk is no longer spoken for. Over the lifetime of a program, you may end up creating thousands or millions of transient objects. If you don’t arrange for these to be tidied up, all that memory will just be wasted (and, what’s worse, unavailable to other applications). So, as responsible developers, we make sure that all these wasted objects are returned to the pool of available memory.

If you fail to reclaim objects you’re no longer using, your application leaks memory. Over time, it will grow and grow, sometimes to the point where it can no longer run (or it prevents other programs from running).

On the other hand, if you reclaim an object that is still being used, there’s a chance that this object will be overwritten by other code that grabs the reclaimed memory—this will lead to data corruption.

And that’s what this chapter is about—how to organize things so that memory is reclaimed when it is no longer needed but not before.^1

1. As you follow along in this chapter, every once in a while your program may fail when it shouldn’t or not fail when it should. Select Build > Clean All Targets..., and try to run again.

### 6.1 Reference Counting

Reference counting is the technique we use to manage the memory of objects ourselves. The rules for memory management are simpler to express than to apply:

- If you own an object, you are responsible for releasing it when you are finished with it. Claiming ownership of an object increases its reference count. Releasing that object decreases the count. An object is unused when its reference count is zero.
- If you don't own an object, you should never release it.

If you violate the first rule, you cause a memory leak. If you violate the second rule, then you could be causing an object to disappear while others still need to send it messages.

So, when do you own an object?

Any time you create a new object using `alloc`, you own the object and need to release it when you are no longer using it. There is also a class method named `new`, which is a combination of `alloc` and `init`. In other words, the following does exactly the same thing:

```objective-c
Greeter *host = [[Greeter alloc] init];
```

as the following:

```objective-c
Greeter *host = [Greeter new];
```

We tend not to use `new` in Objective-C even though it’s available. The point here is that when you use it, you own the object. The reference count is increased by one, and you are responsible for releasing it when you are finished with it.

You may also want to take ownership of an object that has been created elsewhere. When you are given an object you need to hold on to, you are responsible for sending a `retain` or `copy` message to the object. This increases its reference count by one. Whether you create an object using `alloc` or `new` or if you hold onto one using `retain` or `copy`, you now own that object and are responsible for releasing it when you no longer need it.²

2. You'll soon see that if instead you create an object using a class method, you have not retained that object. It is autoreleased. If you want to hold onto the newly created object, you must explicitly retain it.

### 6.2 Finding Leaks with the Clang Static Analyzer

To make things easier up to this point, you might remember that I had you turn automatic garbage collection on. To cause a leak, we need to turn garbage collection off. Choose the menu item Project > Edit Project Settings, and on the Build tab, filter for the garbage collection setting. Set the value of Objective-C Garbage Collection to Unsupported.

![](img/9355405953264484a02198b0e3d25b7e_103_0.png)

Now let’s cause a deliberate memory leak.

To start with, I’m going to remove the GUI code from HelloWorldAppDelegate. Clean up HelloWorldAppDelegate.h like this:

Download Memory/HelloWorld17/HelloWorldAppDelegate.h

```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloWorldAppDelegate : NSObject <NSApplicationDelegate> {
}
@end
```

Reduce the implementation file so that all it does is create a Greeter object and log it:

Download Memory/HelloWorld17/HelloWorldAppDelegate.m

```objective-c
#import "HelloWorldAppDelegate.h"
#import "Greeter.h"

@implementation HelloWorldAppDelegate

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    Greeter *host = [[Greeter alloc] initWithName:@"Maggie"];
    NSLog(@"Greeter %@", host);
}
@end
```

We caused the problem, so we can certainly see what’s wrong. We created an instance of the Greeter class using alloc and pointed to this object with the variable host. The reference count is one. We never send the release message to host, so its reference count never reaches zero, and the memory is never reclaimed.

This is a very short and short-lived program, so this doesn’t cause much of a problem for us. You can imagine that it is part of a much bigger program, and we might have to search for the problem first. In Snow Leopard, this leak will be pretty easy for you to detect using the Clang Static Analyzer.

Run the Clang Static Analyzer by choosing the menu item Build > Build & Analyze or using the keyboard shortcut ⌘⇧A.

![](img/9355405953264484a02198b0e3d25b7e_105_0.png)

The report tells us that an object has been allocated and stored into host with a retain count of 1. You may see three problems reported instead of the one pictured previously—if you click each, you'll see that they are reporting the same issue, and when we fix it, they will all disappear. After host is used in the log statement, it is never referenced again. That's our memory leak. The Greeter object is instantiated and used and then hangs around for as long as the GUI window remains open without ever being used again.

### 6.3 Fixing the Memory Leak on Mac OS X

To fix the memory leak on Mac OS X, go back to your project settings, and change the setting for Objective-C Garbage Collection from Unsupported to Required.

Click Build & Analyze, and the memory leak has disappeared.

Whoa—you just learned a whole new way to manage memory. No need for reference counting and balancing your alloc, new, retain, or copy with a release. In this book, I’m assuming that you are deploying to Leopard or later, so the advice is that simple:

Turn garbage collection on.

People who have mastered reference counting feel that trusting the garbage collector is an affront to them as programmers. It’s not. If you are programming for Mac OS X, turn on the garbage collector, and leave reference counting behind.

The first garbage-collected system I worked with was Java. Back in the really old days of Java, everything would come to a halt when the garbage was collected. In fact, there was an animation that would appear on the screen. It was a bulldozer collecting stuff.

For a while people would study the byte code generated by the compiler and look for little optimizations. One of them involved turning for loops around so that instead of incrementing from 0 to some limit, it was more efficient to decrement from that limit to 0.

But while we were learning these clever little hacks, the garbage collector was getting better at optimizing for situations that naturally arose. It turned out that our clever little hacks were now making it harder for the garbage collector to do its job.

That’s kind of where we are now with Cocoa on the desktop.

That said, you still need to understand reference counting. We’ll soon explore an iPhone example where you have no other choice but to manage your memory manually. First I want to show you what the garbage collector can and can’t help with when it comes to the memory attribute for properties.

### 6.4 Properties and Garbage Collection

Now that we have garbage collection turned on, let’s reconsider the property declarations in the Greeter header file:

```objective-c
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
}
```

