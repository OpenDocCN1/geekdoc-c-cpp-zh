
become especially problematic if, for example, the item in question is an operating system resource, such as a socket. It might seem tempting to simply move the deallocation from your dealloc method to a finalize method. (I've already discussed how your goal should be to have no finalize method at all.) Remember that in a garbage collected environment, your object may be deallocated at an arbitrary point in the future. In other words, you can't count on your finalize method to be called at any particular point in time in the execution of your application. Therefore, it is possible that the resource that you are expecting to be deallocated in your finalize method is not going to be deallocated until much later in your program's execution than you previously expected.

These two problems combined, result in a situation that requires you to rethink this design pattern and to do a little bit of extra work, both in the object itself, and objects that use that object to ensure that resources allocated by that object are closed properly before allowing the object to be garbage collected.

The easiest way to demonstrate this concept is probably to show you some code. Listing 4.17 shows a typical file wrapper class, which is allocating a resource, a file handle, its initializer, and then deallocating that resource in dealloc method.

## Listing 4.17
### A typical file wrapper class

```
@interface Foo : NSObject
{
    int fileHandle;
}

@end

@implementation Foo

-(id)init
{
    if(self = [super init])
    {
        fileHandle = open(...);
    }
    return self;
}

// methods here...
-(void)dealloc
{
    close(fileHandle);
    [super dealloc];
}
@end
```

To convert this class to an appropriate garbage collectible class, you need to take the deallocation of the file handle out of the dealloc method, and put it in another method that can be called manually by users of your object. For example, a close method.

## Listing 4.18
### A garbage collectible file wrapper

```
@interface Foo : NSObject
{
    int fileHandle;
}
@end

@implementation Foo

-(id)init
{
    if(self = [super init])
    {
        fileHandle = open(...);
    }
    return self;
}
-(void)close;
{
    if(fileHandle != -1)
        close(fileHandle);
    fileHandle = -1;
}

-(void)finalize;
{
    [self close];
    [super finalize];
}
@end
```

## Writing foundation applications with garbage collection

I touched on the subject of Foundation command line applications written with garbage collection briefly before. You already know that to create a commandline Foundation application that uses garbage collection, you must manually start the garbage collector at the beginning of your main function, before you allocate any objects. However, another detail is important for you to understand.

The way that the Objective-C garbage collector works is that it searches for pointers that refer to objects in both the global scope and the current local stack. When it does this, it looks at all of the currently active variables in the local stack. When doing so, it doesn’t take into account whether the local stack variable has been initialized or not. Remember that a variable, before it is initialized, is pointing to memory locations which previously may have contained initialized data for objects or variables that have been previously deleted. In other words, an uninitialized variable in your current stack may be pointing to an object that you allocated in a previous function call but subsequently is no longer referenced. Therefore, the garbage collector may mistakenly think that your local variable may be referencing an object which should be garbage collected.

To prevent this problem from happening, you need to clear the local stack on a regular basis. The low-level Objective-C runtime method you use to do this is objc_clear_stack(OBJC_CLEAR_RESIDENT_STACK). Typically, in a command line Foundation application, one without a run loop provided by the frameworks, you would be providing your own run loop for your own application events to be processed. The top of this run loop is considered to be an ideal location to clear the local stack and prevent this problem from occurring.

Taking these two things into consideration, a typical command line Foundation application main function should probably look something like Listing 4.19.

## Listing 4.19
### Commandline Foundation application main function

```
int main (int argc, const char * argv[])
{
    objc_startCollectorThread();

    // ...

    while(running)
    {
        objc_clear_stack(OBJC_CLEAR_RESIDENT_STACK);

        for(RunnableItem *item in runnableItems)
        {
            [item run]; // ..
        }
    }

    return 0;
}
```

## Working with objects in nib files

An uncommon but difficult to debug problem can occur when working with objects in nib files that have no reference from an instantiated object in your application. Again, the garbage collector searches for any objects which have no references from global objects or objects on the current stack. In some rare cases, you may create a nib file, which contains objects that don’t have references to them, for example, view controllers with no external reference. Under normal conditions, these objects are garbage collected. The solution to this problem is to create an IBOutlet in the object that owns your nib, and connect this outlet to the object in question. This provides a strong reference to the object and prevents it from being garbage collected.

### NOTE

Nib files, or “NeXT Interface Builder” files are used in defining interfaces on iOS and Mac OS. I don’t discuss them in this book other than here since it’s specific to Cocoa and Cocoa Touch. For more information, see the Wiley books Cocoa Developer Reference or Cocoa Touch for iPhone OS 3 Developer Reference.

## Forcing garbage collection

In some cases, you may want to force the garbage collector to collect whatever may be available for collection at a particular point of execution in your application. For example, if you have just recently allocated and then deallocated a large collection of objects, it may be appropriate for you to tell the garbage collector to start collecting so that those objects can be completely deallocated as quickly as possible.

To do this, you can use the low-level method `objc_collect()`. This method forces the garbage collector to begin a collection cycle. I detail this method later in this chapter.

### NOTE

> When working with converting non-garbage collected code to garbage collection or code which has to function in both environments, the presence of an autorelease pool will act as a hint to the collector that it should attempt a collection as well. This is an undocumented but somewhat well-known feature of the garbage collector.

## Working with void pointers and garbage collection

Another common Objective-C pattern that can cause difficulty in garbage-collected applications is using a `void*` data type for passing application-specific data between callbacks. The advantage of this approach is that the data passed between methods can be any type of data the developer desires. It could be an object, or it could be just a blob of bytes. The receiving method typecasts the `void*` parameter to whatever type of data it expects to receive.

The problem in a garbage-collected environment arises because the void pointer is opaque, and so may be mistaken for an object without a reference, and thus garbage collected. This can occur between the initiating method and the callback method such that the pointer received by the callback method winds up pointing to a deallocated object.

The solution to this problem is to use the Core Foundation methods CFRetain and CFRelease to force a strong reference to be maintained in the global Core Foundation framework. An example of how this works is shown in Listing 4.20.

## Listing 4.20
### Retaining opaque pointers for use with a callback

```
@implementation Baz

-(void)callbackMethodForObject:(id)object withUserInfo:(void *)inData
{
```
