The interfaces described in the following list are the generic versions of the respective interfaces. Beginning with C# 2.0, you should always try to use the generic versions of the interfaces for type safety. Chapter 9 discusses the use of generics in the C# language.

| Interface | Description |
|---|---|
| IEnumerable<T> and IEnumerator<T> | Enable you to loop through the elements in a collection. |
| ICollection<T> | Contains items in a collection and provides the functionality to copy elements to an array. Inherits from IEnumerable<T>. |
| IComparer<T> and IComparable<T> | Enable you to compare objects in a collection. |
| IList<T> | Inherits from ICollection and provides functionality to allow members to be accessed by index. |
| IDictionary<K,V> | Similar to IList<T>, but members are accessed by key value rather than index. |

The ICollection<T> interface is the base interface for classes in the System.Collections namespace.

# Dynamic Arrays Using the ArrayList Class

Arrays in C# have a fixed size once they are initialized. For example, the following defines a fixed-size array of five integer elements:

```
int[] num = new int[5];
```

If you need to dynamically increase the size of an array during runtime, use the ArrayList class instead. You use it like an array, but its size can be increased dynamically as required.

The ArrayList class is located within the System.Collections namespace, so you need to import that System.Collections namespace before you use it. The ArrayList class implements the IList interface.

To use the ArrayList class, you first create an instance of it:

```
ArrayList arrayList = new ArrayList();
```

Use the Add() method to add elements to an ArrayList object:

```
arrayList.Add("Hello");
arrayList.Add(25);
arrayList.Add(new Point(3,4));
arrayList.Add(3.14F);
```

Notice that you can add elements of different types to an ArrayList object.