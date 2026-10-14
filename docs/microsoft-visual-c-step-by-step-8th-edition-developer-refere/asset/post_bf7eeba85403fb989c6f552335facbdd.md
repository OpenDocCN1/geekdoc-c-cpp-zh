
Several of the interfaces defined by the .NET Framework exhibit covariance, including the IEnumerable<T> interface, which is detailed in Chapter 19, “Enumerating collections.”

## Note

Only interface and delegate types (which are covered in Chapter 18) can be declared as covariant. You do not specify the out modifier with generic classes.

## Contravariant interfaces

Contravariance follows a similar principle to covariance except that it works in the opposite direction; it enables you to use a generic interface to reference an object of type B through a reference to type A as long as type B derives from type A. This sounds complicated, so it is worth looking at an example from the .NET Framework class library.

The System.Collections.Generic namespace in the .NET Framework provides an interface called IComparer, which looks like this:

```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

A class that implements this interface has to define the Compare method, which is used to compare two objects of the type specified by the T type parameter. The Compare method is expected to return an integer value: zero if the parameters x and y have the same value, negative if x is less than y, and positive if x is greater than y. The following code shows an example that sorts objects according to their hash code. (The GetHashCode method is implemented by the Object class. It simply returns an integer value that identifies the object. All reference types inherit this method and can override it with their own implementations.)

```
class ObjectComparer : IComparer<Object>
{
    int IComparer<Object>.Compare(Object x, Object y)
    {
        int xHash = x.GetHashCode();
        int yHash = y.GetHashCode();

        if (xHash == yHash)
            return 0;

        if (xHash < yHash)
            return -1;
        return 1;
    }
}
```

You can create an ObjectComparer object and call the Compare method through the IComparer<Object> interface to compare two objects, like this:

```
Object x = ...;
Object y = ...;
ObjectComparer objectComparer = new ObjectComparer();
IComparer<Object> objectComparator = objectComparer;
int result = objectComparator.Compare(x, y);
```

That’s the boring bit. What is more interesting is that you can reference this same object through a version of the IComparer interface that compares strings, like this:

```
IComparer<String> stringComparator = objectComparer;
```

At first glance, this statement seems to break every rule of type safety that you can imagine. However, if you think about what the IComparer<T> interface does, this approach makes sense. The purpose of the Compare method is to return a value based on a comparison between the parameters passed in. If you can compare Objects, you certainly should be able to compare Strings, which are just specialized types of Objects. After all, a String should be able to do anything that an Object can do—that is the purpose of inheritance.

This still sounds a little presumptive, however. How does the C# compiler know that you are not going to perform any type-specific operations in the code for the Compare method that might fail if you invoke the method through an interface based on a different type? If you revisit the definition of the IComparer interface, you can see the in qualifier prior to the type parameter:

```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
```

The in keyword tells the C# compiler that you can either pass the type T as the parameter type to methods or pass any type that derives from T. You cannot use T as the return type from any methods. Essentially, this makes it possible for you to reference an object either through a generic interface based on the object type or through a generic interface based on a type that derives from the object type. Basically, if type A exposes some operations, properties, or fields, in that case if

type B derives from type A, it must also expose the same operations (which might behave differently if they have been overridden), properties, and fields. Consequently, it should be safe to substitute an object of type B for an object of type A.

Covariance and contravariance might seem like fringe topics in the world of generics, but they are useful. For example, the List<T> generic collection class (in the System.Collections.Generic namespace) uses IComparer<T> objects to implement the Sort and BinarySearch methods. A List<Object> object can contain a collection of objects of any type, so the Sort and BinarySearch methods need to be able to sort objects of any type. Without using contravariance, the Sort and BinarySearch methods would need to include logic that determines the real types of the items being sorted or searched and then implement a type-specific sort or search mechanism. However, unless you are a mathematician, it can be quite difficult to recall what covariance and contravariance actually do. The way I remember, based on the examples in this section, is as follows:

- **Covariance example** If the methods in a generic interface can return strings, they can also return objects. (All strings are objects.)
- **Contravariance example** If the methods in a generic interface can take object parameters, they can take string parameters. (If you can perform an operation by using an object, you can perform the same operation by using a string because all strings are objects.)

> **Note**
> 
> As with covariance, only interface and delegate types can be declared as contravariant. You do not specify the in modifier with generic classes.

## Summary

In this chapter, you learned how to use generics to create type-safe classes. You saw how to instantiate a generic type by specifying a type parameter. You also saw how to implement a generic interface and define a generic method. Finally, you learned how to define covariant and contravariant generic interfaces that can operate with a hierarchy of types.

- If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 18.
- If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Instantiate an object by using a generic type | Specify the appropriate generic type parameter. For example: `Queue<int> myQueue = new Queue<int>();` |
| Create a new generic type | Define the class by using a type parameter. For example: ``` public class Tree<TItem> { ... } ``` |
| Restrict the type that can be substituted for the generic type parameter | Specify a constraint by using a where clause when defining the class. For example: ``` public class Tree<TItem> where TItem : IComparable<TItem> { ... } ``` |
| Define a generic method | Define the method by using type parameters. For example: ``` static void InsertIntoTree<TItem> (Tree<TItem> tree, params TItem[] data) { ... } ``` |
| Invoke a generic method | Provide types for each of the type parameters. For example: `InsertIntoTree<char>(charTree, 'Z', 'X');` |
| Define a covariant interface | Specify the out qualifier for covariant type parameters. Reference the covariant type parameters only as the return types from methods and not as the types for method parameters: ``` interface IRetrieveWrapper<out T> { T GetData(); } ``` |
| Define a contravariant interface | Specify the in qualifier for contravariant type parameters. Reference the contravariant type parameters only as the types of method parameters and not as return types: ``` public interface IComparer<in T> { int Compare(T x, T y); } ``` |

## Chapter 18. Using collections

After completing this chapter, you will be able to:

- Explain the functionality provided in the different collection classes available with the .NET Framework.
- Create type-safe collections.
- Populate a collection with a set of data.
- Manipulate and access the data items held in a collection.
- Search a list-oriented collection for matching items by using a predicate.

Chapter 10, “Using arrays,” introduces arrays for holding sets of data. Arrays are very useful in this respect, but they have their limitations. Arrays provide only limited functionality; for example, it is not easy to increase or reduce the size of an array, and neither is it a simple matter to sort the data held in an array. Also, arrays only really provide a single means of accessing data—by using an integer index. If your application needs to store and retrieve data by using some other mechanism, such as the first-in, first-out queue mechanism described in Chapter 17, “Introducing generics,” arrays might not be the most suitable data structure to use. This is where collections can prove useful.

## What are collection classes?

The Microsoft .NET Framework provides several classes that collect elements together such that an application can access the elements in specialized ways. These are the collection classes mentioned in Chapter 17, and they live in the System.Collections.Generic namespace.

As the namespace implies, these collections are generic types; they all expect you to provide a type parameter indicating the kind of data that your application will be storing in them. Each collection class is optimized for a particular form of data storage and access, and each provides specialized methods that support this functionality. For example, the Stack<T> class implements a last-in, first-out model, where you add an item to the top of the stack by using the Push method, and you take an item from the top of the stack by using the Pop method. The Pop method always retrieves the most recently pushed item and removes it from the stack. In contrast, the Queue<T> type provides the Enqueue and Dequeue methods described in Chapter 17. The Enqueue method adds an item to the queue, while the Dequeue method retrieves items from the queue in the same order, implementing a first-in, first-out model. A variety of other collection classes are also available, and the following table provides a summary of the most commonly used ones.
