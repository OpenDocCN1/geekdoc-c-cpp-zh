
**Note:** Command-line tools are typically not stored in bundles. They still have a main bundle object, however. This object has the directory containing the main executable as its path.

the localized version of a named resource, with the specified extension, in the bundle’s resources directory.

You can use this in your code to get the localized version of a resource file stored in your application bundle or from any loaded bundles. If your code is in a framework, you might want to get resources from the framework bundle. This is slightly more complicated than getting code from the main bundle.

The +bundleForClass: method will give you the bundle that contains the code for a specified class. If you think you might move a class into a framework in the future, it’s a good idea to use this method when loading resources.

## Finding Files in System Locations

```objc
NSArray *dirs =
SSearchPathForDirectoriesInDomains(
    NSLibraryDirectory,
    NSAllDomainsMask,
    YES);
```

From: frameworkLoader.m

On OS X, the filesystem layout is quite well defined. You can probably hard-code paths and expect things to work. If you port your code to other platforms, you will find that things break quite significantly.

This was one of the problems that OpenStep programmers encountered quite often. Porting code between Solaris, OPENSTEP, and Windows NT, for example, required changing a lot of hard-coded paths for each platform.

After Apple bought NeXT, they released a new version of OPENSTEP with a MacOS compatibility layer and a new user interface called Rhapsody. This used the same NeXT filesystem hierarchy as OPENSTEP, complete with a /NeXT folder in the root containing the non-UNIX-like parts of the hierarchy.

With Rhapsody DR2, Apple made some significant changes to the directory layout and introduced the layout that is now familiar to OS X users. To make life easier, and to support YellowBox (Cocoa) for Windows, a product that was discontinued soon after, they introduced the NSSearchPathForDirectoriesInDomains() function.

This function returns an array of directories for a specific use. When you call this function, the first argument describes the kind of directory you want. This might be an applications directory, a library directory, and so on. The second is the filesystem domain.

OS X, like OPENSTEP, divides the filesystem hierarchy into a number of domains that all have roughly the same contents, but for different uses. These are ordered, so you should prefer files in higher-priority domains. The four domains are as follows:

- **User**: This domain is inside the user's home directory. Files here are private to the user and completely under the user's control.
- **Local**: The domain containing files local to the machine. On OS X, this includes things such as the /Library directory that may be modified by the local system administrator.
- **Network**: It is quite rare to see anything in this domain. You will not see it on stand-alone machines, or on machines that are part of a heterogeneous network. It is used for directories controlled by the network administrator.
- **System**: The final domain contains system files. In general, you should never write to any location in this domain, although you can read from it. Any modifications that you make may be reverted the next time the user updates the system.

Not every type of directory exists in every domain. For example, there is no documents directory in the system domain, and it would not make sense if there were.

The final argument tells the function whether to expand tildes in the paths. You will almost always pass YES here.

The frameworkLoader.m example shows several of the things we've looked at in this chapter. This example loads a named framework. Because frameworks are bundles, you can use NSBundle for loading them.

This example first gets a list of all of the Library directories in the system. It then looks in them in order to test whether a directory exists in each of them that has the name of the framework and the .framework extension.

If something with the right name exists, the example program tells NSBundle to load it. You can use this code to lazily load frameworks at run time, rather than linking to them explicitly. Alternatively, you can modify it to look in a plugins directory for your application in the library directory, in which case you should look in NSApplicationSupportDirectory. If you build plugins as bundles, you will load them in exactly the same way.

```objc
NSArray *dirs =
SSearchPathForDirectoriesInDomains(
    NSLibraryDirectory,
    NSAllDomainsMask,
    YES);
for (NSString *dir in dirs)
{
  NSString *f =
    [[dir stringByAppendingPathComponent: @"Frameworks"]
      stringByAppendingPathComponent: @"framework"]
      [pathPathExtension: @"framework"];
}
```

From: frameworkLoader.m

## Threads

The original NeXT operating system was built on top of Mach, just as OS X is. Mach supported threads from the very start and was the first UNIX-like systems to do so. More recently, the POSIX threading APIs have provided a cross-platform way of creating and manipulating threads.

On OS X, POSIX threads are implemented on top of Mach threads and Objective-C threads are implemented on top of POSIX threads. You will almost certainly not want to use Mach threads directly—they do not quite match up to the UNIX process model and are tricky to use correctly—but you may wish to use some of the POSIX threading functions directly.

## Creating Threads

```objc
(void)process {
    SEL sel = @selector(process);
    [NSThread newThreadWithTarget:self selector:sel object:nil];
}
```

From: thread.m

Threads in Objective-C are encapsulated in NSThread objects. There are two ways of creating threads. The first one is similar to the standard way, whereas the second is intended to be Java-like.

When you create a thread using NSThread, you can set its priority. The most common thing to do first is either create an autorelease pool or create a new loop. Creating a thread is a relatively expensive operation in Objective-C, just as it is in C. The process must get some memory for the thread’s stack, create all of the kernel data structures for scheduling, and map some additional space for thread-local storage. It is therefore a good idea to keep threads around for a while once you’ve created them.

Creating a run loop in the thread is a good way of doing this. You can then register timers to fire, monitor file descriptors for new data, and use an event-driven style of programming in the new thread. The POSIX specification defines two contention scopes for threads. OS X only implements the system scope.

The NSThread implements threadPriority and setThreadPriority methods as both class and instance methods. When sent to the class, they control the priority of the current thread. When sent to an instance, they control the priority of the thread encapsulated by that object.

The priority of a thread determines how much CPU time it will get and how long it has to wait between being given access to the CPU. With the lower-level POSIX APIs for controlling thread priority, you can also set the scheduler policy. The functions for doing this are all part of the POSIX realtime extensions, which also provide signal queues and so on. This is not exposed (yet) by the Objective-C APIs.

Priorities set with this API are double-precision floating-point values between 0 and 1. These will be scaled to some integer range that the scheduler understands, so you should remember that small differences will be rounded.

## Controlling Priority

```objc
double oldPriority = [NSThread threadPriority];
[NSThread setThreadPriority:0];
[[NSThread mainThread] setThreadPriority:1];
```

From: threadPriority.m
