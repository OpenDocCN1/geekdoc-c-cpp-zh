
To handle all of the complications in formatting dates, Foundation provides you with the NSDateFormatter class. This class allows you to specify the type of behavior you require and then converts the given NSDate object into a string representation of that date matching the behavior you requested. For example, to display a date using the short, numeric-only style, such as 09/20/10, you would use the NSDateFormatterShortStyle, as shown in Listing 15.9.

## Listing 15.9
### Formatting the date for short numerical format

```
NSDate *date = [NSDate date];
NSDateFormatter *f = [[NSDateFormatter alloc] init];
[f setDateStyle:NSDateFormatterShortStyle];
NSString *dateStr = [f stringFromDate:date]; // yields MM/DD/YY
```

This goes both ways, in that you can also use an NSDateFormatter to convert a natural language string representing a given date to an actual NSDate object. This example is shown in Listing 15.10.

## Listing 15.10
### Converting a natural language string into an NSDate object

```
NSDateFormatter *f = [[NSDateFormatter alloc] init];
[f setDateStyle:NSDateFormatterShortStyle];
NSDate *date = [f dateFromString:@"02/25/10"];
```

Constructing an NSDateFormatter for virtually any date format that you need to work with is impossible, but typically you will use one of the standard sets of formatters that are provided by the system.

## Summary

Working with dates is a complex subject filled with details that can trap the unwary developer. Over the years, Apple and others have put a lot of thought and care into the NSDate and NSCalendar classes to make dates less of a problem for developers. You should avoid manipulating dates manually, and instead use these classes. Doing so saves time.

## IV
### Exploring
### Advanced Topics

## In This Part

- Chapter 16
- Multiprocessing with Threads
- Chapter 17
- Objective-C Design Patterns
- Chapter 18
- Reading and Writing Data with NSCoder
- Chapter 19
- Using Objective-C on Other Platforms

## Multiprocessing with Threads

Threads. Probably no other computing subject strikes more fear and trepidation into the hearts of experienced programmers. It should. Threads cause bugs that are difficult to track down, difficult to reproduce, and maddeningly frustrating to fix. At the same time, however, they promise to unlock more of our multi-computing potential than any other modern software technology. This dual nature makes them a complex subject worthy of an entire chapter dedicated to handling them properly.

Every program has at least one thread, usually called the main thread. The main thread begins execution in your main function and then is responsible for executing the rest of your application unless you explicitly create another thread.

Conceptually, you can think of a thread as a single line of execution through your application by which instructions are executed sequentially. When you create another thread, you actually have two separate threads of execution, running through your application in parallel. If your application is running on a single core, single CPU machine, your threads may appear to be running simultaneously, however, they are actually given different time slices on the CPU. On the other hand, if your application is running on a multicore, or multi-CPU machine, then it is entirely possible for two threads in your application to actually be executing simultaneously.

When two threads are executing simultaneously in this manner, it is possible that the two threads may both try to access the same chunk of memory at the same time. When this occurs, the exact behavior is undefined and as a result, this can cause an error in your program. This circumstance is called an unsafe thread condition. These circumstances only occur when the code which is executing is written without thread safety in mind.

To prevent these kinds of circumstances, you have to prevent one thread from accessing the same memory or data that another thread is accessing at the same time. This is called making your code thread safe. It is vitally important that whenever you use threads you make sure that all of the code that you write is thread safe.

## In This Chapter

- Understanding the causes of thread errors
- Learning how to prevent thread errors with locks
- Using @synchronize
- Creating threads with NSThread
- Using NSOperation and NSOperationQueue

safe. Debugging problems in threads is extremely difficult because often the bug only occurs in very specific very narrow race conditions. This means that a bug might appear on a particular user’s computer because of the speed and configuration of their computer and never show itself on your computer. Additionally, because the debugger specifically can stop your application at particular points and because it narrows the execution of your application down to a specific thread, threading bugs often won’t show up in a debugger at all. It is because of these issues that threading bugs are sometimes known as “heisenbugs”. They get this nickname because you know that they occur, but when you try to observe them they disappear.

Many developers see all of the wonderful thread related tools that they have available in Objective-C, and their first reaction is to think that somehow threads are going to solve all of their design problems. It can be very tempting to fire off threads into the background for various tasks, leaving your main thread free to handle user interface interaction; but doing this is a bad idea. Even in cases like network code, where other languages might encourage you to use threads to prevent blocking I/O, 99 percent of the time, when it comes to Objective-C, using a thread is going to be the wrong tool for the job. Using threads is a technique that should be reserved for narrow requirements, for example situations where you have CPU intensive calculations. Even in these cases, properly written, thread-safe code can be in danger of being blocked by shared resources such as GUI interaction. These problems can cause multithreaded code to, in some cases, actually be slower than the single-threaded alternative.

Objective-C provides a variety of tools for creating and manipulating threads as well as for writing thread safe code. In this chapter, I review some of the key technologies that are required for writing thread-safe code, and then introduce you to some of the classes that make creating and using threads in Objective-C simple.

CAUTION
One note of warning, the Cocoa UI frameworks (UIKit and AppKit) are not, in fact, thread safe. Any interaction with any GUI element in your application at any time must always be done on the main thread. If you must update a GUI element from a background thread, you can dispatch a method to be called on the main thread by using the NSObject method -performSelectorOnMainThread:withObject:... methods to do so.

CAUTION
A common bug which some programmers encounter is in the use of notifications using NSNotificationCenter. Notifications are sent on the thread upon which they are posted. This means that if you post a notification from a background thread that then updates a GUI component, you are in danger of a thread safety issue. Therefore, take care when working with notifications in a threaded application.

## Synchronizing Code

The key to writing thread-safe code is to remember that no thread is ever safe reading or writing a particular chunk of memory that might simultaneously get written to by another thread. If the memory that is being read or written to is also simultaneously changing from underneath the thread, the behavior of the application is undefined. Anything could happen. So the key then is to ensure that when you are writing to a particular block of memory or variable that no other thread will be able to read from it until you are finished.

The most common way to prevent another thread from accessing memory that you’re writing to while you’re writing it is the use of a mutually exclusive lock, or mutex.

## Using Locks

A mutually exclusive lock, or mutex, is an object which prevents the simultaneous access of a common resource (usually memory). It’s called a mutually exclusive lock because it locks out access to the resource and allows exclusive access to only one thread at a time.

The Objective-C foundation framework provides two main types of mutually exclusive locks. The first, and simplest, is the NSLock class. The NSLock class represents a simple mutex that you can instantiate and then lock prior to writing to a particular variable or memory location. Other threads, which want to write to or read from the same variable, should attempt to lock the same NSLock object before initiating their data access. Attempting to lock the NSLock blocks the thread until the lock is unlocked and can be locked again. In this way, the attempt to lock the NSLock will prevent access to the data until the first thread is finished with its access.

To create an instance of an NSLock, you simply instantiate one using the standard alloc/init pattern. Listing 16.1 shows an example of how you do this. Typically, you hold the instance of your NSLock as a member variable of whatever class is accessing the data. It is important that the lock be maintained and available as a variable that both threads can access so that they can acquire the lock accordingly.

## Listing 16.1
### Creating an instance of an NSLock

```
-(id)init
{
    if((self = [super init]))
    {
        lock = [[NSLock alloc] init];
    }
    return self;
}
```

Typically, you would create your instance of NSLock as I’ve shown here in the initializer of the class. Then, within the accessors of the data that you want to protect, you would simply acquire a lock on the NSLock instance before attempting to access the data. Listing 16.2 shows an example of some accessors written using this technique.
