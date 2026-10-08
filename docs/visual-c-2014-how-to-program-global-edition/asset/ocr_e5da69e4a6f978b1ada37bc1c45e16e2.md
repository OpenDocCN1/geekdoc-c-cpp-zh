# Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

| Class | Implements interface | Description |
| --- | --- | --- |
| BitArray | ICollection | A memory-efficient array of bits in which each bit's 0 or 1 represents the bool value false or true. Exercise 21.4 asks you to use a BitArray to implement the Sieve of Eratosthenes algorithm for finding prime numbers. |
| Hashtable | IDictionary | An unordered collection of key-value pairs that can be accessed rapidly by key. |
| Queue | ICollection | A first-in, first-out (FIFO) collection. See 19.6 for information on queues. |
| SortedList | IDictionary | A collection of key-value pairs that are sorted by key and can be accessed either by key or by index. |
| Stack | ICollection | A last-in, first-out (LIFO) collection. See 19.5 for information on stacks.

Fig. 21.2 | .NET Framework collection classes. (Part 2 of 2)

We also discuss the IEnumerator<T> interface. Each class's enumerator allows you to iterate through collection. Although these enumerators have different implementations, they implement the IEnumerator<T> interface so that an app can iterate through a collection's elements (e.g., with a foreach statement). In the next section, we begin our discussion by enumerators and the capabilities for array manipulation. Collection classes directly or indirectly implement ICollection<T> and IEnumerable<T> (or their object-based equivalents ICollection<T> and IEnumerable<T>) with legacy collections.

# 21.3 Class Array and Enumerators

Chapter 8 presented basic array-processing capabilities. All arrays inherit from abstract class Array (namespace System); this class defines Length, which specifies the number of elements in the array. In addition, Array provides static methods that provide algorithms for processing arrays. Typically, class Array overlaps these methods—for example, Array method Reverse can reverse the order of the elements in an array or in a specified range of elements. For a complete list of class Array's static methods

> https://msn.microsoft.com/library/system.array

Figure 21.3 demonstrates several static methods of class Array.

```
// Fig. 21.3: UsingArray.cs
// Array class static methods for common array manipulations.
using System;
using static System.Array;
```

Fig. 21.3 | Array class static methods for common array manipulations. (Part I of 3)