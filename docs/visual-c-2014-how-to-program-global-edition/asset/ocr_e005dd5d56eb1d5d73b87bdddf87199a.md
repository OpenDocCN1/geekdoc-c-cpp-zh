# 9.6 Wrap-Up

declaration would generate a compilation error, because the compiler cannot determine whether you wish to create an array or a collection

```
var items = {"Aqua", "Rust", "yElLow", "rEd"};
```

# 9.6 Wrap-Up

This chapter introduced LINQ (Language Integrated Query), a powerful feature for querying data. We showed how to filter an array or collection using LINQ's where clause, and how to sort the results using the orderby clause. We used the select clause to select specific properties of an object, the let clause to introduce a new variable to make queries more convenient. The StartWith method string was used to filter strings starting with a specific character or series of characters. We used several LINQ extension methods to perform operations not provided by the query—the Distinct method to remove duplicates from the results, the Any method to determine if the results contain any items, and the First method to retrieve the first element in the results.

We introduced List<T> generic collection, which provides all the functionality of arrays, with other useful capabilities such as dynamic resizing. We used method Add to append new items to the end of the List, method Insert to insert new items into specified locations in the List, method Remove to remove the first occurrence of a specified item, method Remove to remove an item at a specified index and method Contains to determine if an item was in the List. We used property Count to get the number of items and Capacity to determine the number of elements the List can hold without growing. We use more advanced features of LINQ in later chapters.

In Chapter 10 we take a deeper look at class concepts. We'll discuss this reference, constructor concepts, how the runtime manages memory with garbage collection, static class members, read-only class members, object initializers and operator overloading.

# 9.7 Deitel LINQ Resource Center

Our LINQ Resource Center (http://www.deitel.com/LINQ/) contains many links to additional information, including blogs by Microsoft LINQ team members, books, sample charts, FAQs, tutorials, webcasts, and more.

# Summary

# Section 9.1 Introduction

+   - .NET's collections provide reusable data structures that are reliable, powerful and efficient.
- Lists automatically increase their size to accommodate additional elements.
- Large amounts of data are often stored in a database—an collection of data. Today's most popular database systems are relational databases. SQL is the international standard used almost universally with relational databases to perform queries (i.e., to request information satisfies given criteria).
- LINQ allows you to write query expressions (similar to SQL queries) that retrieve information from a wide variety of data sources. You can query arrays and Lists, selecting elements that satisfy a set of conditions—this is known as filtering.