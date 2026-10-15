methods C#-style, but to still label the parameters in a way that feels comfortable to them as Objective-C developers. You can rewrite the previous method call like this:

```
car.Accelerate(mph:65, units:SpeedUnits.MPH, lightsOn:false);
```

In this version of the method call, it is much easier to tell exactly what is being passed to the method and what the method expects. Just by using named parameters, your code becomes a lot easier to read, and code that’s easier to read is easier to maintain.

# A Note on Conventions and Named Parameters

I highly recommend that developers who are planning to write code for both environments get into the habit of using named parameters when writing their WP7 code. It will make the context switching between iOS and WP7 development far less jarring and will actually promote a good practice of making your code as self-documenting as possible. In short, skip named parameters only for the simplest, most obvious of methods. Trust me, when you put down your WP7 project for four weeks to work on your iOS project and then come back to a WP7 project without a single named parameter, you will want to stab yourself with a rusty, blunt object. So, save yourself the trip to the ER and embrace named parameters.

# Memory Management

Whenever iOS and .NET developers get into the same room, things typically remain civil and often lighthearted for a long time. Then someone mentions that the iPhone doesn’t have garbage collection. This is when the steak knives, slings, and USB rocket launchers come out and a war begins. Memory management on mobile devices is an enormously important topic—and one that is equally important to developers of iOS or WP7 applications, regardless of whether the runtime has a garbage collector.

This section provides a discussion of reference counting—the memory management system on iOS devices—and garbage collection, the memory management system on WP7 devices. Even if you are a seasoned .NET developer, I highly recommend that you read through this section because, as you will see, it is possible to cause memory-related application crashes even in a garbage-collected environment.

# Reference Counting and Object Ownership

Reference counting is the means by which allocated objects in memory in Objective-C are deallocated. One of the core skills of any iOS developer is the ability to get a firm grasp of retain/release counts.

For those of you reading this who don’t know what retain and release mean, they are messages that are sent to objects to increase or decrement the reference count. When an object wants to take ownership (indicate to the system that it doesn’t want said object freed from memory until it specifically says it’s done with it) of another object, it sends it the retain message. When it is done with the other object, it sends it the release message and, in good practice, the variable is set to nil (called nil in Objective-C, null in C#).