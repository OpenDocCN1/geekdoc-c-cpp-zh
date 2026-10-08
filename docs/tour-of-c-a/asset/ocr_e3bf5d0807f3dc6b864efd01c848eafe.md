# How can I call C and C++ siblings? Look at a simplified family tree:

![](bbox=[0.301, 0.125, 0.663, 0.633])

Classic C has two main descendants: ISO C and ISO C++. Over the years, these languages have evolved at different paces and in different directions. One result of this is that each language provides support for traditional C-style programming in slightly different ways. The resulting incompatibilities can make life miserable for people who use both better and C++, for people who write in one language using libraries imported in the other, and tools for C and C++.

A solid line means a massive inheritance of features, a dotted line a borrowing of minor features. From this, ISO C and ISO C++ emerge as the two major descendants of K&R C [Kernighan,1978], and as siblings. Each carries with it the key aspects of Classic C, and neither is 100% compatible with Classic C. I picked the term “Classic C” from a sticker that was used to be affixed Dennis Ritchie's terminal. It is K&R C plus enumerations and struct assignment. BCPL is defined by [Richards,1980] and C89 by [C1990].