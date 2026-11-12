

The @implementation block is even closer to the class version. The only change is the addition of the category name in parentheses.

```objc
@implementation ClassName (CategoryName)
// Implement the extensions methods here.
@end
```

Here is a simple Stack category on the NSMutableArray class.

```objc
// In Stack.h
#import <Foundation/Foundation.h>
@interface NSMutableArray (Stack)
- (void)push:(id)object;
- (id)pop;
@end

// In Stack.m
#import "Stack.h"
@implementation NSMutableArray (Stack)
- (void)push:(id)object {
    [self addObject:object];
}
- (id)pop {
    // Return nil if the stack is empty.
    if (self.count == 0) return nil;
    // Remove the last object from the array and return it.
    id object = [self lastObject];
    [self removeLastObject];
    return object;
}
@end
```

I’m not going to lie to you. Before iOS 5.0, memory management was undoubtedly the most difficult part of iOS development. Here’s the problem in a nutshell. Whenever you create a variable, you set aside some space in memory. For local variables, you typically use memory on the stack. This memory is managed automatically. When a function returns, any local variables defined within that function are automatically removed from memory.

This sounds great, but the stack has two important limitations. First, it has a very limited amount of space, and if you run out of memory your application will crash. Second, it is hard to share these variables. Remember, functions pass their arguments and returns by value. That means everything going into or out of a function gets copied. This isn’t too bad if you are just tossing around a few ints or doubles. But what happens when you start moving around large, complex data structures? Pass an argument from function to function, and you find yourself copying the copy of a copy. This can quickly waste a lot of time and memory.

Alternatively, we can declare variables on the heap and use a pointer to refer to the memory space. This has several advantages. We have considerably more space available on the heap, and we can pass pointers around freely; only the pointer gets copied, not the entire data structure.

However, whenever we use the heap we must manually manage its memory. When we want a new variable, we must request enough space on the heap. Then, when we’re done, we must free up that space, allowing it to be reused. This leads to two common memory-related bugs.

First off, you may free the memory but accidentally continue using it. This is called a dangling pointer. These bugs can be difficult to find. Freeing a variable does not necessarily change the actual value stored on the stack. It simply tells the OS that the memory can be used again. This means that pointers to freed memory can appear to work fine. You only get into trouble when the system finally reuses the memory, writing over the old values.

This can cause very strange errors in completely unrelated sections of code. Imagine this: You free Object A’s memory from the heap but accidentally continue to use its pointer. Meanwhile, an entirely unrelated section of code requests a new object, Object B, on the heap. It is given a section of memory that partially overwrites Object A. Now you change a value on Object A. This saves new data somewhere inside Object B—putting B into an invalid state. The next time you try to read from Object B, you get errors (or possibly very, very strange results).

The second common memory error occurs when you forget to free up memory. This is called a memory leak, and it can cause your application to grab more and more memory as it continues to run.

On the one hand, this isn’t necessarily all that bad. All the memory will be freed when the application exits. I’ve even heard of server software that deliberately leaks all its memory. After all, if you’re running thousands of copies of the server anyway, it may be easier to periodically kill and respawn individual copies than to risk crashes from dangling pointers.

However, on the iOS we do not have that luxury. All iOS devices have extremely limited memory. Use too much and your app will shut down. Correct and effective memory management is therefore a vital skill.

For us, our main concern is objects. All objects are created on the heap. Yes, you can create variables for C data types or structs on the heap as well, but this is very rare (consult a good book on C programming for more details). For the most part, iOS memory management means managing the lifecycle of our objects.

## OBJECTS AND RETAIN COUNTS

One of the biggest problems is simply determining which portion of the code should have responsibility for freeing up an object’s memory. In simple examples, the solution always appears trivial. However, once you start passing objects around, saving them in other objects’ instance variables or placing them in collections, things get murky fast.

To get around this problem, Objective-C programmers traditionally used reference counting. When we created an object, it started with a reference count of 1. We could increase the reference count by calling retain on the object. Similarly, we could decrease the reference count by calling release. When the reference count hit 0, the system deleted the object from memory.

This made it possible to pass objects around without worrying about ownership. If you wanted to hold onto an object, you retained it. When you were done, you released it. As long as you got all the retains and releases correct (not to mention autoreleases and autorelease pools), you could avoid both dangling pointers and memory leaks.

Of course, getting it right was never as simple as it seemed. Objective-C’s memory management conventions had a lot of rules and odd corner cases. Furthermore, as developers, we had to get it right 100 percent of the time. So we often resorted to following a robotic set of steps every time we created a new variable. This was tedious. It created a lot of boilerplate code, much of which wasn't strictly necessary, but if we didn't follow every step every single time, we ran the risk of forgetting something when it was really important.

Of course, Apple tried to help. Instruments has a number of tools to track allocations and deallocations and to search for memory leaks. In recent versions of Xcode, the static analyzer has gotten better and better at analyzing our code and finding memory management errors.

Which raises the question: If the static analyzer could find these errors, why couldn't it just fix them? After all, memory management is a tedious, detail-oriented task that follows a strict set of rules—exactly the sort of task that compilers excel at. Apple took their compiler and analyzer technologies and applied them to this task. The result is a brand new technology for managing memory: Automatic Reference Counting (ARC).

### INTRODUCING ARC

ARC is a compiler feature that provides automated memory management for Objective-C objects. Conceptually, ARC follows the retain and release memory management conventions (see Apple's Memory Management Programming Guide for more information). As your project compiles, ARC analyzes the code and automatically adds the necessary retain, release, and autorelease method calls.

For developers, this is very good news. We no longer need to worry about managing the memory ourselves. Instead, we can focus our time and attention on the truly interesting parts of our application, like implementing new features, streamlining the user interface, or improving stability and performance.

In addition, Apple has worked to improve the performance of memory management under ARC. For example, ARC's automated retain and release calls are 2.5 times faster than their manual memory management equivalents. The new @autoreleasepool blocks are 6 times faster than the old NSAutoreleasePool objects, and even objc_msgSend() is 33 percent faster. This last is particularly important, since objc_msgSend() is used to dispatch every single Objective-C method call in your application.

All in all, ARC makes Objective-C easier to learn, more productive, simpler to maintain, safer, more stable, and faster. That's what I call a win-win-win-win-win-win situation. For the most part, we don't need to even think about memory management. We just write our code, creating and using our objects. ARC handles all the messy details for us.

