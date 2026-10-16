# Forcing garbage collection

In some cases, you may want to force the garbage collector to collect whatever may be available for collection at a particular point of execution in your application. For example, if you have just recently allocated and then deallocated a large collection of objects, it may be appropriate for you to tell the garbage collector to start collecting so that those objects can be completely deallocated as quickly as possible.

To do this, you can use the low-level method `objc_collect()`. This method forces the garbage collector to begin a collection cycle. I detail this method later in this chapter.

# NOTE

> When working with converting non-garbage collected code to garbage collection or code which has to function in both environments, the presence of an autorelease pool will act as a hint to the collector that it should attempt a collection as well. This is an undocumented but somewhat well-known feature of the garbage collector.

# Working with void pointers and garbage collection

Another common Objective-C pattern that can cause difficulty in garbage-collected applications is using a `void*` data type for passing application-specific data between callbacks. The advantage of this approach is that the data passed between methods can be any type of data the developer desires. It could be an object, or it could be just a blob of bytes. The receiving method typecasts the `void*` parameter to whatever type of data it expects to receive.

The problem in a garbage-collected environment arises because the void pointer is opaque, and so may be mistaken for an object without a reference, and thus garbage collected. This can occur between the initiating method and the callback method such that the pointer received by the callback method winds up pointing to a deallocated object.

The solution to this problem is to use the Core Foundation methods CFRetain and CFRelease to force a strong reference to be maintained in the global Core Foundation framework. An example of how this works is shown in Listing 4.20.

# Listing 4.20

# Retaining opaque pointers for use with a callback

```
@implementation Baz

-(void)callbackMethodForObject:(id)object withUserInfo:(void *)inData
{
```