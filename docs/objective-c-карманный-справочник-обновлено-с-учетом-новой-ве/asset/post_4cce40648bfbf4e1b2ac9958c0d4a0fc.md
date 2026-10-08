
# Using Weak References

One of the nicest things about Apple’s garbage collection implementation is the existence of zeroing weak references. Pointers that are not retained often referred to as “weak” in Objective-C documentation that predates the garbage collector. These are references that are allowed to persist beyond the lifetime of the object. Unfortunately, there is no automatic way of telling whether they are still valid.

Weak references were found to be so useful with the garbage collector that they are now also supported by ARC, with slightly different semantics. The ARC implementation provided for backwards compatibility does not support weak references, so they can only be used with ARC on Apple platforms if you restrict yourself to OS X 10.7 or iOS 5 and later.

**Note:** Weak references in a reference counted environment, such as those referencing delegates, are commonly used to eliminate retain cycles. This is not needed in a tracing environment, so you can use strong references for pointers to delegates and anywhere else you might have a retain cycle.

If you declare an object pointer `__weak`, you get a zeroing weak reference. This is not counted by the garbage collector when determining if an object is still live and does not increment the object’s reference count when assigned to in ARC mode. If all of the references to an object are weak, it can be destroyed. Afterwards, reading the weak references will return nil.

Weak references are most commonly used in connection with things such as notifications. You will keep a weak reference to an object and keep sending it messages as long as it is referenced elsewhere, then you can have it cleaned up automatically later.

Cocoa now comes with some collections that let you store weak references. Older versions of the Foundation framework provide NSMapTable and NSTHashTable as opaque C types, with a set of C functions to use them. These interfaces are still available, but with 10.5, Apple made these two C types into classes.

The NSMapTable type is a general form of NSDictionary that can be used to store any pointer-sized types as both values and keys. With garbage collection, you can use this class to store mappings to and from strong or weak object pointers as well. This is useful for things such as NSNotificationCenter, so that objects can be collected while they are still registered to receive notifications and can be automatically removed from the notification center when this happens.

The example at the start of this section shows an important difference between ARC and GC modes. If you compile and run this example with garbage collection enabled, you will probably see it print an object address. This is because the garbage collector will still see stale temporaries while scanning the stack.

In contrast, this will always print 0 in ARC mode. ARC, unlike GC, is entirely deterministic. Assigning nil to the strong pointer decrements the object's reference count and triggers deallocation. The weak pointer is zeroed before deallocation begins and is guaranteed to be zero by the time the fprintf() is reached.

# Allocating Scanned Memory

```
id *buffer = NSAAllocateCollectable(
  10 * sizeof(id),
  NSScannedOption);
```
From: gc.m

If you allocate memory with malloc(), it is invisible to the garbage collector. This is a problem if you want, for example, something like a C array containing objects. We've already looked at one solution to this. You can call CFRetain on the object you are about to store and CFRlease() on the old value, and then swap them over.

This is not ideal, although it will work. The other option is to allocate a region of memory from the garbage collector. The NSAAllocateCollectable() function is similar to malloc(), but with two important differences.

The first is that the memory that it returns is garbage collected. There is no corresponding NSFreeCollectable() function. When the last pointer to the buffer disappears, the buffer will be collected.

**Note:** The Apple collector does not support interior references, so you must make sure you keep a pointer to the start of the region. Pointers to somewhere in the middle of the buffer will not prevent it from being freed.

The second difference is that the second parameter to this function defines the kind of memory that you want. If you are going to be using the buffer for storing C types, you can just pass zero here. If you pass NSScannedOption, the returned buffer will be scanned as a possible location of object pointers, as well as pointers to other memory regions returned by NSAllocateCollectable().

# Common Objective-C Patterns

Every programming language encourages a different set of design patterns. Understanding the common ones used throughout the Foundation framework makes understanding the framework as a whole, and writing Objective-C code, a lot easier.
This chapter provides an overview of some of the most common patterns in Objective-C. If you want to read more, you can find a much more detailed overview in Cocoa Design Patterns, by Erik M. Buck and Donald A. Yacktman (Addison-Wesley, 2009).

# Supporting Two-Stage Creation

```
NSMutableString *buffer =
  [[MutableString alloc] init];
NSMutableArray *array =
  [[NSMutableArray alloc]
    initWithObject: buffer];
```
From: allocInit.m

One of the patterns you've probably already seen is the two-stage creation pattern. In traditional, pre-NeXT, Objective-C, you create an object by sending the class a +new message. When you implemented a new class, you would override +new to call the superclass implementation and then perform that class's initialization.

NeXT changed this, splitting object creation and object initialization into two different methods. The +new method still works, but now it sends +alloc message to the class and -init message to the returned object.

The +alloc method itself, by default, calls +allocZone:. This takes an NSZone as an argument. This is an opaque type encapsulating an allocation zone. This was used very heavily on NeXT systems, to make efficient use of the small amount of memory these machines came with. It does not work particularly well on OS X, and is not properly supported by all classes, so it's something of a vestigial feature in a lot of modern Objective-C code.

When you create a new class, you override the -init method, or provide a new designated initializer.

**Note:** You can still find some evidence of the old-style creation in GCC. When +new was used to create objects, it was common to access instance variables from class methods. There is some code in GCC to support this. This feature was deprecated a long time ago, so you now get a warning when you try it.

It is very rare to override +alloc. Occasionally, people do this to implement per-class pools or enforce singletons, but it’s quite unusual. If you are implementing a singleton class, you may override +alloc to return an existing instance if one exists. We’ll look at that later in this chapter.

# Copying Objects

```
@interface Pair : NSObject <NSCopying>
@property (nonatomic, retain) id first, second;
@end
@implementation Pair
  @synthesize first, second;
  (id)copyWithZone:(NSZone*)aZone
  {
    Pair *new = [self-isa allocWithZone:aZone];
    new->first = first;
    new->second = second;
    return new;
  }
@end
```
From: copy.m

The Foundation framework includes a function called CopyObject(). You might logically expect that this will copy an object, and you'd be almost right. It creates a new object with the same class as the original and then uses something like memcpy() to copy the instance variables over.

This works for objects that only have primitive C types as their instance variables, but not so well for others. Object pointers need to be sent a -retain message when they are copied. C pointers may need some other things done to them, particularly if they are opaque types returned from some other library.

Without information about exactly what the relationship between objects is, the copy function
