
- Contravariance example: If the methods in a generic interface can take object parameters, they can take string parameters. (If you perform an operation by using an object, you can perform the same operation by using string because all strings are objects.)

> Note As with covariance, only interface and delegate types can be declared as contravariant. You don't specify the in modifier with generic classes.

## Summary

In this chapter, you learned how to use generics to create type-safe classes. You saw how to instantiate a generic type by specifying a type parameter. You also saw how to implement a generic interface and define a generic method. Finally, you learned to define covariant and contravariant generic interfaces that can operate with a hierarchy of types.

- If you want to continue to the next chapter, keep Visual Studio 2022 running and turn to Chapter 18.
- If you want to exit Visual Studio 2022 now, on the File menu, select Exit. If you see a Save dialog, select Yes and save the project.

## Quick reference

| To | Do this |
| --- | --- |
| Instantiate an object by using a generic type | Specify the appropriate generic type parameter. For example:
Click here to view code image
`Queue<int> myQueue = new Queue<int>();` |
| Create a new generic type | Define the class by using a type parameter. For example:
`public class Tree<TItem>(` ... } |
| Restrict the type that can be substituted for the generic type parameter | Specify a constraint by using a where clause when defining the class. For example:
Click here to view code image
```
public class Tree<TItem>
where TItem : IComparable<TItem>
{
  ...
``` |
| Define a generic method | Define the method by using type parameters. For example:
Click here to view code image
```
static void InsertIntoTree<TItem>
(Tree<TItem> tree, params TItem[] data)
{
  ...
``` |
| Invoke a generic method | Provide types for each of the type parameters. For example:
Click here to view code image
```
InsertIntoTree<char>(charTree, 'Z', 'X');
``` |
| Define a covariant interface | Specify the out qualifier for covariant type parameters. Reference the covariant type parameters only as the return types from methods and not as the types for method parameters:
Click here to view code image
```
interface IRetrieveWrapper<out T>
{
  T GetData();
}
``` |
| Define a contravariant interface | Specify the in qualifier for contravariant type parameters. Reference the contravariant type parameters only as the types of method parameters and not as return types:
Click here to view code image
```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
``` |

# Chapter 18

# Using collections

After completing this chapter, you will be able to:

- Explain the functionality provided in the different collection classes available with .NET and understand how to use them.
- Use collection initializers to populate collections.
- Search through collections to find matching data.
- Understand the differences between collections and arrays.

Chapter 10, “Using arrays,” introduced arrays for holding sets of data. Arrays are very useful in this respect, but they have their drawbacks. Arrays provide only limited functionality; for example, it’s not easy to increase or reduce the size of an array, and neither is it simple matter to sort the data in an array. Also, arrays only provide a simple means of accessing data: by using an integer index. If your application needs to use some other mechanism to store and retrieve data, such as the first-in, first-out mechanism described in Chapter 17, “Introducing generics,” arrays might not be the most suitable data structure. This is where collections prove useful.

## What are collection classes?

Microsoft .NET provides several classes that collect elements in specialized ways. These are the collection classes mentioned in Chapter 17, and they live in the `System.Collections` and `System.Collections.Generic` namespace.

As the namespace indicates, these collections are generic types; they expect to provide a type parameter indicating the kind of data your application will store in them. Each collection class is optimized for a particular form of data storage and access, and each provides specialized methods that support this functionality. For example, the `Stack<T>` class implements a last-in, first-out model, where you add an item to the top of the stack using the `Push` method, and you take an item from the top of the stack by using the `Pop` method. The `Pop` method always retrieves the most recently pushed item and removes it from the stack. In contrast, the Queue<T> type provides the Enqueue and Dequeue methods described in Chapter 17. The Enqueue method adds an item to the queue, while the Dequeue method retrieves items from the queue in the same order, implementing a first-in, first-out model. A variety of other collection classes are also available; the following table summarizes the most commonly used ones.

| Collection | Description |
| --- | --- |
| List<T> | A list of objects that can be accessed by index, as with an array, with additional methods with search the list and sort the contents of the list. |
| Queue<T> | A first-in, first-out data structure, with methods to add an item to one end of the queue, remove an item from the other end, and examine an item without removing it. |
| PriorityQueue<TElement, TPriority> | A queue that sorts data by priority. Elements of a higher priority are dequeued before those of a lower priority. |
| Stack<T> | A first-in, last-out data structure with methods to push an item onto the top of the stack, pop an item from the top of the stack, and examine the item from the top of the stack without removing it. |
| LinkedList<T> | A double-ended ordered list, optimized to insertion and removal at either end. This collection can act like a queue or a stack, but it also supports random access as a list does. |
| HashSet<T> | An unordered set of values that is optimized for fast retrieval of data. It provides methods for determining whether the items it holds are a subset of another HashSet<T> object as well as computing the intersection and union of HashSet<T> objects. |
| Dictionary<TKey, TValue> | A collection of values that can be identified and retrieved using keys rather than indexes. |
| SortedList<TKey, TValue> | A sorted list of key/value pairs. The keys must implement the IComparable<T> interface. |

The following sections provide a brief overview of these classes. Refer to the .NET class library documentation for each class.

## .NET class library collection types

The .NET class library provides another set of collection types in the System.Collections namespace. These are non-generic collections, and they were designed before C# generic types (Generics were added to the version of C# developed for .NET 2.0.) With one exception, these types store object references, and are required to perform the appropriate casts when you store and retrieve items. These classes are included for backward compatibility with existing applications, and it is not recommended that you use them when building new solutions. In fact, these classes are not available if you're building Universal Windows Platform (UWP) apps.

One class that does not store object references is the BitArray class. This class implements a compact array of Boolean values using an int; each bit indicates true (1) or false (0). If this sounds familiar, it should; this is very similar to the IntBits struct that you saw in Chapter 16, "Handling binary data and using indexers." The BitArray class is available to UWP apps.

One other set of collections is available, which are defined in the System.Collections.Concurrent namespace. These are thread-safe collection classes that you can use when you're building multithreaded applications. Chapter 24, "Improving response time by performing asynchronous operations," provides more information on these classes.

## The List<T> collection class

The generic List<T> class is the simplest of the collection classes. You can use it much like you use an array. You can reference an existing element in a List<T> collection by using array notation, with square brackets and the index of
