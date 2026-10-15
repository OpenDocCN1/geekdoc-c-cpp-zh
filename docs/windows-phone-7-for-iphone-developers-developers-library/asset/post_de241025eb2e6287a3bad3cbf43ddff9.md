
As we progress throughout the book, you will see more and more ways in which C# and Objective-C differ and how the UI Frameworks (Silverlight and Cocoa Touch/UIKit, respectively) are vastly different.

One other syntactical difference to keep in mind that will often irritate many unprepared Objective-C developers is Boolean statement evaluation. In C (and thus, Objective-C), any expression that evaluates to nonzero, including negative numbers, is considered true. This is not the case in C#, and you will see that idiomatic C# rarely, if ever, has an if statement that occurs without a logic operator specifically to avoid this type of confusion.

For example, the following snippet of Objective-C is quite common because of its C roots:

```
if (memberVariable)
{
    // do something, knowing that memberVariable is not null/non-zero
}
```

Whereas the same evaluation would rarely appear in idiomatic C# and is usually written like this:

```
if (memberVariable == null)
{
    // do something, knowing that memberVariable is null
}
```

Or, to test for null (or empty) strings, you often see code that looks like this:

```
if ((memberVariable == null) || (memberVariable == string.Empty))
{
    // do something, knowing that memberVariable is null or empty
}
```

In this code block, C# takes advantage of logic short-circuiting so that the second condition will not evaluate if the first condition can be used to make the whole statement true. In other words, if the memberVariable is null, it will never attempt to compare it with string.Empty.

C# also has the concept of nullable primitives. In short, you can have a nullable integer or a nullable decimal. It might seem odd to Objective-C programmers, but such constructs can come in handy from time to time, especially when communicating with databases or converting data from disparate sources.

The following few lines of code illustrate how to declare nullable primitive types and how to test to see whether those types have values assigned to them:

```
int? nullableInt;
Nullable<decimal> nullableDecimal;

// do something to the variables
if (nullableInt.HasValue)
{
    // do something, knowing that the value isn't null
}
```

In C#, testing for whether a value is null is often a bit trickier than the equivalent in Objective-C, so C# programmers out of habit generally make very explicit logic statements.

## Method Calls and Message Passing

When we start talking about message passing in Objective-C and method calling in C#, this is where we really start seeing some fundamental differences in the languages.

In Objective-C, to get an object to do some work for you, you have to send it a message. This concept of message passing can be traced directly to Objective-C's Smalltalk heritage.

In conceptual form, message passing is a much less tightly coupled way of getting objects to do work than invoking methods. When you invoke methods in C#, you are executing a specific piece of code at that specific time, by invoking whatever method matches the signature that you're calling.

To indicate that you're sending a message in Objective-C, you enclose the target of the message and all of the parameters to that message in square brackets ([ and ]), as the following code snippet shows:

```
[car accelerateTo:65 inUnits:MPH withLightsOn:NO];
```

In this example, the car object is said to receive the accelerateTo:inUnits:withLightsOn message. What's interesting here is that the Objective-C runtime does not need to know at compile time whether this object will respond to this message. Sure, a warning will appear in Xcode if it doesn't appear as though the object will respond, but that will not prevent the code from compiling. In fact, in Objective-C, you can add messages to which an object will respond at runtime. In this sense, Objective-C is more dynamic than C#.

The same action, when done as a C# method call, would look something like this:

```
car.Accelerate(65, SpeedUnits.MPH, false);
```

Unlike Objective-C, this method call is statically checked at compile time. If a method matching this signature does not exist at compile time, the build will fail. There are dynamic extensions to C# that can make this distinction a little fuzzy, but they are beyond the scope of this book.

Both of these are fairly easy to read, although I would definitely make the case that the Objective-C message passing syntax, in the hands of a good developer, can make for more easily read, self-documenting code.

Before you get discouraged and start thinking that maybe C# isn't up to the task of building your application, C# 4.0 (both in and out of the WP7 SDK) introduced a new but infrequently used feature: named parameters. This allows developers to invoke methods C#-style, but to still label the parameters in a way that feels comfortable to them as Objective-C developers. You can rewrite the previous method call like this:

```
car.Accelerate(mph:65, units:SpeedUnits.MPH, lightsOn:false);
```

In this version of the method call, it is much easier to tell exactly what is being passed to the method and what the method expects. Just by using named parameters, your code becomes a lot easier to read, and code that’s easier to read is easier to maintain.

## A Note on Conventions and Named Parameters

I highly recommend that developers who are planning to write code for both environments get into the habit of using named parameters when writing their WP7 code. It will make the context switching between iOS and WP7 development far less jarring and will actually promote a good practice of making your code as self-documenting as possible. In short, skip named parameters only for the simplest, most obvious of methods. Trust me, when you put down your WP7 project for four weeks to work on your iOS project and then come back to a WP7 project without a single named parameter, you will want to stab yourself with a rusty, blunt object. So, save yourself the trip to the ER and embrace named parameters.

## Memory Management

Whenever iOS and .NET developers get into the same room, things typically remain civil and often lighthearted for a long time. Then someone mentions that the iPhone doesn’t have garbage collection. This is when the steak knives, slings, and USB rocket launchers come out and a war begins. Memory management on mobile devices is an enormously important topic—and one that is equally important to developers of iOS or WP7 applications, regardless of whether the runtime has a garbage collector.

This section provides a discussion of reference counting—the memory management system on iOS devices—and garbage collection, the memory management system on WP7 devices. Even if you are a seasoned .NET developer, I highly recommend that you read through this section because, as you will see, it is possible to cause memory-related application crashes even in a garbage-collected environment.

### Reference Counting and Object Ownership

Reference counting is the means by which allocated objects in memory in Objective-C are deallocated. One of the core skills of any iOS developer is the ability to get a firm grasp of retain/release counts.

For those of you reading this who don’t know what retain and release mean, they are messages that are sent to objects to increase or decrement the reference count. When an object wants to take ownership (indicate to the system that it doesn’t want said object freed from memory until it specifically says it’s done with it) of another object, it sends it the retain message. When it is done with the other object, it sends it the release message and, in good practice, the variable is set to nil (called nil in Objective-C, null in C#).

When your code sends an object the release method and, as a result, the object’s reference count reaches zero, the object is free for deallocation. It will be removed from memory when its reference count reaches zero.

This particular type of memory management is a solution to the classic problem where two objects are working with the same data in memory and one object finishes and disposes of that memory before the other one finishes. With reference counting, both objects can safely work with the data, and neither will dispose of the allocated memory until the shared object’s reference count reaches zero.

One big problem with reference counting in iOS is that it can quickly become difficult to keep track of which code has been retaining your objects and which code is releasing. Something that happens all too often is a memory leak: Objects are allocated and retained and never released, either holding onto the same memory for the lifetime of the application, or worse—continually consuming more and more memory until the application crashes. If you have a memory leak in a loop, chances are, the application will at some point crash.

Thankfully, tools that come with the iOS development SDK include tools for tracking down memory leaks and out-of-control allocation, and with practice, iOS developers can get pretty adept at hunting down and eliminating memory leaks.

That iOS developers often spend a tremendous amount of time hunting down and eliminating problems that stem from retain/release cycles is what causes the knife-wielding bar brawl mentioned earlier. iOS developers often think C# developers are lazy or write inefficient code because their code is garbage-collected. C# developers often think iOS developers are doing everything the “hard way” because they’re manually managing reference counts.

### Garbage Collection

C# removes the burden of manually maintaining reference counts from the developer. When you write code in C# that instantiates classes (you will learn more about working with C# classes in the next chapter), you use the new keyword. When your code is done with an object, many times you can allow the variable pointing at that object to go out of scope, and the garbage collector will eventually take care of that object. Take note of that word, eventually, because it will be important in the next section on finalization.

C# uses a managed heap. This is unlike the way heap memory is managed in Objective-C. Allocation cost on a managed heap is significantly faster than that of a typical C runtime heap. The trade-off occurs with the act of garbage collection. Before we can understand what happens during garbage collection, we need to understand how the runtime knows the difference between good memory and garbage memory.

With Objective-C, the programmer tells the runtime what is garbage by manually decrementing an object’s retain count to zero, which will free the object from memory automatically.
