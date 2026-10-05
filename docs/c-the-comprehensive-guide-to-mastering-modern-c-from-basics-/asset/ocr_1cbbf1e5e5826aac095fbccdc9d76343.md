```
int sum = sumJanuary( jan );
}
```

**Listing 6.9** If you need to use an array definition more than once, use “using.”

If you need to store a fixed number of uniform elements, an array is ideal. It serves well especially as a member variable, and also for static data that you type literally into the source code.

Its particular strength is that the data lies directly next to each other in memory, which is useful in many application areas; for example, it can be written to the hard drive particularly quickly as a block.

Otherwise, you can see the useful accumulate and iota functions from the <algorithm> and <numeric> headers, both of which are so-called algorithms. These are auxiliary functions that you can apply to many, if not all, containers. You will learn more about them in other parts of the book. Chapter 25, Section 25.6, they are all listed in detail.

6.4.2 “vector” However, it is impractical to always have a predetermined number of elements in the container. The all-around talent of the container is undoubtedly the vector. Like an array, it only contains elements of one type. Access also works in the same way—namely, via a number index (starting at 0) or via an iterator.

However, the size of the vector is dynamic: it can grow as needed. For example, you can initialize it empty and