
If you run this program, you will see that calling one block affects the return value the next time that you call the other.

```
2 2, 4, 4
```

Output from: blockCapture

The next time that you call the linkedCounters() function, you will get a new pair of blocks, referring to a new counter variable. Note the difference between the static and __block storage qualifiers. Both have a similar effect, moving a variable off the stack, and allowing it to persist longer than the function, but they work very differently.

When you declare a variable as static, every single reference to it will refer to the same piece of memory. When you declare a variable as __block, every reference to it from the same scope will refer to the same bit of memory, but you will get a new copy every time that you enter the scope in which it is declared.

## Managing Memory with Blocks

```
block int counter;
int(^block)(void) =
^(void) { return counter++; };
block = [block copy];
Block_release(block);
```

From: blockMemory.m

Memory management in Cocoa traditionally uses reference counting. Blocks work in the same way. There are two functions controlling the reference count of a block. The _Block_copy() function increases its reference count, while the _Block_release() function decreases it.

The first function is not called _Block_retain(), to make it explicit that the returned block may not be the block passed as an argument. In some situations, the block might be allocated on the stack, then copied onto the heap when it is copied. Most of the time, you won't call these functions directly. Instead, you will use macros that lack the underscore prefix. These macros wrap the functions and ensure that the return type is the same as the argument type.

In Objective-C, you can also send blocks -retain,-release, and -autorelease messages, just as you can any other object. In fact, you can send blocks any messages that you want, but they only respond to a few. The compiler won't give a warning if you send any messages to blocks, but you will get a run-time exception.

You should be very careful about sending -retain messages to blocks. The contract for this method requires it to return the receiver. You must use -copy to ensure that stack blocks are copied to the heap. This is especially important in garbage collected mode, where -retain messages are silently ignored. In ARC mode, you don't need to call these functions or send these messages at all: ARC handles all memory management in blocks for you.

Memory management of variables referenced by blocks can be more difficult to understand. The blockRetain.m example shows two blocks that both refer to objects. The first gets a copy of the object pointer, the second gets a shared reference because of the __block storage qualifier.

```
id a = [@"a" mutableCopy];
_block b = [@"b" mutableCopy];
unsigned long (^refCountA)() = ^(
{ return [a retainCount]; };
unsigned long (^refCountB)() = ^(
{ return [b retainCount]; };
printf("%ld%ld\n", refCountA(), refCountB());
refCountA = Block_copy(refCountA);
refCountB = Block_copy(refCountB);
printf("%ld%ld\n", refCountA(), refCountB());
[refCountA release]; [refCountB release];
printf("%ld%ld\n", [a retainCount], [b retainCount]);
```

From: blockRetain.m

## Managing Memory with Blocks 295

When you retain the block that has a copy of the object pointer, the object is also implicitly retained, automatically. Note that this only happens once. When you retain the block a second time, it is not. When the block is destroyed, the object is released.

```
1 1
2 1
3 1152921504606846975
```

Output from: blockRetain

This is not the case for the second block. This block has been freed, so sending it a message has undefined behavior. In this particular run, it returned some data from a random memory location. It might alternatively crash.

It is your responsibility to ensure the object remains valid for as long as one or more of the blocks persists. This is very difficult to do correctly, because blocks, unlike objects, do not have a way of registering cleanup code. This is addressed if you compile in ARC mode. Blocks will automatically retain any objects that are stored in their bound variables and will release them when the block itself is destroyed.

This is also a problem when a block refers to other pointers. Even if a pointer does not have the __block storage qualifier, the memory that it references is not copied. This means that you have to keep track of it just as you would any other memory in C, with the added complication that the block, containing a reference to it, may persist for a long time.

## Performing Actions in the Background

```
dispatch_queue_t q =
    dispatch_get_global_queue(0,0);
__block int count;
dispatch_async(q, ^(void){count++;});
sleep(1);
NSAssert(count == 1,
    @"Counter incremented in background");
```

From: libdispatch.m

If you are using Cocoa on OS X 10.6 or GNUstep on FreeBSD, then you have the option of using libdispatch, branded by Apple as Grand Central Dispatch, for concurrent processing. This library was written by Apple and released under the Apache 2 license. If you use libdispatch, you don't manage threads manually, you manage work queues.

Work queues execute work units of code. There are two sorts of queue, concurrent and FIFO. A concurrent queue will start executing work units in the order that they were added to the queue, but may execute more than one. A FIFO queue will wait for each unit to complete before starting the next. Context switching between threads is relatively expensive. It obviously costs at least as much as setjmp(), because it needs to save the current state and restore it later, but there are also some non-obvious costs. Different threads are likely to be accessing different bits of the program's data at the same time, so switching threads also causes a lot of cache and TLB misses.

With the work queue model, a single thread can run one unit from one queue, then run from another, without constantly switching between the working sets. If you have more cores, you can increase the degree of concurrency to take advantage of them without increasing the number of context switches. When the system is busy, you may reduce the number of threads that application is using so that it can use one core effectively. This is all done automatically by libdispatch.

Grand Central does not depend on blocks, but it is much easier to use in conjunction with blocks. In the simplest case, you just push blocks into a work queue and have them executed in the background. That’s what the example at the start of this section does. It gets a handle to the default queue for the normal priority and pushes a block into it. The queue will then execute this in the background as soon as there is some spare CPU time.

## Creating Custom Work Queues

```
dispatch_queue_t q =
dispatch_queue_create("Example",0);
__block int count;
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ printf("%d\n", count); });
```

From: libdispatch

FIFO comes with three concurrent queues, which are created by default. These are registered at three priority levels: low, default, and high. The number of things that will run concurrently on each of these depends on the load of the system and the number of CPU cores available. You can get a handle to one of these with the dispatch_get_global_queue() function that we saw in the last section.

There is no point in creating a new concurrent queue. Blocks pushed into a concurrent queue will begin executing in the order that they were
