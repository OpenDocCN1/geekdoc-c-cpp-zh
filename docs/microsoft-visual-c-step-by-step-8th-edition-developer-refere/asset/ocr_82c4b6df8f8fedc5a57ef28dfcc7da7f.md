# Note

The .NET Framework class library also provides another set of collection types in the System.Collections namespace. These are nongeneric collections, and they were designed before C# supported generic types (generics were added to the version of C# developed for the .NET Framework version 2.0). With one exception, these types all store object references, and you are required to perform the appropriate casts when you store and retrieve items. These classes are included for backward compatibility with existing applications, and it is not recommended that you use them when building new solutions. In fact, these classes are not available if you are building Universal Windows Platform (UWP) apps.

The one class that does not store object references is the BitArray class. This class implements a compact array of Boolean values by using an int; each bit indicates true (1) or false (0). If this sounds familiar, it should; this is very similar to the IntBits struct that you saw in the examples in Chapter 16, “Using indexers.” The BitArray class is available to UWP apps.

One other important set of collections is available, and these classes are defined in the System.Collections.Concurrent namespace. These are thread-safe collection classes that you can use when you’re building multithreaded applications. Chapter 24, “Improving response time by performing asynchronous operations,” provides more information on these classes.

# The List<T> collection class

The generic List<T> class is the simplest of the collection classes. You can use it much like you use an array—you can reference an existing element in a List<T> collection by using ordinary array notation, with square brackets and the index of the element, although you cannot use array notation to add new elements. However, in general, the List<T> class provides more flexibility than arrays do and is designed to overcome the following restrictions exhibited by arrays:

+   - If you want to resize an array, you have to create a new array, copy the elements (leaving out some if the new array is smaller), and then update any references to the original array so that they refer to the new array.
+   - If you want to remove an element from an array, you have to move all the trailing elements up by one place. Even this doesn’t quite work because you end up with two copies of the last element.
+   - If you want to insert an element into an array, you have to move elements down by one place to make a free slot. However, you lose the last element