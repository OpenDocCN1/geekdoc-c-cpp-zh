
# CHAPTER 16: Notifications

**Note:** On OS X, there is only a single type of distributed notification center, sending notifications to applications owned running with the same user ID as the sender. GNUStep provides two others, one for communicating with all applications on a computer, irrespective of the user, and one for broadcasting notifications across the local network.

The delivery semantics for distributed notifications are also somewhat different. When you post a (normal) notification, it is delivered synchronously. The sending object already has control of the CPU. The stack frame for its method is at the top of the stack and it is free to delegate program flow to the notification center, which then delegates it to the notification listeners.

With a distributed notification, this is not the case. You can't just interrupt whatever process is doing in the middle of a function¹ and you must wait until a convenient point. Distributed notifications handle this by interfacing with the run loop. To receive distributed notifications, you must be using NSRunLoop. The distributedNotify.m example is a simple program that writes a log message whenever a new instance of itself is started.

> ¹Well, you can; signals do exactly that, but the things you can do from a signal handler are quite limited.

# Sending Notifications Between Applications 309

```
- (id)init
NSDistributedNotificationCenter *c = 
[NSDistributedNotificationCenter
defaultCenter];

[c addObserver: self
selector:@selector(newCopyStarted:)
name: ProcessDidStart
object: nil
suspensionBehavior:NSNotificationSuspensionBehaviorHold];

ProcessInfo *pinfo =
[ProcessInfo processInfo];
NSNumber *pid = [NSNumber numberWithInt:
[pinfo processIdentifier]];
NSDictionary *userInfo = [NSDictionary initWithObject:pid
forKey:@"pid"];

[c postNotificationName: ProcessDidStart
object:[pinfo projectName]
userInfo: userInfo
options: 0];
[[NSRLoop currentRunLoop] run];
```

From: -init method of this class does all of the real work. First, it registers an observer for a distributed notification. The object is nil, so it will receive this notification from any sender. Then it constructs the notification. The user info dictionary contains a single key-value pair storing the process ID.

After it's posted the notification, it starts the run loop. The program will then sit in a blocking state until some run loop events happen. Only one event has a handler defined in this program, so all that it will ever do is receive a -newCopyStarted: message whenever a ProcessDidStart: notification is posted, which will only happen when another copy of this program is run.

If you compile and run this example, you will see that it receives its own notification, so it will tell you that it has started. If you run another copy, you will get a log message from each running instance telling you about the new one.

This is quite a trivial example, but it's easy to use distributed notifications for more complex events. I use them in XMPPPKit, for example, to notify all running applications when the user changes online state. Other programs listen for this and can push the new status message to microblogging sites.

# Network Access

The standard cross-platform way of writing network-aware applications is the Berkeley Sockets API. This was written as part of the same grant that developed the TCP/IP and is designed to be protocol-agnostic.

Most languages have an implementation of this API. In Objective-C, you are, as always, free to use the C version, which provides all of the power of the low-level interfaces.

Most of the time, however, this is a lot of effort for very little gain. The Foundation framework provides several classes that make it easier to write networked applications. Using these abstractions sometimes loses you some of the power of the lower-level APIs, but not much.

# CHAPTER 17: Network Access

# Wrapping C Sockets

```
return
[[NSFileHandle alloc]
initWithFileDescriptor:s
closeOnDealloc:YES]
autorelease];
```

From: NSFileHandle+Socket.m

We looked briefly at the NSFileHandle class in Chapter 13 and I mentioned that it wrapped a file descriptor. The socket API was designed based on the UNIX everything-is-a-file-even-when-it-doesn’t-make-sense model, so sockets are also file descriptors. You can use the same function calls for reading from and writing to a socket that you can use with any other file descriptor.

You can also use an NSFileHandle to wrap a socket. This lets you use the low-level APIs to create a socket to your exact specifications, then use a more abstract way of interacting with the created socket. If you need to use any parts of the low-level socket API that are not conveniently exposed by the higher-level APIs then this is the only solution that you can use. In other cases, it is still often the most convenient one.

The biggest advantage of wrapping your socket in a file descriptor object is that you can easily integrate it with the run loop. This lets you very easily write event-driven socket code. The other

# Wrapping C Sockets 313

**Note:** Remember that the aim of ObjectiveC was to make life easier for C programmers. Don't use Objective-C APIs just for the sake of it, only use them when they make sense as a solution to your specific problem than the C APIs. Using an Objective-C API that is just a trivial wrapper around the C API adds overhead and complexity, but doesn't make your code any easier to maintain.

big advantage is that you can use Objective-C reference counting for your socket. If you pass YES as the argument to closeOnDealloc: when you create the NSFileHandle, the file descriptor will be closed when the object is deallocated.

If you send waitForDataInBackgroundNotify message to your object, it will be added to the list. With OS X 10.6, this is implemented using Grand Central Dispatch to post the notification, but the core functionality is the same.

The documentation for this method is somewhat misleading. It claims that this method will create another thread. In fact, on OS X the run loop uses kqueue() API and calling this

> ¹GNUstep may poll() or select() instead.

# 314 CHAPTER 17: Network Access

method just adds another file descriptor to the list that it waits for. If you have a handler for this notification, then you can read the new data.

One final advantage is that you are freed from thinking about buffers. When you read data from a socket, you typically have to allocate a buffer and then pass a pointer to it to a read() or recv() system call. With a file descriptor object, you need NSData instances.

If you are writing a list of strings, then you might want to consider adding a category on NSFileHandle that provides -writeUTF8String and -readUTF8String methods, or equivalent methods for the encoding that your protocol uses, allowing you to get and send strings directly.

# Connecting to Servers

```
NSInputStream *in;
NSOutputStream *out;
NSHost *host = [NSHost hostWithName:@"example.com"];
[NSStream getStreamsToHost:host port:80 inputStream:&in &out];
[in open];
```

From: nsstream.m
Objective-C provides a set of Java-like classes for network communication, as well as the low-level UNIX interfaces. Unfortunately, the stream versions are not particularly useful. They don’t provide a clean way of adding filters like compression or of negotiating encryption in the middle of a connection, which a lot of modern protocols require.

The most distressing limitation, however, is that they don’t make it easy to support SRV records. These are DNS records that advertise a service to port mapping, as well as a hostname to IP address mapping. They are used by DNS-SD, but the IP address shortage makes them increasingly common in hierarchical DNS on the public Internet.

If you look up a server address on OS X using the POSIX getaddrinfo() function, then you provide a host name and service name. The system then maps these to network addresses and port numbers on any of the supported protocols.

When you construct an NSStream, you must specify the port number as an integer. This means that it will fail on any service that uses DNS SRV records. If you use getaddrinfo() and then wrap the resulting socket in an NSFileHandle, however, it will work correctly. In EtoileFoundation, we provide a category on NSFileHandle that allows you to create file handles directly from a host name and protocol name, wrapping this call.
