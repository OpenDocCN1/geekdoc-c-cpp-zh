# Chapter 10: Well-Formed Types

objects are organized into three generations. Each time an object survives a garbage collection cycle, it is moved to the next generation, until it ends up in generation 2 (counting starts from zero). The garbage collector, then, runs more frequently for objects in generation 0 than it does for objects in generation 2.

Over time, in spite of the trepidation that .NET stirred during its early beta releases when compared with unmanaged code, .NET's garbage collection has proved extremely efficient. More important, the gains realized in development productivity have far outweighed the costs in development for the few cases where managed code is dropped to optimize particular algorithms.

All references discussed so far are strong references because they maintain an object's accessibility and prevent the garbage collector from cleaning up the memory consumed by the object. The framework also supports the concept of weak references. Weak references do not prevent garbage collection on an object, but they maintain a reference so that if the garbage collector does not clean up the object, it can be reused.

Weak references are designed for reference objects that are expensive to create, yet too expensive to keep around. Consider, for example, a large list of objects loaded from a database and displayed to the user. The loading of this list is potentially expensive, and once the user closes the list, it should be available for garbage collection. However, if the user requests the list multiple times, a second expensive load call will always be required. With weak references, it becomes possible to use code to check whether the list has been cleaned up, and if not, to re-reference the same list. In this way, weak references serve as a memory cache for objects. Objects within the cache are retrieved quickly, but if the garbage collector recovers the memory of these objects, they will need to be re-created.

Once a reference object (or collection of objects) is recognized as worthy of potential weak reference consideration, it needs to be assigned to System .WeakReference (see Listing 10.14).

+   LISTING 10.14: Using a Weak Reference

```
public static class ByteArrayDataSource
{
    static private byte[] LoadData()
```