# ## REDUCING MEMORY OVERHEAD

In general, unless you have a very good reason to do otherwise, you should always use an SQLite-based store. You should also avoid loading more objects into memory than is absolutely necessary. I also recommend saving changes as you go—rather than letting unsaved changes accumulate in the managed object context. This also helps free up memory and can help you avoid problems with overly long save times.

By default, Core Data only retains objects that have unsaved changes. However, managed objects do retain each other through relationships. This can easily create retain cycles, which will prevent objects from being released. If you find that you are accumulating large numbers of objects in memory, you can break these cycles by re-faulting the objects.

We can manually refault objects by calling the context’s `refreshObject:mergeChanges:` method. We can also clear the entire managed object context by calling its `reset` method.

> > **NOTE:** Calling `reset` on the managed object context will invalidate any objects currently in the context. Be sure to dispose of all references you have to these objects before resetting. Accidentally holding onto these references will produce dangling pointers, leading to errors that are bizarre, intermittent, and otherwise difficult to debug.

![](bbox=[0.0, 0.515, 0.24, 0.633])

# ## LARGE DATA OBJECTS

Adding large binary objects (i.e., images, sounds, videos, etc.) to a persistent store can severely affect performance. Here we get into an area that’s more art than science. How large is large? Well, the answer really depends on how your application uses the data. If you’re only loading one or two objects into memory at a time, then large attributes may not be a problem. If you’re loading hundreds or thousands—you really need to think things through.

In general there are three approaches. You can store the object directly in the data as an attribute. This is usually only recommended for small binary objects.

Next, you can create a separate entity for the data and refer to it using a to-one relationship. This can be particularly helpful if the binary data isn’t always used. When your object is fetched, the to-one relationship will be a fault. You won’t load the binary data unless you actually need it. This is recommended for modestly sized data objects.