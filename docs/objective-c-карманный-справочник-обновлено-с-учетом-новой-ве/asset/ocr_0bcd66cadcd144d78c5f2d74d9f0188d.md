# CHAPTER 14: Threads

this keyword. Although it is familiar to Java programmers, the implementation is very inefficient. It needs to associate a lock with the object, and it always uses a recursive lock even when this isn't ideal. You can achieve the same effect by making sure that you send the -unlock message in an @finally block.

You can avoid the @try and @finally block if you are sure that none of the called methods or functions will throw an exception, but with the GNU and Modern Apple runtimes they don't have any run-time penalty.

# Storing Thread-Specific Data

```
NSMutableDictionary *threadDict = [[NSThread currentThread] threadDictionary]; [threadDict setObject:@"default" forKey:@"NewKey"];
```

From: threadDict.m
Once you have threads, you often want to store some data privately to the thread. An example of this in Cocoa is the current graphics context, which must be available to any code that is drawing, but must not be shared between threads.

Typically, you implement this using the pthread_set_specific() function, which stores a pointer associated with the current thread. This is commonly implemented by storing the