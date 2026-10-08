# 21.14 Wrap-Up 921

Web Resources
For a list of covariant and contravariant interface types, visit

```
https://msdn.microsoft.com/library/dd799517#VariantList
```

It's also possible to create your own types that support covariance and contravariance. For information, visit

```
https://msdn.microsoft.com/library/mt654058
```

# 21.14 Wrap-Up

This chapter introduced the packaged collection classes provided by the .NET Framework. We presented the hierarchy of interfaces that manage the collection classes implementation, overview of the implementation classes and introduced enumerators that enable programs to iterate through collections.

We discussed the .NET namespaces dedicated to collections, including System.Collections for object-based collections and System.Collections.Generic for generic collections—such as List<T>, Dictionary<K,V>, and SortedDictionary<K,V> classes—that store objects of types you specify when you create the collection. We also mentioned the namespace System.Collections.Concurrent containing thread-safe generic collections for use in multithreaded applications, and System.Collections.Specialized containing collections that are optimized for specific scenarios, such as manipulating collections of bits.

You how to use class Array to perform array manipulations. We continued our discussion of delegates that hold references to methods and introduced lambda expressions, which allow you to define anonymous methods that can be used with delegates. We focused on using lambdas to pass method references to methods that specify delegate parameters.

We provided a brief introduction to functional programming, showing how to write code concisely and with fewer bugs than programs with previous techniques. In particular, we used LINQ extension methods and lambdas to implement functional operations that manipulated lists of values.

In Chapter 22, we begin our discussion of databases, which organize data in a way that the data can be selected and updated quickly. We introduce the ADO.NET Entity Framework and LINQ to Entities, which allow you to write LINQ queries that are used to query databases.

# Summary

# Section 21.1 Introduction

+   - The packaged data-structure classes provided by the .NET Framework are known as collection classes—they store collections of data.
- With collection classes, instead of creating data structures to store these sets of items, you simply use existing data structures, without concern for how they're implemented.