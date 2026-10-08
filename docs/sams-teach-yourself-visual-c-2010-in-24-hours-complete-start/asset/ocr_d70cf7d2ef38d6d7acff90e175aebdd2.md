8. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 9.3.

![](bbox=[0.25, 0.16, 0.66, 0.31])

# FIGURE 9.3

Results of using a custom indexer over two instances

# # Generic Collections

Although arrays are the only built-in data structure in C# that supports the concept of a collection of objects, the base class library provides a rich set of collection and collection-related types to supplement them, which provide much more flexibility and enable you to derive custom collections for your own data types.

These types are separated into classes and interfaces, and are further separated in to non-generic and generic collections. The non-generic collections are not type-safe, because they work only with the object type, and are available for backward compatibility with older versions of the .NET Framework. The generic collections are preferred because they provide type-safety and better performance than the non-generic collections. There are almost twice as many generic collections as there are non-generic collections.

# GO TO

Hour 11, “Understanding Generics,” for more information on generic types.

> **Generic Collections in Silverlight**

The Silverlight version of the .NET Framework removes the non-generic collections because there was no legacy code to be compatible with.

# Did you know?

# ## Lists

Within the set of collection types, `List<T>` is the one that could be considered to be closest to an array and is probably the most commonly used collection. Like an array, it is a numerically indexed collection of objects. Unlike an array, a `List<T>` is dynamically sized as needed.

The default capacity for a list is 16 elements. When you add the 17 $^{th}$ element, the size of the list is automatically doubled. If the number (or an approximate number) of elements the list contains is known ahead of time, it can be beneficial to set the initial capacity using one of the overloaded constructors or by setting the Capacity property before adding the first item.